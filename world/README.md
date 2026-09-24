# World

The Unity 3D client lives here.

Planned structure:

- `Assets/CryptoCity/` — city scenes, building prefabs, avatar controllers
- `Assets/CryptoCity/Scripts/` — bridge client (WebSocket), plot renderer,
  deed linkage, storefront UI

Bridge protocol: localhost WebSocket, JSON. The world never holds keys —
it requests signatures from GhostSuite. See `../docs/architecture.md`.
