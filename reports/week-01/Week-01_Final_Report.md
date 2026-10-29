# Week 1 Final Report

## Aim

Establish the library's core K-Means modules and public interfaces. This report combines the Week 1 module contribution reports and records how those components fit the current codebase.

## Completed

- **Dataset loading — `DataLoader`:** reads header-based CSV data into a numeric matrix, supports selection and ordering of zero-based columns, preserves invalid numeric cells as NaN, and rejects malformed CSV structure.
- **Data preprocessing — `DataPreprocessor`:** removes columns or rows with missing values, imputes missing values with mean, median, or mode, and appends one-hot columns from separately supplied category strings.
- **Feature scaling — `FeatureScaler`:** fits MinMax or standardization statistics, transforms and inverse-transforms matrices, and tracks fitted state.
- **Centroid initialization — `CentroidInitializer`:** selects `k` distinct observations, with optional seed for repeatability and validation of invalid data and cluster counts.
- **Distance calculation — `DistanceCalculator`:** supplies Euclidean and squared Euclidean distance for finite, equal-dimension points.
- **Cluster assignment — `ClusterAssignment`:** assigns each point to its nearest centroid using squared distance, with ties resolved by the lowest centroid index.
- **Empty-cluster handling — `handleEmptyClusters`:** repopulates empty clusters by moving eligible farthest points and updating labels and centroids.
- **Cluster evaluation — `ClusterEvaluator`:** computes inertia from points, labels, and centroids with input validation.
- **Centroid update — `CentroidUpdater`:** computes per-cluster arithmetic means and retains the previous centroid for an empty cluster.
- **Convergence detection — `ConvergenceDetector`:** checks centroid movement, assignment stability, and the maximum iteration limit.

## Integration and current state

These are separate public components, not one estimator class. The caller coordinates their use. The current example combines preprocessing, scaling, initialization, assignment, empty-cluster repair, centroid update, convergence detection, final assignment, and inertia evaluation. The Week 1 reports describe the modules assigned in that reporting period; the week-level reports for subsequent work document additional components and integration.

## Challenges / Notes

- The implementation uses a consistent vector-of-vectors numeric representation for datasets, rather than a fixed 2D point structure.
- Invalid or non-finite values are validated at module boundaries; CSV parsing maps invalid numeric cells to NaN so preprocessing can handle them.
- The example reports inertia in scaled feature space and inverse-transforms centroids for display.

## Week 1 contribution reports included

- `contributions/Week-01 report dataLoader.md`
- `contributions/data_preprocessor.md.md`
- `contributions/feature_scaler.md`
- `contributions/report_centroid_initialization(week-01).md`
- `contributions/Week 1 distance calculation.md`
- `contributions/Week-01_Cluster_Assignment_Report.md`
- `contributions/Week-01_Empty_Cluster_Report.md`
- `contributions/cluster_evaluation.md`
- `contributions/Centroid_Update(week-01).md`
- `contributions/week-01(convergenceDetection).md`

## Header/source report coverage

Each row below has a corresponding Week 1 module report in `contributions/`.

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
| Empty-cluster handler | `include/k_means/EmptyCluster.hpp` | `src/EmptyCluster.cpp` |
| `ClusterEvaluator` | `include/k_means/Cluster_Evaluator.hpp` | `src/Cluster_evaluation.cpp` |
