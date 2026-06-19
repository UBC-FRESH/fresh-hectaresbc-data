# Full Annex Import Validation

## Purpose

Record the Phase 5 import of all recovered HectaresBC ZIP payloads into this DataLad/git-annex data repository.

This report supports P5.3 in the main `fresh-hectaresbc` roadmap.

## Import Inputs

Manifest:

```text
metadata/archive_inventory/zip_manifest.csv
```

Local source archive used for import:

```text
/home/gep/projects/fresh-hectaresbc/tmp/shared-data/hectaresbc
```

Data-repo raw destination:

```text
raw/hectaresbc_2022_export/
```

Import was driven by manifest paths, not by an unreviewed broad directory copy.

## Import Result

| Check | Result |
| --- | ---: |
| manifest ZIP rows | 2183 |
| source ZIPs missing before import | 0 |
| ZIPs already present before import | 6 |
| ZIPs copied during P5.3 | 2177 |
| bytes copied during P5.3 | 16705881100 |
| expected compressed bytes for all ZIPs | 17531591717 |

## Annex Validation

After `git annex add`, the data repo index matched the full manifest:

| Check | Result |
| --- | ---: |
| expected raw ZIP paths | 2183 |
| tracked raw ZIP paths | 2183 |
| missing manifest ZIP paths | 0 |
| extra raw ZIP paths | 0 |
| ZIP paths with non-annex Git mode | 0 |
| data-layer ZIPs | 418 |
| virtual-layer ZIPs | 1765 |

All raw ZIP paths are tracked as Git mode `120000`, which is the git-annex symlink mode for these files.

`git annex info` reported:

| Metric | Result |
| --- | ---: |
| local annex keys | 2184 |
| local annex size | 17.53 GB |
| annexed files in working tree | 2184 |
| size of annexed files in working tree | 17.53 GB |

The extra annex key beyond the 2,183 ZIP payloads is the Phase 4 smoke-test payload:

```text
metadata/validation/arbutus_s3_smoke_test.bin
```

## Storage Remote Status

This P5.3 import represents ZIP payloads in the local DataLad/git-annex repository. Full upload to `arbutus-s3` is handled by P5.4.

At the end of P5.3, `arbutus-s3` still contains the Phase 4 representative payload set and smoke-test content, not the full ZIP payload set.

## Validation Commands

Representative commands used:

```bash
python - <<'PY'
import csv
from pathlib import Path
import subprocess

repo = Path('/home/gep/projects/fresh-hectaresbc-data')
rows = list(csv.DictReader((repo / 'metadata/archive_inventory/zip_manifest.csv').open()))
expected = {'raw/hectaresbc_2022_export/' + row['relative_path']: int(row['size_bytes']) for row in rows}
ls = subprocess.check_output(['git', 'ls-files', '-s', 'raw/hectaresbc_2022_export'], cwd=repo, text=True)
zip_modes = {}
for line in ls.splitlines():
    parts = line.split(None, 3)
    if len(parts) == 4 and parts[3].endswith('.zip'):
        zip_modes[parts[3]] = parts[0]
print(len(expected), len(zip_modes), sum(1 for mode in zip_modes.values() if mode != '120000'))
PY

git annex info
```
