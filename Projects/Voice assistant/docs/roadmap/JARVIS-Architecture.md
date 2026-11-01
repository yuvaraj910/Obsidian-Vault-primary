# JARVIS Architecture

> Status: proposed architecture. The existing Voice assistant project folder had no source files or project notes when inspected for this roadmap; this document does not describe a deployed system.

Related: [[Projects/Voice assistant/docs/roadmap/JARVIS-Master-Roadmap.excalidraw|Master roadmap]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Learning-Curriculum|Learning curriculum]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Milestone-Tracker|Milestone tracker]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Research-Backlog|Research backlog]]

## Architecture goals

- Keep speech recognition independent from the AI engine and UI.
- Keep the AI engine independent from the user interface.
- Keep phone, camera, operating-system, and smart-home integrations behind replaceable adapters.
- Start as one local application with clear module boundaries. Split into services only when a measured need justifies it.
- Work offline for declared core functions. Cloud model use is an explicit optional provider, never a silent fallback.
- Treat speech, images, model output, tool output, and network clients as untrusted input.
- Do not run arbitrary shell commands. Tools are allowlisted, typed, permission-checked, and audited.

## Proposed component view

Desktop/phone input → interaction controller → ASR adapter → transcript/event → deterministic router or LLM planner → schema validator → policy/approval gate → tool registry → result → response builder → TTS/UI.

The event log and SQLite store are separate from the live audio path. The camera adapter is idle unless explicitly activated. The phone talks to a local API and does not host the primary model.

## Modules and responsibilities

| Module | Responsibility | Initial boundary |
|---|---|---|
| Audio input | Capture bounded audio frames; expose device, sample rate, channel count, start/stop, and health. | SoundDevice adapter; no ASR or command decisions. |
| VAD/segmenter | Detect speech and produce bounded utterance segments. | Optional until push-to-talk works; no model policy. |
| ASR adapter | Convert audio to text and return language, timestamps/confidence when available, and typed errors. | Vosk or faster-whisper candidate; selected by benchmark. |
| Interaction controller | Manage idle/listening/processing/approval/speaking/error states, cancellation, request IDs, and timeouts. | Owns one request lifecycle; does not execute tools itself. |
| Assistant core | Interpret text; use deterministic router first; optionally request an LLM plan/tool call. | Provider-independent interface. |
| LLM adapter | Send bounded context and tool descriptions to local Ollama or an explicitly enabled cloud provider. | Returns untrusted text or structured tool proposal. |
| Tool registry | Store named handlers, schemas, required permission, and side-effect category. | No generic shell, unrestricted filesystem, or arbitrary Python execution. |
| Policy and approval | Decide whether a proposed action is permitted; request user approval for state changes. | Runs after model output and before every side effect. |
| Tool adapters | Implement narrowly scoped time, app-launch, file, calendar, media, or smart-home operations. | OS- and service-specific; disabled until explicitly configured. |
| Response/TTS | Convert validated result into a concise explanation and speech. | pyttsx3 first; Piper is a later offline candidate. |
| UI | Display transcript, active sensors, status, approvals, errors, and stop/cancel controls. | Tkinter desktop first; mobile/web clients later. |
| API | Expose health, command, status, and event contracts to authenticated clients. | FastAPI on localhost first; LAN access only after auth/TLS design. |
| Vision adapter | Capture a requested image or process a camera stream when visibly enabled; return landmarks/classifications with timestamp. | OpenCV/MediaPipe candidate; no default recording. |
| Persistence | Store settings, approved preferences, conversation summaries, audit events, and retrieval metadata. | SQLite initially; explicit retention and deletion. |
| Observability | Record state transitions, latency, error category, model ID, and request ID without secret or raw-sensor leakage. | Rotating local logs; no raw audio/image by default. |

## Request data flow

1. The user starts push-to-talk or an explicitly enabled wake-word session. The UI indicates microphone state.
2. Audio input returns a bounded buffer with device metadata and request ID. VAD/segmentation may split it into utterances.
3. The ASR adapter returns a transcript or typed failure. The transcript is shown before any sensitive action.
4. The deterministic router handles known commands. If enabled, the LLM receives only the minimum transcript and context needed.
5. Any model tool call is treated as a proposal. A schema validates name and arguments; policy checks tool permission, user scope, and risk.
6. Read-only, low-risk tools may run under configured policy. State-changing, external, destructive, or privacy-sensitive actions require an explicit confirmation screen/phrase.
7. The tool returns a typed result or error. The assistant records a redacted audit event and builds a response.
8. TTS and UI present the result. Cancellation, timeout, disconnect, and failure return to a safe idle state.
9. Conversation context expires according to policy. Only separately approved memories are persisted.

For “point at an object and ask what it is,” the camera snapshot is captured only for that request, tagged with a timestamp and camera ID, and attached to the voice event. The system does not infer that a gesture authorizes an unrelated action.

## Interfaces

### Internal contracts

- ASR input: audio bytes/array, sample rate, channels, language hint, cancellation token.
- ASR output: text, optional segment timestamps/confidence, model identifier, duration, and typed error.
- Tool proposal: tool name plus JSON arguments only; no executable code.
- Tool result: typed success/failure, user-visible summary, side-effect description, and audit metadata.
- Sensor event: modality, timestamp, device ID, permission state, payload reference, and retention flag.
- All long-running work has a timeout and cancellation path; queues are bounded.

### Initial local API proposal

| Route | Use | Guard |
|---|---|---|
| GET /health | Liveness/readiness and loaded model status. | Return no secrets, file paths, or personal data. |
| POST /v1/commands | Submit typed text or a user-approved audio upload. | Authenticated client; request ID/idempotency; body-size limit. |
| GET /v1/requests/{id} | Read status/result for a request. | Owner/device authorization. |
| WebSocket /v1/events | Optional live status and transcript updates. | Authenticated session, origin checks, bounded messages. |
| POST /v1/confirmations/{id} | Accept or reject a pending action. | Short-lived request-bound approval; replay protection. |

These are design proposals, not implemented API routes. Keep the service bound to localhost during early desktop development. LAN exposure requires device authentication and a reviewed transport; never port-forward an unauthenticated assistant endpoint.

## State and memory

- **Ephemeral:** raw audio frames, current transcript, tool proposal, and current camera frame. Drop after request completion unless the user explicitly saves them.
- **Session context:** bounded conversation window; visible clear/reset operation; configurable expiration.
- **Durable memory:** explicit user-approved facts or preferences in SQLite, with source, created time, and deletion path.
- **Retrieval:** start with SQLite tables and full-text search. Add embeddings/vector search only after a tested corpus shows that lexical retrieval is inadequate.
- **Audit data:** record tool name, policy decision, confirmation, outcome, request ID, and timestamps; omit secrets and raw sensor content.

## Security boundaries

| Boundary | Threat | Control |
|---|---|---|
| Microphone/camera → application | Accidental or unnoticed capture. | Push-to-talk first; visible indicator, per-sensor permission, immediate stop, no raw media retention by default. |
| Transcript/image → model | Prompt injection, ambiguous intent, malicious content. | Treat as data, limit context, validate output, never let model text bypass policy. |
| Model → tools | Hallucinated or unsafe action. | Tool allowlist; typed schema; per-tool permission; confirmation for consequential actions; no generic shell. |
| Phone → API | Unauthorized command, replay, data theft. | Device enrollment/revocation; authenticated TLS for network use; request IDs; rate and size limits; least privilege. |
| API → host OS | Arbitrary process/file access. | Narrow adapters, fixed executable/argument lists, path allowlists, no shell interpolation, least-privilege process. |
| Storage/logs → user data | Secret or media leakage. | Separate secret store/environment config; redact logs; local retention and deletion; backup encryption decision before sync. |
| External/cloud provider | Unintended data transfer or outage. | Local-first default; explicit provider setting and disclosure; minimized payload; timeouts; no silent fallback. |

Review OWASP API risks and Android runtime/foreground-service permissions when the relevant interfaces are implemented; platform rules change.

## Deployment progression

### Development host

- Begin on the user's primary PC; the exact CPU, RAM, GPU, and OS support matrix is not established in this roadmap.
- Use one Python environment and a local data directory; run without administrator/root privileges.
- Keep models separate from code and record model/license/version.
- Use localhost only until authentication and LAN threat modeling are complete.

### Phone companion

- Infinix Smart 7 is a thin client/sensor endpoint with 4 GB RAM and 64 GB storage.
- Initially submit push-to-talk audio or text; receive status and speech response; do not assume it can run the primary LLM.
- Test current Android microphone/camera permissions and foreground-service restrictions on the actual device/software version.
- Tailscale is a possible private-network option for later remote access, not a substitute for API authentication.

### Optional ecosystem

- Home Assistant/MQTT, containers, Linux service management, and multiple terminals are later adapters.
- Containerize only components that gain from isolation/reproducibility; native audio access may be simpler on the host.
- Define backups and restore before saving durable personal memory or connecting home devices.

## Quality and operational requirements

- Unit test routing, policy, state transitions, schemas, and storage.
- Integration test ASR, TTS, API, and each tool adapter behind fakes where possible.
- Keep a fixed, consented audio test set and report WER/latency against a declared machine.
- Measure startup time, memory, queue depth, false activations, request latency, reconnects, and error rates.
- On exception or lost network, stop or decline safely; do not replay a partially completed side effect.
- Make sensor state, data retention, provider choice, and device access visible and reversible.

## Decisions still open

- Primary desktop OS and hardware budget.
- ASR model and streaming strategy.
- Wake word versus push-to-talk after V0.1/V0.2 measurements.
- Local TTS engine and licensed voice.
- Native Android, browser client, or Termux prototype.
- Local LLM/model size and whether cloud inference is ever enabled.
- Long-term memory schema and backup/encryption policy.
- Which operating-system, calendar, file, media, and home-device tools are in scope.
