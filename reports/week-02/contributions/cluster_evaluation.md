# Week 2 Report: Cluster Evaluation

## 1. What class did you create?

I created the `ClusterEvaluator` utility class. Its public aliases are `Point` (`std::vector<double>`) and `Dataset` (`std::vector<Point>`); the library does not use a separate fixed two-coordinate `Point` struct.

## 2. Why?

K-Means needs a measure of how closely points fit their assigned centroids. Inertia provides the sum of squared distances within the assigned clusters and can be used to evaluate a clustering result.

## 3. What data does it hold?

The class has no member data. All inputs are passed to the static evaluation function.

## 4. What functions operate on that data?

`computeInertia(points, labels, centroids)` validates that inputs are nonempty, dimensions and label counts agree, coordinates are finite, and each label is a valid centroid index. It returns the sum of squared Euclidean distances. Invalid input raises a standard exception; excessive results raise `std::overflow_error`.

## 5. How is the class used?

The class is stateless and its constructor is deleted, so callers invoke `ClusterEvaluator::computeInertia(...)` directly. The example assigns points against the final centroids before computing inertia. With the example's scaling pipeline, its inertia is in scaled feature space.
