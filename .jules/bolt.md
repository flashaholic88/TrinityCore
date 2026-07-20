# Bolt's Performance Journal

## 2026-07-20 - Sequential Map Updates and Scratchpads
**Learning:** In TrinityCore, `Map::Update` runs sequentially on single threads, meaning map member variables can be safely used as scratchpad containers (such as `std::vector` and `std::unordered_set`) without any thread-safety or synchronization overhead. Reusing these member containers completely eliminates the high frequency of dynamic heap allocations/deallocations in the update loop (which occurs every tick for every active player and object).
**Action:** Always look for transient collection patterns (like vectors or sets allocated per-player/per-tick inside map or session loops) and refactor them to use class-level scratchpads, ensuring they are cleared before each usage and fully cleared at the end of the update call to avoid dangling raw pointers.
