# Full Publication Remote Availability Validation

Date: 2026-06-19

Roadmap task: P5.4 upload all annexed payloads to `arbutus-s3`.

## Scope

This validation checks remote availability for the full raw HectaresBC ZIP payload set described by `metadata/archive_inventory/zip_manifest.csv`.

Expected raw ZIP payloads:

- data-layer ZIPs: 418
- virtual-layer ZIPs: 1,765
- total ZIPs: 2,183
- total expected bytes: 17,531,591,717

## Upload Command

The upload used user-local credentials from `~/.config/fresh-hectaresbc/arbutus_env.sh`. Credentials were not printed, copied, or committed.

```bash
export PATH="$HOME/.local/bin:$PATH"
set -a
source "$HOME/.config/fresh-hectaresbc/arbutus_env.sh"
set +a
git annex enableremote arbutus-s3
git annex copy --to arbutus-s3 raw/hectaresbc_2022_export
```

## Validation Commands

```bash
export PATH="$HOME/.local/bin:$PATH"
git annex find --in arbutus-s3 raw/hectaresbc_2022_export > /tmp/fresh-hectaresbc-p5-arbutus-present.txt
git annex find --not --in arbutus-s3 raw/hectaresbc_2022_export > /tmp/fresh-hectaresbc-p5-arbutus-missing.txt
```

The present and missing path lists were compared against `metadata/archive_inventory/zip_manifest.csv`.

## Results

- expected ZIP count: 2,183
- `arbutus-s3` present ZIP count: 2,183
- missing expected ZIP count: 0
- extra remote ZIP count under raw export path: 0
- `git annex find --not --in arbutus-s3` ZIP count: 0
- expected bytes: 17,531,591,717
- present expected bytes: 17,531,591,717

`git annex info` reported matching local and `arbutus-s3` annex sizes after upload:

```text
17.53 GB: arbutus-s3
17.53 GB: local repository
```

## Status

All expected raw HectaresBC ZIP payload content is available from `arbutus-s3` according to git-annex remote-availability metadata.

P5.5 should still perform the separate full ZIP inventory coverage validation required by the Phase 5 closeout contract.
