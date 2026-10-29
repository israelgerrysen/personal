# Week 2 Final Report

## Class Structure and Implementation: K-Means Library Modules

### 1. What classes and components are included?

The current library exposes ten module pairs: `DataLoader`, `DataPreprocessor`, `FeatureScaler`, `CentroidInitializer`, `DistanceCalculator`, `ClusterAssignment`, `CentroidUpdater`, `ConvergenceDetector`, `ClusterEvaluator`, and the `handleEmptyClusters` free function. The assignment, distance, update, and evaluation utilities use static methods; `CentroidInitializer`, `FeatureScaler`, and `ConvergenceDetector` hold configuration or fitted state. Empty-cluster handling is a free function rather than a class.

### 2. Why are these components separate?

Each module owns one K-Means stage: reading numeric data, cleaning and scaling it, choosing initial centroids, assigning points, repairing empty clusters, updating means, deciding when to stop, or measuring inertia. Keeping these operations separate makes them reusable and testable. The library does not expose one monolithic estimator; the caller controls the sequence.

### 3. What data do the components hold?

Most utility components have no persistent data. `CentroidInitializer` stores the cluster count and random generator. `FeatureScaler` stores its method, per-feature offsets and scales, and fitted status. `ConvergenceDetector` stores a tolerance and maximum iteration count. Dataset points and centroids are represented as vectors of `double`; labels are integer centroid indices.

### 4. What functions operate on the data?

- `DataLoader::loadCSV` loads a header-based CSV, optionally selecting and ordering columns. Invalid numeric cells become NaN; malformed row widths and CSV quoting are rejected.
- `DataPreprocessor` drops columns or rows with missing values, imputes missing values by mean/median/mode, and one-hot encodes a separate category vector.
- `FeatureScaler` fits and applies MinMax or standard scaling and can inverse-transform results.
- `CentroidInitializer::initialize` selects `k` distinct rows; a seed makes the random selection repeatable.
- `DistanceCalculator` calculates Euclidean or squared Euclidean distance. `ClusterAssignment::assignClusters` returns the nearest-centroid label for each point, resolving ties in favor of the lowest index.
- `handleEmptyClusters` moves eligible farthest points from donor clusters with more than one point into empty clusters, updating labels and centroid positions.
- `CentroidUpdater::update` returns means for nonempty clusters and leaves an empty cluster's prior centroid in place.
- `ConvergenceDetector` checks centroid movement, unchanged assignments, or the iteration limit.
- `ClusterEvaluator::computeInertia` calculates the sum of squared distances to assigned centroids.

### 5. How are access and use organized?

Each public header declares the API; its matching source file implements it. Stateless utilities expose public static operations and generally delete their constructors. Stateful classes hide their fields and validate configuration through their public interfaces. The caller typically loads or supplies data, preprocesses and scales it, initializes centroids, then repeats assignment, empty-cluster repair, update, and convergence checks. The caller should reassign points against the final centroids before evaluating inertia.

## Week 2 contribution reports included

- `contributions/Week-02_Report dataLoader.md`
- `contributions/data_preprocessor.md`
- `contributions/feature_scaler.md`
- `contributions/report_centroidinitializer_class(week-02).md`
- `contributions/DistanceCalculation week2.md`
- `contributions/Cluster_Assignment_Class_Report( week 02).md`
- `contributions/Centroid_Update(week-02).md`
- `contributions/week-02(convergencedetection).md`
- `contributions/cluster_evaluation.md`
- `contributions/Empty_Cluster_Report.md`

## Public header and implementation coverage

| Module | Public header | Matching implementation |
|---|---|---|
| `DataLoader` | `include/k_means/DataLoader.hpp` | `src/DataLoader.cpp` |
| `DataPreprocessor` | `include/k_means/DataPreprocessor.hpp` | `src/DataPreprocessor.cpp` |
| `FeatureScaler` | `include/k_means/feature_scaler.hpp` | `src/feature_scaler.cpp` |
| `CentroidInitializer` | `include/k_means/Centroid_initialization.hpp` | `src/Centroid_initialization.cpp` |
| `DistanceCalculator` | `include/k_means/Distance_Calculation.hpp` | `src/Distance_calculation.cpp` |
| `ClusterAssignment` | `include/k_means/ClusterAssignment.hpp` | `src/ClusterAssignment.cpp` |
| `CentroidUpdater` | `include/k_means/Centroid_Update.hpp` | `src/Centroid_Update.cpp` |
| `ConvergenceDetector` | `include/k_means/ConvergenceDetector.hpp` | `src/ConvergenceDetector.cpp` |
| `EmptyCluster` function | `include/k_means/EmptyCluster.hpp` | `src/EmptyCluster.cpp` |
| `ClusterEvaluator` | `include/k_means/Cluster_Evaluator.hpp` | `src/Cluster_evaluation.cpp` |
