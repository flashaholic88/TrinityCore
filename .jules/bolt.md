## 2025-05-15 - [Map::Update Scratchpad Optimization]
**Learning:** In TrinityCore, `Map::Update` is a high-frequency hot path executed for every active map. Local `std::vector` and `std::unordered_set` allocations within this loop, especially per-player, cause significant heap churn. Reusing member variables as scratchpads is safe here because map updates are sequential per instance.
**Action:** Always check the most frequent update loops (Map, World, Object) for local container allocations and move them to class members with `.clear()` to reuse capacity.
