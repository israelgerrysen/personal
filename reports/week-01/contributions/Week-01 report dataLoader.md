# Week 1 Report: Data Loading

## Aim

Implement a reusable CSV loader that supplies numeric rows to the K-Means library.

## Completed

- Implemented `DataLoader::loadCSV` in `include/k_means/DataLoader.hpp` and `src/DataLoader.cpp`; it returns a `std::vector<std::vector<double>>`.
- The loader treats the first CSV row as a header, parses quoted fields (including escaped quotes), and can select and reorder columns by zero-based index. An empty selection loads every column.
- Numeric cells must parse completely and be finite. Invalid or non-finite cells are represented as NaN for later preprocessing; they are not silently omitted, so matrix rows retain consistent feature positions.
- File-open failures throw `std::runtime_error`; an empty file, malformed quoting, or row/header field-count mismatch is reported with an exception. Out-of-range selected columns are rejected.
- Added the loader to the CMake library, CSV example, public API, and dedicated test target.

## In Progress

- Connecting the loader output with preprocessing and scaling in the example workflow.

## Challenges / Blockers

- CSV data can contain quoted delimiters and invalid numeric values. The current parser handles quoted fields and preserves invalid numeric cells as NaN so preprocessing can address them explicitly.

## Next Week

- Exercise selected columns with the bundled CSV and continue integrating the library modules.
