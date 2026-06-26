
## 2026-06-20 - Map::Update Scratchpad Optimization
**Learning:** In TrinityCore's MapUpdater, each Map instance is updated sequentially by a single thread at a time. This allows for the use of Map member variables as scratchpad containers (e.g., for unit visitation) without requiring thread synchronization.
**Action:** Use Map member variables for temporary containers in the Map::Update loop to avoid repeated allocations every tick, especially within the player loop.
