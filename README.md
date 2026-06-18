# fresh-hectaresbc-data

DataLad/git-annex dataset for the recovered HectaresBC archive payloads.

This repository stores large HectaresBC source payloads and compact data metadata for use by the `fresh-hectaresbc` code and documentation repository.

The main project repository is <https://github.com/UBC-FRESH/fresh-hectaresbc>.

## Current Status

This dataset has been initialized as a DataLad/git-annex repository. Large archive payloads have not yet been imported or published to an object-storage special remote.

## Intended Layout

- `raw/hectaresbc_2022_export/`: recovered original HectaresBC archive payloads.
- `metadata/`: compact inventories, recovered catalog records, validation reports, and schema notes.
- `derived/`: future derived products, documented separately before use.
- `docs/`: dataset-specific operational notes.

## Data Handling

Large source files belong in git-annex. Small documentation, manifests, schemas, and compact tabular metadata should remain in Git when practical.
