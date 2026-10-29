# Week 1 Progress Report: Cluster Assignment

## Completed

- Implemented `ClusterAssignment` in `include/k_means/ClusterAssignment.hpp` and `src/ClusterAssignment.cpp` as a stateless utility class.
- `assignClusters(data, centroids)` calculates squared Euclidean distance from each point to each centroid and returns the nearest centroid index for every point.
- Equal-distance ties resolve to the lowest centroid index. The function validates nonempty data and centroids, consistent nonzero dimensions, finite coordinates, and throws `std::invalid_argument` for invalid input.
- The function leaves the input matrices unchanged and returns zero-based integer labels.

## In Progress

- Integrating the assignment result with centroid updates, empty-cluster repair, and convergence checks in the K-Means iteration.

## Challenges / Blockers

- Assignment requires compatible point and centroid dimensions. The module validates this before comparing distances so malformed data does not produce misleading labels.

## Next Week

- Use the returned labels in centroid update and exercise tie and invalid-input cases through the registered module test.
