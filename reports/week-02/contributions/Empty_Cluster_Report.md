# Week 2 Report: Empty-Cluster Handling

## 1. What component did you create?

The empty-cluster handling component is the free function `handleEmptyClusters`, declared in `include/k_means/EmptyCluster.hpp` and implemented in `src/EmptyCluster.cpp`. It is not a class.

## 2. Why?

Nearest-centroid assignment can leave a centroid with no assigned observations. This function repairs those empty clusters before centroid update, so a cluster can be repopulated during an iteration.

## 3. What data does it hold?

The function has no persistent state. It receives the dataset as a const reference and modifies the centroid and assignment vectors passed by reference.

## 4. What operations does it perform?

`handleEmptyClusters(data, centroids, assignments)` validates nonempty inputs, matching row/label counts, dimensions, finite coordinates, and label ranges. For each empty cluster, it selects the farthest eligible point whose donor cluster has more than one point, moves that point's label, and sets the empty cluster's centroid to the point. A point is moved at most once during a call. If there is no eligible donor point, it throws `std::invalid_argument`.

## 5. How is the component used by the rest of the program?

The caller invokes it after assigning points and before calling `CentroidUpdater::update`. Because it changes labels and centroids in place, the caller uses the repaired assignments for the following update and convergence check. The library does not automatically invoke this free function; the caller coordinates the workflow.
