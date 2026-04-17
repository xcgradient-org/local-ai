# local-ai (locai)

A custom, on-demand local LLM orchestration system designed for high-performance inference using `llama.cpp`.

## Overview

The `locai` system (powered by `llmctl` and `llama-gateway`) provides a seamless way to manage multiple large language models on a local machine with multi-GPU support. It features an OpenAI-compatible API gateway that handles model switching automatically based on incoming requests.

## Architecture

### 1. The Gateway (`llama-gateway.py`)
- **Service:** Managed via `systemd` as `llama-gateway.service`.
- **API:** Provides a unified OpenAI-compatible endpoint at `http://100.72.248.102:18080/v1`.
- **Dynamic Loading:** Automatically unloads the current model and loads a new one when a different model is requested.
- **Admin API:** Internal management endpoint on `localhost:18079`.

### 2. The CLI (`locai` / `llmctl`)
The `locai` command is a powerful management tool:
- **`locai status`**: View active model, backend state, and GPU memory stats.
- **`locai models`**: List available models and their configurations (Context, Split mode, GPU layers).
- **`locai top`**: A real-time dashboard monitoring the gateway and GPU health.
- **`locai chat`**: Interactive CLI chat interface.
- **`locai switch <model>`**: Manually trigger a model reload.
- **`locai logs`**: Stream logs from the gateway or specific model backends.

### 3. Backend System
- **Engine:** `llama-server` (llama.cpp).
- **Launchers:** Specialized bash scripts located in `~/.local/bin/llama-serve-*` that configure specific model parameters (tensor splitting, KV cache quantization, etc.).

## Configured Models

The system currently supports the following models:

| Model | Context | Split Mode | Notable Config |
|-------|---------|------------|----------------|
| **DeepSeek-R1-Distill-Llama-70B** | 8192 | Tensor | Multi-GPU (CUDA0, CUDA1) |
| **Qwen3-32B** | 16384 | Tensor | Full GPU offloading |
| **Qwen3-Coder-Next** | 8192 | Layer | Specialized Q4_0 KV Cache |

## Files and Locations
- **Gateway Script:** `~/.local/bin/llama-gateway.py`
- **CLI Tool:** `~/.local/bin/llmctl`
- **State File:** `~/.local/share/llama-services/gateway-state.json`
- **Logs:** `~/.local/share/llama-services/logs/`
- **Models:** `~/models/`
