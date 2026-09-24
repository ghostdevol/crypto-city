# CryptoCity

A real crypto economy in a 3D world. Not a game — a place where you can run an
actual business from a digital storefront: real wallets, real transactions,
real ownership, on-chain.

Walk into one building and you're in your wallet. Another is the bank with
your portfolio. The museum is the NFT store. The casino runs real games.
Storefronts are ownable, rentable, real estate — with deeds and rental
agreements as smart contracts.

## Status

Foundation phase. The repo, license, plans, and contract specs come before
build. See `docs/`.

## What's here

| Path          | What                                                      |
|---------------|-----------------------------------------------------------|
| `docs/`       | Vision, roadmap, architecture, economy, contract specs     |
| `contracts/`  | Smart contracts (Solidity) — deeds, rentals, marketplace  |
| `world/`      | Unity 3D world client                                     |
| `apps/`       | CryptoCity apps — GhostSuite (wallet/bank) lives here     |

## Docs

- `docs/vision.md` — what CryptoCity is and why
- `docs/roadmap.md` — phased build plan
- `docs/architecture.md` — how the pieces connect
- `docs/economy.md` — land, deeds, rentals, storefronts, fees
- `docs/contracts.md` — smart contract specifications
- `docs/assets.md` — mesh generation: user assets vs dev world-building

## Apps

**GhostSuite** — the self-custody wallet, chain explorer, and address
forensics suite. It's the bank building in CryptoCity and the wallet rail for
every transaction in the world. Ships as a Tauri desktop app today; the world
bridge comes next.

## License

Business Source License 1.1 — see `LICENSE`. Source is visible; commercial
production use requires a license from GhosTech. Converts to Apache 2.0 on
the change date.

> The license has not been reviewed by an attorney. Get one before real
> money touches this.

## Who builds this

Daniel James Sielaff (ghostdevol) — GhosTech.
