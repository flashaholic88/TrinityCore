# Bolt's Journal ⚡

## 2026-07-22 - Reusable Map scratchpads for Map::Update
**Learning:** In TrinityCore's MapUpdater, each Map instance is updated sequentially by a single thread at a time. This unique single-threaded map update design allows us to safely use Map member variables as scratchpad containers (such as std::vector or std::unordered_set) without needing thread synchronization, significantly reducing heap allocation churn in the extremely hot Map::Update path.
**Action:** Always identify sequential update patterns and leverage Map or other class-level member variables as reusable scratchpads instead of local vectors or sets to completely avoid heap allocations in critical hot loops.
