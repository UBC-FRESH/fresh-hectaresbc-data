# fresh-hectaresbc-data

DataLad/git-annex dataset for the recovered HectaresBC archive payloads.

This repository stores large HectaresBC source payloads and compact data metadata for use by the `fresh-hectaresbc` code and documentation repository.

The main project repository is <https://github.com/UBC-FRESH/fresh-hectaresbc>.

## Current Status

This dataset has been initialized as a DataLad/git-annex repository. An Arbutus-backed S3 special remote named `arbutus-s3` is configured for annexed payloads.

The full recovered HectaresBC ZIP payload set has been imported under `raw/hectaresbc_2022_export/`, annexed, and published to `arbutus-s3`.

Current published scope:

- raw ZIP payloads: 2,183
- data-layer ZIPs: 418
- virtual-layer ZIPs: 1,765
- published ZIP bytes: 17,531,591,717

Validation reports:

- `metadata/validation/full_annex_import.md`
- `metadata/validation/full_publication_whereis.md`
- `metadata/validation/full_zip_inventory_coverage.md`
- `metadata/validation/full_publication_retrieval_sampling.md`

## Intended Layout

- `raw/hectaresbc_2022_export/`: recovered original HectaresBC archive payloads.
- `metadata/`: compact inventories, recovered catalog records, validation reports, and schema notes.
- `derived/`: future derived products, documented separately before use.
- `docs/`: dataset-specific operational notes.

See `docs/arbutus_s3_remote.md` for the non-secret Arbutus special-remote contract and retrieval smoke test.

## Metadata

Compact public metadata from the main `fresh-hectaresbc` repository is mirrored under `metadata/`. Root HectaresBC control files are stored under `raw/hectaresbc_2022_export/` beside the preserved raw payload layout.

## Data Handling

Large source files belong in git-annex. Small documentation, manifests, schemas, and compact tabular metadata should remain in Git when practical.

## Retrieval

Users with configured Arbutus credentials can retrieve annexed payloads on demand:

```bash
export PATH="$HOME/.local/bin:$PATH"
source ~/.config/fresh-hectaresbc/arbutus_env.sh
git annex enableremote arbutus-s3
datalad get raw/hectaresbc_2022_export/data_layers/adminunits_bcts.zip
```

Credential files are local private state and must not be committed.
