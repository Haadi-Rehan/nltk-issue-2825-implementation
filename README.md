# NLTK Issue #2825 – Expand `~` in Paths

This repository contains the Phase 4 implementation for ENGG*4450, adding tilde (`~`)
expansion support to the NLTK data loading system in NLTK.

## Feature Summary

- Adds `expand_user_path()` to `nltk/data.py` as a safe wrapper around
  `os.path.expanduser()`.
- Ensures paths beginning with `~` or `~username` are expanded to the user’s home
  directory before NLTK looks for data.
- Applies expansion in:
  - `nltk.data.find(...)`
  - Initialization of the `NLTK_DATA` environment variable search paths.
- Absolute and relative paths without `~` are left unchanged (backwards compatible).

## Repository Layout

- `implementation/data.py` – modified `nltk.data` module containing `expand_user_path()`
  and the integration changes.
- `tests/test_path_expansion.py` – automated test suite (24 tests) for the new behaviour.
- `tests/test_tilde_expansion_demo.py` – demo script illustrating typical usage.
- `docs/Issue_2825_Implementation_Summary.md` – detailed implementation and testing summary.

## Setup and Installation

git clone https://github.com/Haadi-Rehan/nltk-issue-2825-implementation
cd nltk-issue-2825-implementation

# Install required packages (including NLTK itself)
python -m pip install --upgrade pip
python -m pip install nltk pytest pytest-cov pytest-mock regex click### Apply the patched `data.py` to NLTK

The tests import `nltk.data`, so the installed NLTK must use the patched `data.py`:

# Find where NLTK is installed
python -c "import nltk, os; print(os.path.dirname(nltk.__file__))"Copy `implementation/data.py` over the `data.py` in that directory, for example:

# PowerShell / CMD example (adjust the path to match the output above)
copy implementation\data.py "C:\Users\YOUR_USER\AppData\Local\Programs\Python\Python311\Lib\site-packages\nltk\data.py"(or the equivalent `cp` command if using Git Bash).

## Running the Tests

From the **repository root**:

python -m pytest tests/test_path_expansion.py -v
python -m pytest tests/test_path_expansion.py --cov=nltk.data --cov-report=htmlThe coverage report will be written to `htmlcov/index.html`.

## Running the Demo

From the repository root:

python tests/test_tilde_expansion_demo.pyThe script prints several scenarios and should end with:

[SUCCESS] ALL TESTS PASSED!
