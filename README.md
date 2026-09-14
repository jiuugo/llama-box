# llama-box

This is my personal configuration and Docker Compose setup for running local LLMs with [`llama.cpp`](https://github.com/ggml-org/llama.cpp) server.

It is tailored for an **AMD Radeon RX 9070 XT** running on **Linux** (tested on Fedora Linux), using the ROCm-enabled container image and custom model presets.

---

## Features

- **ROCm GPU Acceleration**: Passes `/dev/kfd` and `/dev/dri` to the container for AMD Radeon acceleration.
- **Model Presets**: Pre-configured context sizes, quantization, KV cache settings, and vision/MTP draft specs in [`models.ini`](./models.ini).
- **External Model Storage**: Keeps heavy GGUF files outside the git repository via a configurable `.env` file.
- **SELinux Compatible**: Volume mounts configured with `:ro,Z` for Fedora/RHEL compatibility.

---

## Quick Start

### 1. Configure the models directory

Copy the example environment file and set the path where you store your `.gguf` models on your host machine:

```bash
cp .env.example .env
```

Edit `.env`:

```bash
MODELS_PATH=/path/to/your/models
```

### 2. Start the server

```bash
docker compose up -d
```

### 3. Check logs

```bash
docker compose logs -f
```

The server will be available at `http://127.0.0.1:8080`.

---

## Stopping the Server

```bash
docker compose down
```
