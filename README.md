# J.A.R.V.I.S. Voice Agent Framework

## Overview
J.A.R.V.I.S. is an advanced autonomous AI assistant framework. It combines local Large Language Model (LLM) execution, fast Speech-to-Text (STT), Neural Text-to-Speech (TTS), and a dynamic tool matrix to provide a seamless voice-first interactive experience. Built using FastAPI and LangGraph, this system is designed to run efficiently on an NVIDIA GPU environment (like a Tesla T4) and provides a polished web interface.

## System Architecture
* **`main.py`**: The core FastAPI application. It orchestrates the audio processing pipeline utilizing LangGraph to transition states between STT, the LLM Brain, and TTS.
* **`database.py`**: A persistent SQLite memory bank (`jarvis_memory.db`) for managing personal tasks and reminders.
* **`tools.py`**: Extends the agent's capabilities with real-time web search powered by the Tavily API.
* **`index.html`**: A highly polished, cyberpunk-themed web dashboard featuring automatic Voice Activity Detection (VAD), audio waveforms, a VU meter, and telemetry metrics.

## Key Features
* **Local STT**: Utilizes `faster-whisper` on GPU for rapid, privacy-preserving voice transcription.
* **Agentic Reasoning**: Powered by the `mistral` model via local Ollama integration (v0.1.48).
* **Dynamic Tools**: Can search the web for live data (weather, news, scores) or manage personal tasks (add/list/clear) in real-time.
* **Neural TTS**: High-fidelity synthesized voice responses using `edge-tts` (en-GB-RyanNeural).
* **Cybernetic UI**: Built-in VAD engine automatically triggers recording when you speak, locks during playback, and displays real-time latency telemetry.

## Prerequisites
* **Hardware**: NVIDIA GPU (e.g., Tesla T4) for optimal STT and LLM inference.
* **API Keys**:
  * `TAVILY_API_KEY`: Required for real-time web search capabilities (setup via Kaggle Secrets or environment variable).
* **Dependencies**: Python 3.x, `faster-whisper`, `langgraph`, `langchain-ollama`, `tavily-python`, `fastapi`, `uvicorn`, `edge-tts`, and the Ollama binary.

## Installation & Execution
1. **Install Dependencies**: Install the required Python packages (`pip install faster-whisper edge-tts langgraph langchain-ollama tavily-python uvicorn fastapi...`) and the Ollama binary.
2. **Start Ollama**: Run the Ollama daemon and pull the Mistral model:
   ```bash
   ollama serve
   ollama pull mistral
   ```
3. **Launch the Server**: Start the backend using Uvicorn:
   ```bash
   uvicorn main:app --host 0.0.0.0 --port 8000
   ```
4. **Access the Dashboard**: Use LocalTunnel (or a similar proxy) to expose port 8000 and access the web interface from your browser.
