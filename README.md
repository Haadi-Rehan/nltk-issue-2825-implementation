# NLTK Issue #2825 – Expand `~` in Paths

This repository contains the Phase 4 implementation for ENGG*4450, adding tilde (`~`)
expansion support to the NLTK data loading system.

## Feature Summary

- Adds `expand_user_path()` to `nltk/data.py` as a safe wrapper around
  `os.path.expanduser()`.
- Ensures paths containing `~` or `~username` are expanded before NLTK looks for data.
- Applies expansion in:
  - `nltk.data.find(...)`
  - Initialization of the `NLTK_DATA` environment variable search paths.
- Keeps absolute and relative paths without `~` unchanged and fully backward compatible.

## Repository Layout

- `nltk-project/nltk/data.py` – modified source file with `expand_user_path()` and integrations.
- `nltk-project/nltk/test/test_path_expansion.py` – automated tests (24 tests) for the feature.
- `nltk-project/test_tilde_expansion_demo.py` – demo script illustrating typical usage.
- `docs/Issue_2825_Implementation_Summary.md` – detailed implementation and testing summary.

## Setup and Installation

git clone https://github.com/Haadi-Rehan/nltk-issue-2825-implementation
cd nltk-issue-2825-implementation

pip install pytest pytest-cov pytest-mock regex click## Running the Tests

From the project root:

cd nltk-project
python -m pytest nltk/test/test_path_expansion.py -v
python -m pytest nltk/test/test_path_expansion.py --cov=nltk.data --cov-report=htmlThe coverage report will be written to `htmlcov/index.html`.

## Running the Demo

cd nltk-project
python test_tilde_expansion_demo.pyThe script prints several scenarios and should end with:

`[SUCCESS] ALL TESTS PASSED!`
