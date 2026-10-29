# Week 3 Report: Empty-Cluster Handling

This report describes encapsulation, inheritance, and polymorphism for the empty-cluster component. The component is a free function rather than a class.

## 1. Component Layout

| Part | Name | Access |
|---|---|---|
| Function | `handleEmptyClusters()` | namespace scope |
| Input data | dataset (const reference) | read-only |
| Updated data | centroids and assignments (references) | modified in place |
| Persistent member data | none | — |

## 2. Encapsulation

The function groups the repair operation behind a declared interface in `EmptyCluster.hpp`; its temporary counts and point-selection state remain local to the implementation. It finds empty clusters, moves eligible farthest points from donor clusters with more than one point, and updates both labels and centroids. It validates inputs and throws if repopulation is impossible.

## 3. Inheritance

Inheritance does not apply to this free-function component. It has no class hierarchy or base class.

## 4. Polymorphism

The component does not use virtual dispatch, overloads, or runtime polymorphism. The caller invokes the single `handleEmptyClusters` function directly.

## 5. Summary

| Concept | Used? | Where |
|---|---|---|
| Encapsulation | Function boundary and local implementation state | `handleEmptyClusters()` |
| Inheritance | No | It is not a class |
| Polymorphism | No | Single free function |
