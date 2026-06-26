# GLM-5.2 Ollama HF Runtime Image

Small RunPod image for serving `unsloth/GLM-5.2-GGUF` UD-IQ1_S with Ollama.

The image does not include the model. On first container start it downloads the GGUF shards from Hugging Face, merges them with `llama-gguf-split`, imports the model into Ollama as `glm-5.2-1bit`, and serves Ollama on port `11434`.

Use a persistent RunPod volume mounted at `/workspace` so later starts reuse `/workspace/.ollama` and skip the download/import path.

## Image

```text
ghcr.io/immogpu/glm52-ollama-hf:latest
```

## RunPod

- Container disk: `800 GB`
- Volume mount path: `/workspace`
- Port: `11434/http`
- Optional secret env: `HF_TOKEN`

First run needs large temporary storage because shards, merged GGUF, and Ollama import data overlap.
