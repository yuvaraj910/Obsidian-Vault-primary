# JARVIS Research Backlog

> Status: questions to investigate later. Nothing here is selected for implementation. Promote an item only when a milestone needs the answer and a small experiment can resolve it.

Related: [[Projects/Voice assistant/docs/roadmap/JARVIS-Master-Roadmap.excalidraw|Master roadmap]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Learning-Curriculum|Learning curriculum]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Milestone-Tracker|Milestone tracker]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Architecture|Architecture]]

## Selection rule

For each experiment, write the question, candidate approaches, fixed test input, machine/software versions, measurement, result, and decision. Do not select a framework because it appears in the idea list. Prefer the smallest experiment that answers a real milestone question.

| Priority / stage | Research question and alternatives | Small experiment | Decision gate |
|---|---|---|---|
| High · V0.1 | Which ASR path best fits the actual PC and language: Vosk streaming, faster-whisper with small/local model, or a wrapper such as SpeechRecognition? | Use the same 20–50 consented clips; report WER, exact-command accuracy, median/p95 latency, startup, RAM/VRAM, and whether network is used. | Choose only after results meet the V0.1 use case; retain adapter interface. |
| High · V0.2 | Push-to-talk, VAD-only segmentation, or wake-word activation? Compare openWakeWord and other candidates only after continuous capture works. | Record false activations and missed utterances in quiet, TV/noise, and distance conditions; measure stop latency and CPU. | Add wake word only if convenience outweighs false activation and privacy cost. |
| High · V0.4 | Which local ASR/TTS models fit available host compute and licenses? Compare CPU/GPU, quantization, and model size. | Benchmark first response latency, throughput, resident memory, and transcription/voice quality on the declared PC. | Pick a model that fits a written resource and quality budget; no phone inference requirement. |
| Medium · V0.3/V0.4 | Which TTS path is simplest and sufficiently natural: OS voice/pyttsx3 versus local Piper? | Compare startup, pronunciation, interruption, voice availability, and model/voice license on target OS. | Keep one default; do not ship voice assets without license review. |
| High · V0.5 | Which LLM setup is viable: local Ollama, explicitly enabled cloud provider, or a provider adapter supporting both? | Run a fixed set of intents/tool proposals; measure latency, schema validity, cost if cloud is enabled, and offline behavior. | Keep deterministic commands available regardless of model/provider. Cloud requires explicit opt-in and payload disclosure. |
| High · V0.5 | How reliable are tool calls under ambiguous, adversarial, and malformed prompts? | Red-team a read-only tool set; test schema rejection, unauthorized tool names, duplicate requests, and injection in retrieved text. | Do not allow a tool until policy tests show zero unauthorized side effects. |
| Medium · V0.5 | How much memory is useful, and when is vector search justified? Compare session-only context, SQLite/FTS, and Chroma or another vector store. | Create a small labeled question set over user-approved notes; measure retrieval relevance, source correctness, deletion, disk/RAM cost. | Start with SQLite/FTS; add vector indexing only if it improves measured retrieval. |
| High · V0.6 | Native Android app, mobile web client, or Termux prototype? | Compare PTT UX, permission handling, reconnects, background limits, maintenance load, and phone thermal/battery behavior on the Infinix Smart 7. | Select the least complex client that meets the intended use; phone remains a client initially. |
| Medium · V0.6 | How should phone audio reach the PC: uploaded bounded clip, WebSocket chunks, or WebRTC? | Compare end-to-end latency, packet loss, reconnect behavior, implementation cost, and permission surface on local Wi-Fi. | Choose based on measured streaming need; prefer bounded clip upload if it meets interaction goals. |
| High · V0.6/V1.0 | What authentication and remote-access model is appropriate: local LAN only, private tailnet, or other authenticated proxy? | Threat-model LAN/remote attackers; test device revocation, expired credentials, replay, and service exposure. | Never expose a public endpoint or use network location as identity. |
| Medium · V0.7 | Which vision task is actually needed: hand landmarks, gesture classification, body pose, or full motion capture? | Start with one camera and three gestures; measure precision/recall and false activation across lighting, distance, and occlusion. | Keep claims limited to measured tracking/gesture capability; defer full motion capture unless a real need and sensor plan exist. |
| Medium · V0.8 | Snapshot-based vision versus continuous video, and which vision-language model can answer the intended questions? | Use a consented fixed image set; compare accuracy, uncertainty behavior, latency, memory, and data sent to any cloud provider. | Default to one-shot snapshots; do not store or stream video by default. |
| Optional · V0.7/V1.0 | Are extra depth cameras, IMUs, ESP32 sensors, or Raspberry Pi-class boards needed? | Define a concrete interaction first; prototype one sensor; measure calibration burden, power, reliability, and useful accuracy. | Buy/attach hardware only after software-only testing shows a measurable gap. |
| Medium · V1.0 | Should home automation use Home Assistant's native integration, MQTT, or direct device adapters? | Simulate/read one sensor; test unavailable broker and revoked credentials; then evaluate one reversible action. | Prefer an existing platform integration; do not add a message broker without multiple consumers or a clear need. |
| Medium · V1.0 | How should services be installed: native process, Windows service, Docker Compose, or Linux system service? | Package one stable feature on the intended host; compare audio device access, upgrade/rollback, logs, and recovery. | Choose per deployment target; don't containerize device access just for architectural style. |
| Low · Research later | Can model quantization, batching, or GPU scheduling improve latency enough to justify complexity? | Profile one selected model and identify the measured bottleneck before changing settings. | No optimization without a baseline and a repeatable benchmark. |
| Low · Research later | Could long-term personalization, speaker identification, face recognition, or emotion inference add real value? | First write a privacy and consent analysis and a concrete use case; test with synthetic/consented data only. | Defer identity/emotion inference unless the user explicitly wants it and the benefit outweighs privacy risk. |

## Explicitly deferred

- Training a foundation language model or building a custom ASR model.
- Always-on cloud recording or silent cloud fallback.
- Running the primary LLM on the 4 GB phone.
- Full-body motion capture claims from a single uncalibrated RGB camera.
- Autonomous shell access, unrestricted filesystem access, or unattended destructive actions.
- Public internet exposure of the assistant API.
- Distributed microservices, vector databases, message brokers, and Kubernetes before a measured need.
- Storing all conversations/audio/images permanently.
