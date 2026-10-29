# BUSULWA GERRYSON ISRAEL 25/U/0826 BELE

# Week 2 Report: CentroidInitializer Class

## 1. What class did I create?

I created `CentroidInitializer`.

## 2. Why?

K-Means needs starting centroids before assignment can begin. The class keeps the requested cluster count and its random generator together, and can repeat initialization when given a fixed seed.

## 3. What data does it hold?

The private members are `k_` and `gen_` (`std::mt19937`). Public aliases `Point` and `Dataset` represent a vector of feature values and a vector of points.

## 4. What functions operate on that data?

The constructors accept `k`, optionally with an unsigned seed. `getK()` reads it, `setK(k)` validates and changes it, and `initialize(data)` selects `k` distinct rows by shuffling row indices. Constructors and setter reject `k < 1`; initialization rejects empty, ragged, zero-feature, non-finite data and `k` larger than the row count with `std::invalid_argument`.

## 5. Why are some members private and others public? How is the class used?

The random generator and cluster count are private so they are managed through the class interface. The rest of the program constructs an initializer and calls `initialize(data)`; the returned centroids are passed to assignment. Invalid input raises an exception rather than returning an empty result.
