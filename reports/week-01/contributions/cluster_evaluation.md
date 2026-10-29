# Week 1 Report: Cluster Evaluation

## Completed

- Implemented the public `ClusterEvaluator` class in `include/k_means/Cluster_Evaluator.hpp` and `src/Cluster_evaluation.cpp`.
- The API uses `Point = std::vector<double>` and `Dataset = std::vector<Point>`; it is not a fixed two-dimensional `Point` struct.
- `computeInertia(points, labels, centroids)` sums squared Euclidean distances from each point to the centroid identified by its label. It validates nonempty inputs, matching dimensions, finite values, label count, and label range; malformed inputs raise standard exceptions.
- The class has no stored state and its constructor is deleted. Inertia is evaluated after labels have been assigned to the final centroids.

## In Progress

- Integrating the evaluator with the example workflow and maintaining coverage for malformed inputs and expected inertia values.

## Challenges / Blockers

- Earlier prototype notes described standalone helpers and a 2D structure. The current library API is a static class operating on vectors of arbitrary feature dimension.

## Next Week

- Use the evaluator with the final assignment step and describe whether reported inertia is calculated in scaled or original feature space.
