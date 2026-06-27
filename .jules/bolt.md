## 2025-06-27 - [Map::Update Optimization]
**Learning:** In Map::Update, frequently used temporary containers (vectors and sets) for unit visitation were being reallocated every tick for every player. Reusing these as member variables in the Map class (which is updated sequentially by one thread at a time) significantly reduces heap churn.
**Action:** Always look for high-frequency loops where temporary containers are used, and consider promoting them to scratchpad member variables if thread safety is guaranteed by the architecture.
