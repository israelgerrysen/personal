# Week 2 Report: DataLoader Class

## 1. What class did I create?

I created the `DataLoader` utility class.

## 2. Why?

It reads a CSV file into the numeric matrix used by preprocessing and clustering, while keeping file parsing out of the algorithm modules.

## 3. What data does it hold?

The class has no persistent member data. Temporary strings, rows, and parsed cells are local to the implementation in `src/DataLoader.cpp`.

## 4. What functions operate on that data?

`loadCSV(filename, selectedColumns = {})` is a public static function. It skips the header, handles quoted fields and escaped quotes, and returns numeric cells as a `std::vector<std::vector<double>>`. An empty column selection means all columns; supplied zero-based indices select and order the fields. Invalid or non-finite numbers become NaN, preserving row shape for preprocessing. The loader throws on file-open failure, empty input, invalid CSV quoting, row/header width mismatch, and out-of-range selection.

## 5. Why are some members private and others public? How is the class used?

There is no object state to expose, so callers use the static function directly, for example `DataLoader::loadCSV(path, {12, 13})`. The local parser details are not part of the public API. The returned matrix can then be passed to preprocessing and scaling.
