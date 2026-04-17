# 🧬 XC Gradient Local-AI (Locai)

A custom, on-demand local LLM orchestration system designed for high-performance inference using `llama.cpp`.

## 🏛️ Overview

The `locai` system provides a seamless way to manage multiple large language models on a local machine with multi-GPU support. It features an OpenAI-compatible API gateway that handles model switching automatically based on incoming requests.

## 🚀 System Architecture

### 1. The Gateway (`llama-gateway.py`)
- **Service:** Managed via `systemd` as `llama-gateway.service`.
- **API:** OpenAI-compatible endpoint at `http://<local-ip>:18080/v1`.
- **Dynamic Loading:** Automatically swaps models based on incoming request metadata.

### 2. The CLI (`locai` / `llmctl`)
The `locai` command is the main interaction point:
- `locai status`: View active model and GPU memory stats.
- `locai models`: List available models and configurations.
- `locai chat`: Interactive CLI chat interface.
- `locai switch <model>`: Manually trigger model reload.

## 📁 System Requirements & Paths

- **GPU:** NVIDIA CUDA-enabled GPUs.
- **Backend Engine:** `llama-server` (from `llama.cpp`).
- **Models Folder:** `~/models/` (where GGUF files are stored).
- **Service Files:** `~/.local/share/llama-services/`
- **CLI Executable:** `~/.local/bin/llmctl`

## ⚖️ License

All rights reserved. © 2026 XC Gradient.
