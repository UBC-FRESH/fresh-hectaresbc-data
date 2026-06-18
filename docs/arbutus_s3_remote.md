# Arbutus S3 Remote

This DataLad/git-annex dataset is configured with an S3 special remote named:

```text
arbutus-s3
```

The remote points to the DRAC Arbutus object-storage bucket:

```text
fresh-hectaresbc-data
```

Endpoint host:

```text
object-arbutus.cloud.computecanada.ca
```

Region:

```text
ca-west-1
```

## Credential Contract

Credentials are user-local and are not stored in this repository.

Expected local file:

```text
~/.config/fresh-hectaresbc/arbutus_env.sh
```

Expected exported variables:

```bash
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
export AWS_DEFAULT_REGION="ca-west-1"
export S3_ENDPOINT_URL="https://object-arbutus.cloud.computecanada.ca"
```

The file should be readable only by the local user:

```bash
chmod 600 ~/.config/fresh-hectaresbc/arbutus_env.sh
```

## Retrieval Smoke Test

From a fresh clone:

```bash
export PATH="$HOME/.local/bin:$PATH"
source ~/.config/fresh-hectaresbc/arbutus_env.sh
git annex enableremote arbutus-s3
datalad get metadata/validation/arbutus_s3_smoke_test.bin
```

Expected SHA-256:

```text
b9e0965b49a18d3e53d4476b7712662438be93f02ff253d8067da8cb777427cc
```

## Safety Rules

- Do not commit credentials.
- Do not initialize the remote with `embedcreds=yes`.
- Do not paste credential values into issues, pull requests, logs, or documentation.
- Store large HectaresBC payloads in git-annex and publish annexed content to `arbutus-s3`.
