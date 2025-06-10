# Kinect-to-WebXR Volumetric Streaming

**Real-time holographic presence over the web** — This project turns any space equipped with an Azure Kinect (or multiple Kinect v2 sensors) into a live, stream-ready volumetric capture rig and delivers the resulting 3-D mesh + texture frames straight to a browser-based WebXR client. The goal is friction-less, two-way communication where remote participants appear as life-size holograms inside VR today and, eventually, mixed-reality headsets tomorrow.

---

## Why it matters
Traditional video chat flattens people into rectangles. By streaming depth-aware geometry and RGB data, we preserve body language, spatial cues, and a true sense of “being there,” unlocking richer collaboration, education, and performance experiences.

---

## Key Features
| Feature | Details |
|---------|---------|
| **Low-latency pipeline** | Custom C++/CUDA capture daemon decimates + compresses point-clouds to a lean GLB frame stream (< 40 ms glass-to-glass on LAN). |
| **Adaptive mesh resolution** | Dynamic level-of-detail keeps bandwidth predictable from broadband to 5 G. |
| **WebXR front-end** | A-Frame + Three.js viewer renders incoming GLB frames at up to 90 FPS in Quest/PCVR. |
| **Multi-sensor fusion** | Optional multi-Kinect calibration for 360° capture; handles occlusion and merges color maps. |
| **Modular transport** | Default WebRTC data-channels; swap in QUIC or gRPC if you need custom paths. |
| **Session recording** | Fire-and-forget recorder outputs time-stamped GLB sequences and synchronized .wav audio. |

---

## Tech Stack

- **Capture** – Azure Kinect SDK, OpenCV, C++17, CUDA  
- **Encoding** – glTF (GLB) + Draco mesh compression  
- **Transport** – WebRTC / UDP  
- **Frontend** – A-Frame ^1.5, Three.js r165, TypeScript, WebGL 2  
- **DevOps** – Docker Compose, GitHub Actions, Vite hot-reload for rapid scene tweaks

---

## Quick Start

```bash
# 1. Clone mono-repo
git clone https://github.com/your-handle/kinect-volumetric-xr.git
cd kinect-volumetric-xr

# 2. Build & run the capture service (needs an attached Kinect)
docker compose up capture

# 3. Serve the WebXR client
cd client
npm i && npm run dev
