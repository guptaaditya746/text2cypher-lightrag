# Text2Cypher LightRAG source snapshot

A source snapshot of the LightRAG checkout used for Text2Cypher experiments. It includes the LightRAG Python package, API, web UI, examples, deployment files, and a copy of the upstream LightRAG documentation in `LIGHTRAG_README.md`.

## Getting started

Review `LIGHTRAG_README.md` for the full project setup and service configuration. For the Python package, create an isolated environment and install from the repository root:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -e .
```

Fill the blank-value environment templates under `lightrag/api/` and `lightrag_webui/` with local settings before starting services. They intentionally contain no credentials. Deployment secret manifests were omitted; create those locally from your deployment environment.

This is a sanitized snapshot of the current `text2cypher` working tree. Historic Git commits were not copied because an earlier commit contains a token-shaped literal; the original local Git history remains untouched on the cluster.
