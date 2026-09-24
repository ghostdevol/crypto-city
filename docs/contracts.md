# CryptoCity Smart Contract Specifications

> Specs first, code second. Every contract below gets a full Solidity
> implementation, test suite, and testnet deployment before mainnet.
> OpenZeppelin base contracts throughout. External audit before mainnet.

## 1. PlotDeed (ERC-721)

Own the land.

- `mintPlot(district, x, y, sizeSqFt, zoning)` — owner/manager only, capped
  per-district supply
- Token ID → plot coordinate mapping, on-chain
- Metadata: district name, coordinates, sq ft, zoning, image (render)
- Standard ERC-721 transfers; marketplace-compatible

## 2. PlotShares (ERC-1155)

Fractional square feet.

- Plot owner fractionalizes a deed into N shares (locks the ERC-721 in escrow)
- Share ID = deed token ID; fungible within a plot
- Revenue splitter: payments to the plot split pro-rata to shareholders
- Reconstitution: 100% of shares → unlock the deed

## 3. RentalAgreement

Rent the space. Terms are the contract.

State per agreement:
- `plotId`, `landlord`, `tenant`
- `rentAmount`, `payToken`, `payInterval` (seconds)
- `startTime`, `endTime`
- `deposit` (escrowed)
- `gracePeriod`, `evicted` flag

Functions:
- `createAgreement(...)` — landlord lists terms, tenant accepts + pays deposit
- `payRent()` — permissionless (anyone can pay on tenant's behalf)
- `checkEviction()` — permissionless; if past due + grace, marks evicted,
  releases occupancy, returns deposit per terms
- `terminate()` — mutual or per-agreement conditions
- `releaseDeposit()` — auto on clean exit

Events: `AgreementCreated`, `RentPaid`, `Evicted`, `Terminated`.

## 4. Marketplace

Buy from storefronts.

- `listItem(storefrontId, itemId, price, payToken, metadataURI)`
- `buyItem(listingId)` — escrow: payment in → delivery window →
  release to seller minus protocol fee
- `protocolFeeBps` — published, changeable only with notice period
- Dispute hook: escrow held, resolution path (v1: landlord/arbiter multisig)

## 5. CityTreasury

- Receives protocol fees
- Multisig-controlled (owner set at deploy)
- `allocate(to, amount, purpose)` — on-chain record of spend

## Deployment order (Sepolia)

1. PlotDeed
2. PlotShares
3. RentalAgreement
4. Marketplace
5. CityTreasury

## Security requirements

- No upgradeable proxies in v1 (immutable = trustable)
- Reentrancy guards on all payment flows
- Pull-over-push for withdrawals
- Full Foundry/Hardhat test suite, 100% branch coverage on money paths
- External audit before mainnet — non-negotiable with real money
