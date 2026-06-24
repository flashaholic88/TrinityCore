## 2024-11-20 - Frequent heap allocations in Map::Update
**Learning:** `Map::Update` contains a loop over all players where `std::vector` and `std::unordered_set` containers are allocated locally on every tick to track units that need visibility updates. This causes high allocation frequency in a hot path.
**Action:** Move these containers to be members of the `Map` class and reuse them by calling `clear()` to preserve their capacity.
