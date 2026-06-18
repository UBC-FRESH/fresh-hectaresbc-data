# Representative Payloads

These six HectaresBC ZIP payloads are the Phase 4 cold-clone validation set.

They were selected by the main `fresh-hectaresbc` repository during Phase 3 because they cover typical data layers, virtual layers, a nested-ZIP edge case, and larger payloads.

All files are stored with git-annex under `raw/hectaresbc_2022_export/` and should be retrievable from the `arbutus-s3` special remote.

| Purpose | Path | Bytes | SHA-256 |
| --- | --- | ---: | --- |
| typical data layer with category metadata | `raw/hectaresbc_2022_export/data_layers/adminunits_bcts.zip` | 1092878 | `ef4cab4539b67d7153a44669e4b04f630c561029febc732c37f80c37d8a445ce` |
| typical data layer with value metadata | `raw/hectaresbc_2022_export/data_layers/climatedecade_ahm.zip` | 53393852 | `445e88094e1e1fc299bc04990494035925d89980cc689a6c29e9647a09fa0024` |
| data layer with nested ZIP member | `raw/hectaresbc_2022_export/data_layers/climatercp452050_tmaxsp.zip` | 93872336 | `55c2bde2eb023e7eca830834bc903ca0956242e96f51cb58d1b0b2a6411bedf8` |
| large data-layer ZIP | `raw/hectaresbc_2022_export/data_layers/water_distancetocoast.zip` | 664393838 | `4ac62cddca628fc9d15d75f2cdfaa4bd92ffde7cda1ff5048b7beb74b9ca9119` |
| typical virtual layer | `raw/hectaresbc_2022_export/virtual_layers/virtualecocomm.alaskanmountainheatherdwarfshrublandharrimanellastellerianadwarfshrubland.425.zip` | 1716839 | `e0a3a373c53ffcd0348af6a39729235c629897f7edca540c759f925dd7a0ff2c` |
| large virtual layer | `raw/hectaresbc_2022_export/virtual_layers/virtualspecies.bulltroutsalvelinusconfluentus.1135.zip` | 11240874 | `609f2fbf4a7a572fd93c2783e90ab5684e63c0161816887749ad06211c653c4b` |

## Retrieval

```bash
source ~/.config/fresh-hectaresbc/arbutus_env.sh
git annex enableremote arbutus-s3
datalad get \
  raw/hectaresbc_2022_export/data_layers/adminunits_bcts.zip \
  raw/hectaresbc_2022_export/data_layers/climatedecade_ahm.zip \
  raw/hectaresbc_2022_export/data_layers/climatercp452050_tmaxsp.zip \
  raw/hectaresbc_2022_export/data_layers/water_distancetocoast.zip \
  raw/hectaresbc_2022_export/virtual_layers/virtualecocomm.alaskanmountainheatherdwarfshrublandharrimanellastellerianadwarfshrubland.425.zip \
  raw/hectaresbc_2022_export/virtual_layers/virtualspecies.bulltroutsalvelinusconfluentus.1135.zip
```
