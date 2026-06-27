# GLM-5.2 Runtime Images

Small RunPod images for serving `unsloth/GLM-5.2-GGUF` UD-IQ1_S.

The images do not include the model. They download model files from Hugging Face on first container start and reuse `/workspace` on later starts.

Use a persistent RunPod volume mounted at `/workspace`.

## Ollama Image

```text
ghcr.io/immogpu/glm52-ollama-hf:latest
```

Downloads the ready Ollama store from `mstoken/glm52-ollama-store` and serves Ollama on port `11434`.

## llama-server Image

```text
ghcr.io/immogpu/glm52-llama-hf:latest
```

Downloads the split GGUF shards from `unsloth/GLM-5.2-GGUF` and starts `llama-server` directly against shard `00001`. This skips GGUF merge and Ollama import.

Default reasoning settings:

```text
GLM52_ENABLE_THINKING=true
GLM52_REASONING_EFFORT=high
```

The server listens on port `11434` and exposes the llama.cpp server API, including OpenAI-compatible routes.

## RunPod Defaults

- Container disk: `300-350 GB`
- Volume mount path: `/workspace`
- Port: `11434/http`
- Optional secret env: `HF_TOKEN`

The llama-server image needs enough disk for the split shards only. The Ollama image needs enough disk for the ready Ollama store.
