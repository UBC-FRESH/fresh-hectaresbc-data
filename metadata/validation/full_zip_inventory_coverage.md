# Full ZIP Inventory Coverage Validation

Date: 2026-06-19

Roadmap task: P5.5 validate full ZIP inventory coverage against the recovered archive manifest.

## Scope

This validation compares Git-tracked raw ZIP paths in the DataLad data repository against `metadata/archive_inventory/zip_manifest.csv`.

Expected manifest scope:

- manifest rows: 2,183
- total expected raw ZIPs: 2,183
- expected data-layer ZIPs: 418
- expected virtual-layer ZIPs: 1,765
- expected ZIP bytes: 17,531,591,717

## Validation Logic

The check compared:

- expected paths from `metadata/archive_inventory/zip_manifest.csv`, mapped under `raw/hectaresbc_2022_export/`;
- tracked ZIP paths from `git ls-files -s raw/hectaresbc_2022_export`;
- Git file modes for ZIP payloads;
- root control file presence and Git tracking mode;
- blocked/disposable/private path patterns.

Blocked path patterns checked:

- `.ipynb`
- `.ipynb_checkpoints`
- `tmp/`
- `bootstrap`
- `aws-secrets`
- `arbutus_env`
- `secret`
- `credentials`

## Results

- tracked raw ZIP count: 2,183
- tracked data-layer ZIP count: 418
- tracked virtual-layer ZIP count: 1,765
- missing manifest ZIP count: 0
- extra raw ZIP count: 0
- non-annex ZIP count: 0
- missing root control file count: 0
- root control files with unexpected Git mode: 0
- blocked path pattern hits: 0

Root control files present as Git-tracked files:

- `raw/hectaresbc_2022_export/data_layers.txt`
- `raw/hectaresbc_2022_export/virtual_layers.txt`
- `raw/hectaresbc_2022_export/virtual_layers_metadata_all.csv`

## Status

The data repository raw ZIP payload set exactly matches the recovered archive ZIP manifest. No intentional exceptions are recorded for this validation.

P5.6 should validate retrieval from a cold clone beyond the Phase 4 representative payload set.
