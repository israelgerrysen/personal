# Week 3 Report: Cluster Assignment

This report describes encapsulation, inheritance, and polymorphism in `ClusterAssignment` as it is implemented in the current library.

## 1. Class Layout

| Part | Name | Access |
|---|---|---|
| Member data | none | — |
| Type names | `Point`, `Dataset` | public |
| Member function | `assignClusters()` (static) | public |
| Constructor | deleted | public |
| Private/protected members | none | — |

## 2. Encapsulation

`ClusterAssignment` groups nearest-centroid label calculation behind one public function. The caller supplies the data and centroids as const references and receives a vector of zero-based labels. The operation does not mutate its inputs. It checks for empty input, inconsistent or zero dimensions, and non-finite coordinates, and throws `std::invalid_argument` when validation fails. Squared distance is used for comparisons, and ties select the lowest centroid index.

## 3. Inheritance

The class has no base class and is not used as a base class. It has no inheritance hierarchy.

## 4. Polymorphism

The class declares no virtual functions, overrides, or overloaded functions. Its single static operation is called directly; the deleted constructor prevents object creation.

## 5. Summary

| Concept | Used? | Where |
|---|---|---|
| Encapsulation | Yes, as a stateless API boundary | `assignClusters()` and its validation |
| Inheritance | No | No base or derived classes |
| Polymorphism | No | No virtual dispatch or overloads |
