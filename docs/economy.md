# CryptoCity Economy

## Land

- The city is a grid. Each plot is a fixed-size parcel.
- Plots are scarce by design — the city has a fixed footprint per district.
- New districts open by governance/owner decision, not inflation.

## Deeds (ownership)

- Each plot is an ERC-721 NFT: the deed.
- Holding the deed = owning the plot. Transfer the deed, transfer the land.
- The deed's token ID maps to a plot coordinate in the city.
- Deed metadata: district, coordinates, size (sq ft), zoning
  (commercial / residential / entertainment).

## Square feet (fractional)

- Large plots can be fractionalized into ERC-1155 shares (per sq ft).
- Enables shared ownership, investment syndicates, REIT-style pools.
- Shareholders vote on plot use; revenue splits pro-rata on-chain.

## Rentals

- Plot owners list space for rent via the rental contract.
- Rental agreement terms (all on-chain):
  - Duration (blocks or timestamps)
  - Rent amount + payment token + interval
  - Deposit (held in escrow, auto-released)
  - Permitted use / zoning compliance
  - Early termination conditions
- Rent auto-pays per interval. Missed payment → grace period → eviction
  (occupancy rights revoked on-chain, building access removed in-world).
- Subletting allowed unless the agreement forbids it.

## Storefronts

- A rented or owned commercial plot can run a storefront.
- Storefront kit (no coding): inventory list, prices, open/closed sign,
  branding.
- Sales go through the marketplace contract:
  - Customer pays → escrow → item/event delivered → funds split
  - Split: seller (net of protocol fee), protocol fee to city treasury
- Protocol fee: small, fixed, published. (TBD — e.g. 2.5%)

## Entertainment

Games are businesses. The entertainment district runs on the same rails
as everything else — pay to play, prizes in crypto, all on-chain.

- **Casino** — real on-chain games (slots, tables). Provably fair,
  house edge published.
- **Mini-games** — golf, go-karts, paintball, billiards, whatever devs build.
  Entry fees in crypto, tournament pots, leaderboards.
- **Events** — concerts, tournaments, openings. Ticket sales on-chain,
  sponsor slots (see Advertising).

Anyone can open a venue on their commercial plot. The city doesn't run the
games — it provides the streets, the deeds, and the payment rails.

## Advertising

The city is foot traffic — and foot traffic is ad inventory.

- **Billboards** — designated ad plots (high-traffic intersections, plazas).
  Auctioned per time slot, paid in crypto. Billboard owners (deed holders
  of ad-zoned plots) get the revenue minus protocol fee.
- **Building wraps** — plot owners can sell their building's exterior as
  ad space. Their building, their deal, settled on-chain.
- **Sponsored districts** — naming rights for districts/plazas. Highest
  bidder per season.
- **Featured placement** — storefronts pay for highlighted pins on the city
  map and directory. Discovery as a service.
- **Event sponsorships** — in-world events (tournaments, openings, concerts)
  with sponsor slots.

All ad placements are time-boxed, on-chain, and transparent — no dark
patterns, no tracking. Advertisers pay for placement, not for user data.

**Ad philosophy:** ambient, never interruptive. Billboards, video screens,
building wraps — things you see walking around, like a real city. No pop-ups,
no forced views, no modals blocking your path. If you don't want to look at
it, you just keep walking.

## Treasury

- Protocol fees accrue to the city treasury (multisig).
- Funds: development, audits, infrastructure, district expansion.

## What the city never does

- Never holds user keys or funds outside escrowed contract logic.
- Never mints deeds beyond the published district supply.
- Never changes the protocol fee without a published notice period.
