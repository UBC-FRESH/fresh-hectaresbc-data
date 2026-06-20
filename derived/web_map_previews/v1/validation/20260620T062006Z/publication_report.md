# Web Map Preview Publication Report

Generated: 2026-06-20T06:20:06Z

## Artifact Set

- Artifact root: `derived/web_map_previews/v1`
- Manifest/index version: `v1`
- Catalog records represented in `index.json`: 2,183
- Preview PNG artifacts generated: 2,163
- Records marked not previewable: 20
- Preview PNG artifacts annexed locally: 2,163
- Preview PNG artifacts available on `arbutus-s3`: 2,163

## Representative Remote Checks

The following checks were run after `git annex copy derived/web_map_previews/v1 --to arbutus-s3`.

### `dl_adminunits_bcts`

```text
whereis derived/web_map_previews/v1/layers/dl_adminunits_bcts/preview.png (2 copies)
   78f7b9e0-fc71-43fa-85a6-c1b66f449e1a -- [arbutus-s3]
   7b77926b-1422-492c-9cbb-4513d6fd8072 -- gep@jupyterhub11:~/projects/fresh-hectaresbc/external/fresh-hectaresbc-data [here]
ok
```

### `vl_virtualspecies_bulltroutsalvelinusconfluentus_1135`

```text
whereis derived/web_map_previews/v1/layers/vl_virtualspecies_bulltroutsalvelinusconfluentus_1135/preview.png (2 copies)
   78f7b9e0-fc71-43fa-85a6-c1b66f449e1a -- [arbutus-s3]
   7b77926b-1422-492c-9cbb-4513d6fd8072 -- gep@jupyterhub11:~/projects/fresh-hectaresbc/external/fresh-hectaresbc-data [here]
ok
```

### `dl_linearfeat_wellsites`

```text
whereis derived/web_map_previews/v1/layers/dl_linearfeat_wellsites/preview.png (2 copies)
   78f7b9e0-fc71-43fa-85a6-c1b66f449e1a -- [arbutus-s3]
   7b77926b-1422-492c-9cbb-4513d6fd8072 -- gep@jupyterhub11:~/projects/fresh-hectaresbc/external/fresh-hectaresbc-data [here]
ok
```

## Commands

```bash
find derived/web_map_previews/v1/layers -name preview.png | wc -l
git annex find --in arbutus-s3 derived/web_map_previews/v1/layers --include='*.png' | wc -l
git annex whereis derived/web_map_previews/v1/layers/dl_adminunits_bcts/preview.png
git annex whereis derived/web_map_previews/v1/layers/vl_virtualspecies_bulltroutsalvelinusconfluentus_1135/preview.png
git annex whereis derived/web_map_previews/v1/layers/dl_linearfeat_wellsites/preview.png
```
