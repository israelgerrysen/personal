# SEBBOWA MASAMBILA ABRAHAM 25/U/04087/PS

# Week 1 Progress Report: Distance Calculation

## Completed

- Implemented the `DistanceCalculator` utility declared in `include/k_means/Distance_Calculation.hpp` and implemented in `src/Distance_calculation.cpp`.
- `distance(p1, p2)` returns Euclidean distance; `squareddistance(p1, p2)` returns squared Euclidean distance, which is sufficient for nearest-centroid comparisons.
- Both operations validate matching dimensions and finite coordinates and throw `std::invalid_argument` for invalid inputs. Points are vectors and may have any positive number of features.
- Cluster assignment now uses squared distance to choose the closest centroid. The constructor is deleted because all operations are static.

## In Progress

- Reviewing how the common distance calculation is used throughout clustering and evaluation.

## Challenges / Blockers

- An earlier standalone function name did not match between its declaration and implementation. The current library has a consistent `DistanceCalculator` API.

## Next Week

- Continue integration with assignment and evaluation, and keep the documented interface aligned with the public header.
