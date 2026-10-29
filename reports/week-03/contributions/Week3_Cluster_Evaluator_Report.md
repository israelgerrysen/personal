# Week 3 Report: Cluster Evaluation

This report describes encapsulation, inheritance, and polymorphism in the `ClusterEvaluator` module.

## 1. Class Layout

| Part | Name | Access |
|---|---|---|
| Member data | none | — |
| Type names | `Point`, `Dataset` | public |
| Member function | `computeInertia()` (static) | public |
| Constructor | deleted | public |
| Private/protected members | none | — |

## 2. Encapsulation

`ClusterEvaluator` exposes inertia calculation through `computeInertia(points, labels, centroids)`. It stores no state; the class groups the evaluation operation and its input contract in one public API. The function validates nonempty inputs, matching point dimensions, finite coordinates, one label per point, and labels within the centroid range. It returns the sum of squared distances from each point to its labeled centroid and reports malformed or overflowing results with exceptions.

## 3. Inheritance

The class has no base class and is not used as a base class. Inheritance is not implemented in this module.

## 4. Polymorphism

The class has no virtual functions or overrides. `computeInertia` is static and the constructor is deleted, so the function is used without runtime dispatch or an object instance.

## 5. Summary

| Concept | Used? | Where |
|---|---|---|
| Encapsulation | Yes, as a stateless API boundary | `computeInertia()` and validation |
| Inheritance | No | No base or derived classes |
| Polymorphism | No | No virtual dispatch or overloads |
