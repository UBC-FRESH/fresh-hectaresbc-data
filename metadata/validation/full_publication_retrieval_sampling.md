# Full Publication Retrieval Sampling

Date: 2026-06-19

Roadmap task: P5.6 validate cold-clone retrieval sampling.

## Scope

This validation checks that a fresh clone of the main repository can initialize the data submodule, enable the `arbutus-s3` special remote, retrieve the Phase 4 representative payload set, and retrieve additional samples selected after full publication.

The test used the Phase 5 branch because Phase 5 has not yet merged to `main`.

## Cold-Clone Setup

```bash
export PATH="$HOME/.local/bin:$PATH"
git clone --branch feature/p5-full-data-publication \
  https://github.com/UBC-FRESH/fresh-hectaresbc.git \
  /tmp/fresh-hectaresbc-p56-coldclone
cd /tmp/fresh-hectaresbc-p56-coldclone
git submodule update --init --recursive external/fresh-hectaresbc-data
cd external/fresh-hectaresbc-data
git annex init
set -a
source "$HOME/.config/fresh-hectaresbc/arbutus_env.sh"
set +a
git annex enableremote arbutus-s3
```

The credential file was used as local private state. Credential values were not printed, copied, or committed.

`git annex init` emitted the expected warning that the normal GitHub `origin` remote is not usable by git-annex. This is not a retrieval failure because payload content is provided by `arbutus-s3`.

## Retrieval Command

```bash
datalad get \
  raw/hectaresbc_2022_export/data_layers/adminunits_bcts.zip \
  raw/hectaresbc_2022_export/data_layers/climatedecade_ahm.zip \
  raw/hectaresbc_2022_export/data_layers/climatercp452050_tmaxsp.zip \
  raw/hectaresbc_2022_export/data_layers/water_distancetocoast.zip \
  raw/hectaresbc_2022_export/virtual_layers/virtualecocomm.alaskanmountainheatherdwarfshrublandharrimanellastellerianadwarfshrubland.425.zip \
  raw/hectaresbc_2022_export/virtual_layers/virtualspecies.bulltroutsalvelinusconfluentus.1135.zip \
  raw/hectaresbc_2022_export/data_layers/topography_rhsp.zip \
  raw/hectaresbc_2022_export/data_layers/mgtdes_landreserves.zip \
  raw/hectaresbc_2022_export/virtual_layers/virtualspecies.yellowwarblerdendroicapetechia.1119.zip \
  raw/hectaresbc_2022_export/virtual_layers/virtualecocomm.sitkasedgepeatmossescarexsitchensissphagnumspp.464.zip
```

Result:

```text
get (ok: 10)
```

All 10 files were reported as retrieved from `arbutus-s3`.

## Sample Set

| Sample class | Path | Bytes | SHA-256 |
| --- | --- | ---: | --- |
| Phase 4 representative, category metadata | `raw/hectaresbc_2022_export/data_layers/adminunits_bcts.zip` | 1,092,878 | `ef4cab4539b67d7153a44669e4b04f630c561029febc732c37f80c37d8a445ce` |
| Phase 4 representative, climate data layer | `raw/hectaresbc_2022_export/data_layers/climatedecade_ahm.zip` | 53,393,852 | `445e88094e1e1fc299bc04990494035925d89980cc689a6c29e9647a09fa0024` |
| Phase 4 representative, nested ZIP edge case | `raw/hectaresbc_2022_export/data_layers/climatercp452050_tmaxsp.zip` | 93,872,336 | `55c2bde2eb023e7eca830834bc903ca0956242e96f51cb58d1b0b2a6411bedf8` |
| Phase 4 representative, large data layer | `raw/hectaresbc_2022_export/data_layers/water_distancetocoast.zip` | 664,393,838 | `4ac62cddca628fc9d15d75f2cdfaa4bd92ffde7cda1ff5048b7beb74b9ca9119` |
| Phase 4 representative, ecological community virtual layer | `raw/hectaresbc_2022_export/virtual_layers/virtualecocomm.alaskanmountainheatherdwarfshrublandharrimanellastellerianadwarfshrubland.425.zip` | 1,716,839 | `e0a3a373c53ffcd0348af6a39729235c629897f7edca540c759f925dd7a0ff2c` |
| Phase 4 representative, large virtual species layer | `raw/hectaresbc_2022_export/virtual_layers/virtualspecies.bulltroutsalvelinusconfluentus.1135.zip` | 11,240,874 | `609f2fbf4a7a572fd93c2783e90ab5684e63c0161816887749ad06211c653c4b` |
| Additional sample, large topography data layer | `raw/hectaresbc_2022_export/data_layers/topography_rhsp.zip` | 178,187,351 | `f6e5937cf9e0c012bf3a940518c96267b48fde8693038a0a8b7b374bef3e555a` |
| Additional sample, small category metadata data layer | `raw/hectaresbc_2022_export/data_layers/mgtdes_landreserves.zip` | 1,289,162 | `1223cbd85b524e46099166cbdaebbbd4b8f9d6695dfd093190ba5b1d8e3014e2` |
| Additional sample, virtual species layer | `raw/hectaresbc_2022_export/virtual_layers/virtualspecies.yellowwarblerdendroicapetechia.1119.zip` | 2,913,843 | `a15138f49824e12030300096f60b21572aa6b73504c47f30691c3b78a26720ff` |
| Additional sample, virtual ecological community layer | `raw/hectaresbc_2022_export/virtual_layers/virtualecocomm.sitkasedgepeatmossescarexsitchensissphagnumspp.464.zip` | 1,619,223 | `2d08a2d8439d3f6e693d106baba71544048cf6324142269f8e0d1fc53a808531` |

Total retrieved sample bytes: 1,009,720,196.

## Integrity Checks

The validation ran:

```bash
git annex whereis <sample paths>
git annex fsck <sample paths>
sha256sum <sample paths>
git annex lookupkey <sample paths>
```

Results:

- `git annex whereis` listed local content and `arbutus-s3` for sampled payloads.
- `git annex fsck` reported checksum `ok` for all 10 sampled payloads.
- `sha256sum` matched the SHA-256 digest embedded in each git-annex key for all 10 sampled payloads.
- checksum/key mismatches: 0

## Status

Cold-clone retrieval sampling passed for the Phase 4 representative set plus four additional full-publication samples.

P5.7 should update final Phase 5 documentation and submodule references before the phase PR is marked ready for review.
