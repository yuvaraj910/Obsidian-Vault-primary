# JARVIS Milestone Tracker

> Status: all releases below are planned. No implementation state is claimed. Record actual evidence and the test environment before changing a milestone to complete.

Related: [[Projects/Voice assistant/docs/roadmap/JARVIS-Master-Roadmap.excalidraw|Master roadmap]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Learning-Curriculum|Learning curriculum]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Architecture|Architecture]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Research-Backlog|Research backlog]]

## Release sequence

| Release | Goal | Status | Hard dependency |
|---|---|---|---|
| V0.1 | Speech recognition | Planned | Python, audio files, microphone I/O |
| V0.2 | Continuous listening | Planned | V0.1, bounded audio pipeline |
| V0.3 | Basic voice assistant | Planned | V0.1; deterministic tools and TTS |
| V0.4 | Offline assistant | Planned | V0.3 plus selected local ASR/TTS |
| V0.5 | AI-powered assistant | Planned | V0.3 plus schemas and policy gate |
| V0.6 | Smartphone companion | Planned | Stable local API and device authentication |
| V0.7 | Gesture and motion control | Planned | Camera pipeline; can progress in parallel with V0.4–V0.6 |
| V0.8 | Multimodal assistant | Planned | Voice core plus image/gesture event contract |
| V1.0 | Integrated JARVIS ecosystem | Planned | Operationally tested core, deployment, security, recovery |

V0.7 is a parallel capability track. Computer vision does not block V0.4 offline voice. V0.8 integrates streams only after each individual adapter is testable.

## V0.1 — Speech recognition

- **Features:** Select a microphone, record a bounded clip, transcribe it, show/save the transcript, and report failures.
- **Prerequisites:** Python functions/modules/exceptions; WAV/PCM basics; Git and a repeatable environment.
- **Learning requirements:** Audio devices, sample rate/channels, ASR model versus wrapper, WER, latency.
- **Implementation tasks:** Build a file transcription path; add push-to-talk capture; keep ASR behind one adapter; save benchmark configuration separately from private audio.
- **Testing requirements:** Test empty clips, unsupported devices, silence, noisy audio, timeout, model load failure, and keyboard interruption.
- **Definition of done:** 20 labeled test clips each produce a transcript or controlled error; report WER and median/p95 latency with model, machine, and audio settings; microphone resources close after success and failure.
- **Known limitations:** Accuracy depends on language, accent, room, microphone, model, and hardware; streaming is not implied by a successful batch transcription.
- **Future improvements:** Compare Vosk/faster-whisper models; add language selection and optional confidence display.

## V0.2 — Continuous listening

- **Features:** Continuous audio capture with VAD/segmentation, visible listening state, cancellation, and bounded buffering.
- **Prerequisites:** V0.1; audio chunks; queues; threading or asyncio basics.
- **Learning requirements:** Producer/consumer flow, backpressure, silence thresholds, interruption, false activation measurement.
- **Implementation tasks:** Add a bounded queue; isolate capture from inference; make start/stop explicit; add VAD; keep wake-word activation optional.
- **Testing requirements:** 30-minute soak; silence/noise/speech transitions; device unplug/replug; cancellation during inference; measure missed speech and false activations.
- **Definition of done:** Queue remains bounded throughout the soak; no dead microphone or stuck UI after injected errors; stop releases resources; false activations and missed segments are recorded.
- **Known limitations:** Always-on audio can create privacy, battery, and background-service constraints; noise conditions vary.
- **Future improvements:** Wake word, barge-in, language-aware segmentation, model streaming.

## V0.3 — Basic voice assistant

- **Features:** Spoken commands routed to a small deterministic allowlist; spoken and visible responses; command history and safe error handling.
- **Prerequisites:** V0.1; text normalization; command schemas; basic UI; TTS.
- **Learning requirements:** Intent routing, state, testable adapters, subprocess/file-operation boundaries.
- **Implementation tasks:** Implement 5–8 low-risk commands; add help/stop/unknown-command paths; add pyttsx3 or OS speech output; add a simple Tkinter surface.
- **Testing requirements:** At least 20 phrasing examples per command; ambiguous/noisy transcript cases; unknown commands; TTS unavailable; user cancellation.
- **Definition of done:** At least 95% correct routing on the declared command test set; every other case safely declines or requests clarification; all actions have unit tests; no arbitrary shell execution.
- **Known limitations:** Fixed command set; recognition can confuse similar phrases; TTS voice and device behavior differ by OS.
- **Future improvements:** Aliases, local Piper voice, accessible UI, OS-specific app launcher adapter.

## V0.4 — Offline assistant

- **Features:** Core ASR, command routing, and speech output work without an internet connection.
- **Prerequisites:** V0.3; local models; model storage and resource profiling.
- **Learning requirements:** CPU/GPU inference, model loading, quantization, disk/RAM/VRAM tradeoffs, local model licenses.
- **Implementation tasks:** Select local ASR/TTS using measured results; cache model assets; make cloud features explicitly optional; show missing-model and low-resource errors.
- **Testing requirements:** Disconnect network; exercise transcription, commands, TTS, shutdown, and restart; inspect logs and outbound connections during the test.
- **Definition of done:** A 30-minute offline test completes with no network dependency for the declared core feature set; every unsupported cloud feature is labeled; resource and latency measurements are documented.
- **Known limitations:** Local quality and speed depend on PC hardware and model; initial model downloads need a connection.
- **Future improvements:** Improve CPU/GPU settings, model download management, local wake-word model.

## V0.5 — AI-powered assistant

- **Features:** Natural-language responses and constrained tool selection with typed inputs, policy checks, user approval, audit records, and cancellation.
- **Prerequisites:** V0.3; JSON schemas; local or remote model adapter; authentication and security design.
- **Learning requirements:** Tokens/context, structured outputs, tool calling, validation, prompt injection, policy enforcement, error recovery.
- **Implementation tasks:** Add an LLM provider interface; expose only a few read-only tools first; validate arguments; require approval for side effects; never expose a generic shell tool.
- **Testing requirements:** At least 50 prompts covering valid, ambiguous, adversarial, malformed, and tool-failure cases; test provider timeouts and disconnects.
- **Definition of done:** No tool runs when schema or policy validation fails; every side effect has an audit record; confirmation is required for high-impact actions; all tests that request unauthorized actions are rejected.
- **Known limitations:** Models can hallucinate, choose the wrong tool, or misunderstand context; tool calling is a proposal, not an authorization.
- **Future improvements:** Multi-step plans with per-step approval, better evaluations, local/cloud provider comparison.

## V0.6 — Smartphone companion

- **Features:** Authenticated Android client for push-to-talk, transcript/status display, speech response, and selected user-approved sensor input.
- **Prerequisites:** V0.5 or a stable deterministic API; local networking; device identity and revocation.
- **Learning requirements:** Android lifecycle/permissions, REST/WebSockets, TLS, connection recovery, mobile battery/thermal behavior.
- **Implementation tasks:** Freeze a small API contract; build a client prototype; compare native Android, web, and Termux options; keep inference on PC; use ADB only for development.
- **Testing requirements:** 20 disconnect/reconnect cycles; unauthorized token; revoked device; permission denial; phone sleep/wake; server restart.
- **Definition of done:** Client reconnects without duplicating an action; unauthorized requests fail; microphone/camera use is visible and permission-based; core model is not installed on the phone.
- **Known limitations:** Android background audio/camera behavior is restricted and varies by version/manufacturer; 4 GB RAM and 64 GB storage constrain local model ambitions.
- **Future improvements:** Native UI, optional camera snapshot, secure remote access through a reviewed private network.

## V0.7 — Gesture and motion control

- **Features:** A separate vision adapter that tracks landmarks and recognizes a small, explicitly selected set of gestures.
- **Prerequisites:** Python arrays, camera capture, image processing, temporal classification; no dependency on offline ASR.
- **Learning requirements:** Frame rate, camera geometry, landmarks, gesture windows, confidence thresholds, calibration and evaluation.
- **Implementation tasks:** Build camera preview; add MediaPipe landmarks; classify three gestures; gate each gesture behind a visible camera state and cooldown.
- **Testing requirements:** 30 trials per gesture across lighting/distance changes; test no-gesture, occlusion, and bystander cases; measure false activations per 10-minute session.
- **Definition of done:** Precision and recall are at least 0.90 on the declared controlled test set; unintended activations are below one per 10-minute test; user can disable the camera immediately.
- **Known limitations:** Single RGB camera landmarks are not full motion capture; background, lighting, and body/hand occlusion affect results.
- **Future improvements:** Body pose, calibration, temporal models, additional sensors only if the use case needs them.

## V0.8 — Multimodal assistant

- **Features:** A request can combine voice with one user-authorized image snapshot and/or a recognized gesture.
- **Prerequisites:** V0.3 plus tested voice and vision adapters; timestamps, event IDs, cancellation, and context selection.
- **Learning requirements:** Event synchronization, modality confidence, image handling, stale-context rejection, provenance.
- **Implementation tasks:** Build a “point and ask” demo; capture a snapshot only on request; associate transcript/image/gesture IDs; return an answer with uncertainty and source time.
- **Testing requirements:** 20 scripted requests with clear images, ambiguous images, no image, stale image, and cancel; verify no unintended continuous capture or image persistence.
- **Definition of done:** Test report shows each output’s input modalities and timestamps; ambiguous cases ask for clarification; no frame is saved by default; the user can cancel.
- **Known limitations:** Model visual capabilities and performance vary; camera field of view does not guarantee that a pointed object is identifiable.
- **Future improvements:** Object tracking, additional sensors, model comparisons, user-selected retention.

## V1.0 — Integrated JARVIS ecosystem

- **Features:** Supported desktop deployment, optional phone companion, secure local integrations, documented recovery/backup, and clear offline/cloud boundaries.
- **Prerequisites:** V0.3–V0.6 stable; V0.7/V0.8 only if included in declared scope; threat model and deployment target.
- **Learning requirements:** Packaging, service management, authentication/authorization, observability, backups, reliability and release management.
- **Implementation tasks:** Freeze release scope; package the selected host; document setup/upgrade/rollback; implement modular adapters; add monitored optional MQTT/Home Assistant integrations.
- **Testing requirements:** 60-minute soak; restart/recovery; backup/restore; offline test; API authentication/authorization test; supported-platform smoke tests; secret scan.
- **Definition of done:** Every listed feature has acceptance tests and a support status; no secrets appear in repository or logs; backup restore succeeds; optional integrations fail closed when unavailable; one setup guide works from a clean installation on each claimed platform.
- **Known limitations:** “Works everywhere” is not a release claim; the initial support matrix must name exact OS versions, devices, model versions, and features.
- **Future improvements:** Additional platforms, service orchestration, hardware satellites, improved voice/persona and broader home integrations.

## Release evidence template

For each release, record: date; commit/tag; host OS and hardware; model/library versions; test inputs; acceptance results; remaining defects; data-retention behavior; rollback method; and a link to the relevant project log. Do not mark a milestone complete from a demo alone.
