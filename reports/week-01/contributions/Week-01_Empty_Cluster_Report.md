# Week 1 Progress Report: Empty-Cluster Handling

## Completed

- Implemented the `handleEmptyClusters` operation declared in `include/k_means/EmptyCluster.hpp` and defined in `src/EmptyCluster.cpp`.
- This component is a free function, not a class. It accepts the data by const reference and updates centroid and label vectors by reference.
- For each empty cluster, it moves the farthest eligible point from a donor cluster that has more than one point. It updates that point's label and sets the empty cluster's centroid to the moved point.
- It validates data, centroid, label, dimension, and finite-value constraints. If no point can be moved without emptying a donor cluster, it throws `std::invalid_argument`.

## In Progress

- Integrating repair after nearest-centroid assignment and before centroid update, so the update step receives the repaired labels.

## Challenges / Blockers

- Moving a point from a one-point cluster would create another empty cluster. The handler therefore only chooses donor clusters with multiple assigned points and moves any one point at most once per call.

## Next Week

- Exercise multiple empty clusters and impossible-to-repopulate inputs through the module test and the full clustering example.
