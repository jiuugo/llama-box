# Agent Guidelines for llama-box

Personal Docker Compose setup for running local LLMs with llama.cpp on AMD ROCm (RX 9070 XT, Fedora Linux).

## Golden Rules
1. **Never store model weights in the repo**: GGUFs live on the host in `${MODELS_PATH}`, mounted to `/models` in the container.
2. **Path conventions**:
   - In `models.ini`, all model paths MUST begin with `/models/`.
   - In `compose.yml`, maintain `:ro,Z` flags for Fedora SELinux compatibility.
3. **Hardware pass-through**: Do not remove ROCm devices (`/dev/kfd`, `/dev/dri`) or `ipc: host`.
4. **Environment**: Never commit `.env`. Keep `.env.example` updated if variables change.

## Verification
- Validate compose syntax after any change: `docker compose config`
