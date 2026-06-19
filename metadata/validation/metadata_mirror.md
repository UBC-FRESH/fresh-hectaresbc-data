# Metadata Mirror Validation

## Purpose

Record the Phase 5 metadata and root-control-file mirror from the main `fresh-hectaresbc` repository into this DataLad data repository.

## Mirrored Main-Repo Metadata

The following compact metadata groups were mirrored under `metadata/`:

- `metadata/archive_inventory/`
- `metadata/catalog_schema/`
- `metadata/recovered_catalog/`
- `metadata/validation/`

Mirrored main-repo metadata files: 17.

Additional data-repo metadata notes retained or added:

- `metadata/README.md`
- `metadata/validation/representative_payloads.md`
- `metadata/validation/arbutus_s3_smoke_test.bin`

## Mirrored Root Control Files

The following root HectaresBC control files were mirrored under `raw/hectaresbc_2022_export/`:

| Path | Bytes |
| --- | ---: |
| `raw/hectaresbc_2022_export/data_layers.txt` | 29677 |
| `raw/hectaresbc_2022_export/virtual_layers.txt` | 349361 |
| `raw/hectaresbc_2022_export/virtual_layers_metadata_all.csv` | 3699170 |

## Tracking Validation

The mirrored metadata and root control files are Git-tracked text or tabular files. ZIP payloads remain git-annex files under the raw data-layer and virtual-layer directories.

Validation commands:

```bash
git check-attr annex.largefiles -- \
  metadata/archive_inventory/zip_manifest.csv \
  metadata/recovered_catalog/virtual_layer_records.csv \
  raw/hectaresbc_2022_export/data_layers.txt \
  raw/hectaresbc_2022_export/virtual_layers_metadata_all.csv \
  raw/hectaresbc_2022_export/data_layers/adminunits_bcts.zip
```

Expected result:

- mirrored metadata and root control files: `annex.largefiles: nothing`
- raw ZIP payloads: `annex.largefiles: anything`

## Exclusions

The following source-local materials remain excluded:

- `hectaresbc_download_layers.ipynb`
- `.ipynb_checkpoints/`
- local `tmp/` content
- credentials and local logs
- extracted rasters and derived products not covered by a derived-data contract
