# CryptoCity Architecture

## The pattern

Unity world as the client, JS services as the backends, one per building.
They talk over a localhost WebSocket bridge with a tiny JSON protocol.

```
┌─────────────────────────────────────────────────┐
│                   UNITY WORLD                    │
│  streets · buildings · avatars · storefronts     │
└──────────┬──────────────────────┬────────────────┘
           │ WebSocket (JSON)     │
           ▼                      ▼
┌─────────────────────┐  ┌──────────────────────┐
│     GhostSuite      │  │   Building services   │
│  wallet / bank /    │  │  casino · museum ·    │
│  signing / portfolio│  │  explorer · shops     │
└─────────────────────┘  └──────────────────────┘
           │                      │
           ▼                      ▼
┌─────────────────────────────────────────────────┐
│                  EVM CHAINS                       │
│  deeds · rentals · marketplace · payments         │
└─────────────────────────────────────────────────┘
```

## Components

### World (Unity)

- Renders the city, buildings, avatars
- Owns movement, presence, chat
- Never touches private keys — it asks GhostSuite to sign

### Bridge

- Localhost WebSocket, JSON messages
- Message types: `sign_request`, `sign_response`, `chain_read`,
  `contract_call`, `event_subscribe`
- The world never sees a seed phrase. Signing happens in GhostSuite,
  user confirms, signature comes back.

### GhostSuite

- Self-custody wallet (already shipped as Tauri app)
- In CryptoCity it runs as the wallet backend: holds keys, signs
  transactions the world requests, shows portfolio in the bank building

### Contracts

- Deeds, rentals, marketplace, protocol fees
- Deployed on EVM chains; Sepolia first, mainnet after audit
- See `contracts.md` for specs

## Data flow: buying from a storefront

1. Customer walks in, picks a product
2. World sends `contract_call` → marketplace contract (price, item)
3. GhostSuite pops a sign request — customer confirms
4. Transaction hits chain; world listens for the event
5. Item transfers, payment splits (seller + protocol fee)
6. Both parties see it settle in-world in real time
