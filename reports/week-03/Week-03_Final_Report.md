# Week 3 Final Report

## Overview

This report combines the Week 3 module reports and describes encapsulation, inheritance, and polymorphism across the corresponding current library modules.

## 1. Encapsulation

- **`DataLoader`:** exposes a static CSV-loading function. Parsing helpers and temporary buffers stay in the implementation file; optional zero-based column selection is part of the public interface.
- **`DataPreprocessor`:** groups stateless matrix operations as public static methods. It has no internal dataset state.
- **`FeatureScaler`:** keeps its scaling method, fitted offsets and scales, and fitted flag private. Public methods fit, transform, inverse-transform, and report fitted status.
- **`CentroidInitializer`:** keeps its `k_` and random generator private; callers use constructors, accessors, and `initialize()`.
- **`DistanceCalculator`:** exposes static distance operations and stores no data. Its constructor is deleted.
- **`ClusterAssignment`:** exposes stateless nearest-centroid assignment and returns one label per point.
- **`CentroidUpdater`:** exposes a static update operation, stores no data, and returns a new centroid set without mutating its inputs.
- **`ConvergenceDetector`:** keeps tolerance and iteration limit private, validates them through construction/setters, and exposes convergence checks.
- **`ClusterEvaluator`:** exposes stateless inertia calculation over points, labels, and centroids.
- **`handleEmptyClusters`:** is a free function that repairs empty clusters and updates centroid and label vectors in place.

## 2. Inheritance

None of the reported modules participates in an inheritance hierarchy. Each component has a separate responsibility and is used through its own public API. No base or derived classes are declared in these modules.

## 3. Polymorphism

These modules do not use virtual functions, overrides, or runtime dispatch. `CentroidInitializer` overloads its constructors to support random-device seeding or a caller-supplied seed; this is compile-time overload resolution. `FeatureScaler::Method` selects MinMax or Standard scaling through configuration and does not itself implement polymorphism.

## 4. Current workflow and class layout drawings

The modules are composed by the caller: CSV loading is optional, preprocessing and scaling prepare numeric data, initialization chooses starting centroids, and the caller runs assignment/update with empty-cluster repair and convergence checks. The example coordinates these steps and evaluates final assignments with inertia. The library does not expose a single estimator class.

The module-specific reports retain their class layout diagrams where available. The diagrams show standalone classes and their public/private members; they do not imply inheritance relationships.

## Week 3 contribution reports included

- `contributions/ Week-03 report dataLoader.md`
- `contributions/data_preprocessor.md`
- `contributions/feature scaler.md`
- `contributions/Week3_Centroid_Initialization_Report.md`
- `contributions/Week3 distance calculation.md`
- `contributions/Week3_Cluster_Assignment_Report.md`
- `contributions/Week3_Cluster_Evaluator_Report.md`
- `contributions/Week3_Empty_Cluster_Report.md`
- `contributions/Week3_Centroid_Update_Report.md`
- `contributions/week-03(convergenceDetection).md`

## Header/source report coverage

Each row below has a corresponding Week 3 module report in `contributions/`.

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
