# Repository Guidelines

## Project Structure & Module Organization

This repository configures the ROCm-enabled `llama.cpp` server for Linux and an AMD Radeon RX 9070 XT. It contains configuration rather than application source code.

- `compose.yml`: container image, GPU devices, mounts, networking, and server arguments.
- `models.ini`: shared defaults in `[*]` and named model presets.
- `.env.example`: template for the host's `MODELS_PATH`; `.env` holds local settings and is ignored by Git.
- `README.md`: setup and operating instructions.

GGUF models live outside the repository and are mounted at `/models`. There are no source, test, or asset directories.

## Build, Test, and Development Commands

Run commands from the repository root:

- `cp .env.example .env`: initialize local configuration if `.env` does not already exist; set `MODELS_PATH` to your model directory.
- `docker compose config --quiet`: validate Compose syntax and environment substitution.
- `docker compose up -d`: start the server using the published container image; no local build is defined.
- `docker compose logs -f llama-server`: inspect startup, model loading, and GPU errors.
- `docker compose down`: stop and remove the container.

The server listens locally at `http://127.0.0.1:8080`.

## Coding Style & Naming Conventions

Use two-space indentation in YAML. Preserve the INI file's section dividers, semicolon comments, aligned assignments, and grouping of related settings. Use lowercase, hyphenated preset names, such as `qwen3.8-27b-mtp` or `qwen3.8-27b-long`. Reference container paths under `/models`, and keep context-size comments consistent with configured values. No formatter or linter is configured.

## Configuration Safety

Keep machine-specific paths in `.env` and model weights outside Git. Preserve localhost port binding and read-only model mounts unless an intentional deployment change requires otherwise.
