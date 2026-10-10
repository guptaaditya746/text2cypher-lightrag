# Excluded and sanitized files

- `lightrag_webui/.env.development`: excluded; its endpoint settings were not copied. A blank-value `.env.development.example` is provided.
- `lightrag/api/.env.aoi.example`: original values (including a non-empty Azure API key field) were removed; a blank-value template is provided.
- `k8s-deploy/lightrag/templates/secret.yaml`: omitted because it is a Kubernetes secret manifest.
- `examples/unofficial-sample/lightrag_llamaindex_litellm_opik_demo.py`: an earlier commit in the source history contained a token-shaped literal. This recovery repository is a clean source snapshot and does not include the source Git history.
- Build outputs, caches, logs, and compiled files are ignored.

The original cluster checkout and its history remain unchanged. Rotate any removed credential if it was real and used outside a local test.
