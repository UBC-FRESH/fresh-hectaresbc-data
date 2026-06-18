# Annex Tracking Policy

This dataset uses DataLad/git-annex for large HectaresBC payloads.

Initial policy:

- ZIP archives under `raw/hectaresbc_2022_export/data_layers/` and `raw/hectaresbc_2022_export/virtual_layers/` are annexed.
- Common documentation, manifest, schema, and compact metadata formats are tracked directly in Git.
- Other non-text files larger than 1 MiB are annexed by default.

Object-storage remotes are not configured yet; that is handled by the next roadmap task.
