# BUSULWA GERRYSON ISRAEL 25/U/0826 BELE

# Week 1 Progress Report: Centroid Initialization

## Completed

- Implemented the `CentroidInitializer` class, which selects `k` distinct existing data rows as initial centroids by shuffling row indices.
- The class stores `k_` and a `std::mt19937` generator privately. Its public API includes constructors with a random-device seed or a caller-provided seed, `getK()`, `setK()`, and `initialize()`.
- Invalid `k` is rejected by the constructors/setter. `initialize()` throws `std::invalid_argument` for empty data, `k` greater than the number of rows, ragged or zero-feature data, or non-finite values.
- A fixed seed makes selection repeatable. This implementation uses distinct-row random initialization; it does not implement K-Means++.

## In Progress

- Integrating the initialized centroids with assignment, update, convergence, and empty-cluster handling.

## Challenges / Blockers

- The initial procedural prototype was replaced by the current stateful class API. Reports should refer to `CentroidInitializer::initialize`, not the old free function or an empty-result error contract.

## Next Week

- Exercise seeded and unseeded initialization through the CMake test target and use the result in the example clustering loop.
