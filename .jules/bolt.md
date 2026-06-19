
## 2026-06-17 - [Optimization of Core Utility: Trinity::Tokenize]
**Learning:** Core utility functions like `Tokenize` are used in nearly 100 locations, including database loading and packet parsing. Small improvements here have an amplified effect. Pre-calculating `std::vector` capacity with `reserve` is a low-risk, high-reward optimization in such high-frequency code paths.
**Action:** Always check core utility functions (`StringReplaceAll`, `Tokenize`, `ByteArrayToHexStr`) for potential memory allocation optimizations when working in C++ codebases.
