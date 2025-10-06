# 🗣️ Real-Time Text-to-Speech Streaming Service (ElevenLabs Clone)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yrshanker/tts-elevenlabs-clone/blob/main/TTS_final_submission.ipynb)
![Python](https://img.shields.io/badge/Python-3.10-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-async-green)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

---

### 🚀 Overview
This project implements a **low-latency, open-weight Text-to-Speech (TTS)** engine inspired by ElevenLabs' real-time streaming API.  
It’s fully contained in a **Google Colab notebook** using **open-source models only** — no cloud-based APIs like Azure or ElevenLabs are used.

The notebook exposes a **bidirectional WebSocket server** to stream JSON text chunks in and **44.1 kHz audio** chunks out with real-time playback and **character-level timestamp alignment**.

---

### ✨ Key Features
- ⚡ **~550 ms p50 latency** from first input to first audio output  
- 🎧 **44.1 kHz / 16-bit mono PCM audio** streamed via Base64 JSON  
- 🔠 **Character-level alignment** (≤ ±120 ms error) for real-time captions  
- 🧮 **Math-aware TTS**: interprets LaTeX and symbolic notation in speech  
- 🧱 **End-to-end Colab deployment** using open-weight TTS models  
- 🧩 **Coqui XTTS, Bark, and SpeechT5** support  

---

### 🧠 Architecture
```text
Client (Colab / WebSocket)
   │
   ├──► JSON stream {"text": "...", "flush": bool}
   │
WebSocket Server (FastAPI + asyncio)
   ├── Text buffer aggregation
   ├── Model inference (open-weight TTS)
   ├── Alignment estimation
   └──► {"audio": <Base64>, "alignment": {...}}
