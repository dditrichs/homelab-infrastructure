# Service Documentation: Open WebUI & Ollama (LXC 104)

## Container Overview
* **CT ID:** `104`
* `* **Hostname:** openwebui-ollama`[cite: 2]
* **IP Address:** `10.0.0.104`
* **Ports:** `3000` (Open WebUI Dashboard) | `11434` (Ollama API)
* **Storage:** `local-lvm`
* **GPU Passthrough:** NVIDIA GeForce GTX 1650 SUPER (`/dev/nvidia0`)

---

## Active AI Models

| Model Name | Parameters | Primary Purpose | Performance / Execution |
| :--- | :--- | :--- | :--- |
| **`qwen2.5:3b`** | 3.09B | Daily Driver, Summarization, Code & Chat | 100% GPU VRAM (Instant) |
| **`deepseek-r1:1.5b`** | 1.78B | Multi-step Reasoning, Math, Logic | 100% GPU VRAM (Fast) |

---

## Service Management & Troubleshooting

### Check GPU Status Inside LXC Shell
```bash
nvtop
# OR
nvidia-smi
```