# JARVIS Learning Curriculum

> Status: proposed learning plan. This is a curriculum and a set of experiments, not evidence that any milestone has been implemented.

Related: [[Projects/Voice assistant/docs/roadmap/JARVIS-Master-Roadmap.excalidraw|Master roadmap]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Milestone-Tracker|Milestone tracker]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Architecture|Architecture]] · [[Projects/Voice assistant/docs/roadmap/JARVIS-Research-Backlog|Research backlog]]

## How to use this curriculum

Follow the sequence below and build one small, testable slice at a time. Keep the first version local and push-to-talk. Add continuous listening, an LLM, camera access, phone access, and home automation only after the preceding slice works and has tests.

Priority labels:

- **Essential** — required before the first dependable voice assistant.
- **High** — required for offline operation, controlled AI tools, or phone integration.
- **Medium** — useful for later interfaces and ecosystem work.
- **Optional** — learn only when an experiment or deployment needs it.

The exact model, device, and latency budget are open decisions. Benchmark on the actual computer before selecting model sizes or promising real-time performance. The spare Infinix Smart 7 (4 GB RAM, 64 GB storage) is planned as a lightweight client and sensor device; do not plan around running the main language model on it.

## Recommended learning order

1. Python, Git, small modules, exceptions, tests, and basic networking.
2. Record and play audio; understand PCM, sample rate, buffering, and latency.
3. Transcribe saved clips, then add microphone input and measure accuracy.
4. Add a small deterministic command registry and speech output.
5. Make listening continuous with bounded queues, VAD, and explicit stop controls.
6. Benchmark local ASR and TTS; verify core behavior with the network disconnected.
7. Add an API and phone client after the desktop interfaces are stable.
8. Add an LLM behind typed tools and a policy/confirmation layer.
9. Add vision and gestures as a parallel track; they do not block the offline voice milestone.
10. Combine voice, snapshots, and gestures, then add optional integrations and deployment.

## Curriculum

### 1. Python, command line, and project setup

| Field | Plan |
|---|---|
| Subject | Python fundamentals and repeatable development setup. |
| Subtopics | Values and types; conditions and loops; strings; lists, tuples, sets, dictionaries; functions; file paths and JSON; exceptions; modules and packages; virtual environments; dependency pinning; classes and composition; type hints; logging; configuration. Learn generators and decorators when a concrete interface needs them. |
| Prerequisites | Basic computer and file-system use. If programming is new, learn variables, branching, loops, and functions before reading the Python tutorial, which assumes general programming familiarity. |
| Purpose | The assistant, its tests, adapters, and first tools can be built and debugged in small understandable modules. |
| Application | Audio adapters, command handlers, state, settings, local storage, packaging, and diagnostics. |
| Practical work | Build a command-line note or timer program that reads validated JSON settings, catches invalid input, logs failures, and has a virtual environment and Git history. Split it into input, domain, and output modules. |
| Completion criteria | Explain each module’s responsibility; add a new command without editing unrelated code; handle missing files and malformed input without a traceback; run the program from a clean environment. |
| Priority | Essential. |
| Recommended docs | [Python Tutorial](https://docs.python.org/3/tutorial/index.html), [venv](https://docs.python.org/3/library/venv.html), [typing](https://docs.python.org/3/library/typing.html), [logging](https://docs.python.org/3/library/logging.html), [Git reference](https://git-scm.com/docs). |

### 2. Software engineering and computer-science foundations

| Field | Plan |
|---|---|
| Subject | Version control, tests, processes, networking, and modular design. |
| Subtopics | Git commits and branches; readable diffs; debugging; unit, integration, and end-to-end tests; dependency management; process versus thread; CPU-bound versus I/O-bound work; memory and queues; client/server; JSON; HTTP methods and status codes; TCP/IP, ports, DNS, localhost, LAN addressing; timeouts and retries. |
| Prerequisites | Python functions, modules, exceptions, and command-line use. |
| Purpose | Continuous audio and device communication fail in ways that are difficult to diagnose without observability, test boundaries, and basic network understanding. |
| Application | Separate recognizer, assistant core, UI, API, storage, and operating-system integrations; reproduce bugs and prevent regressions. |
| Practical work | Create a small local HTTP service with a health endpoint, a typed request, useful logs, tests for valid/invalid requests, and a Git branch containing one focused change. |
| Completion criteria | Explain a request from client to server; distinguish a timeout from a refused connection; test a success path and failure path; inspect and revert a change using Git. |
| Priority | Essential. |
| Recommended docs | [Python asyncio](https://docs.python.org/3/library/asyncio.html), [pytest](https://docs.pytest.org/en/stable/), [GitHub Actions: Python CI](https://docs.github.com/en/actions/tutorials/build-and-test-code/python), [HTTP semantics (RFC 9110)](https://www.rfc-editor.org/rfc/rfc9110). |

### 3. Audio fundamentals and device I/O

| Field | Plan |
|---|---|
| Subject | Digital audio and reliable microphone/speaker handling. |
| Subtopics | Analog-to-digital conversion; sampling rate and Nyquist intuition; bit depth; mono/stereo; PCM and WAV; frames and chunks; clipping and amplitude; buffering; device selection; callback versus blocking I/O; resampling; latency; noise and signal-to-noise ratio; safe device shutdown. |
| Prerequisites | Python functions, arrays, file handling, and basic units (samples per second, bytes, milliseconds). |
| Purpose | ASR quality and responsiveness depend on feeding the recognizer correctly shaped, correctly timed audio. |
| Application | Push-to-talk capture, audio playback, future streaming transcription, speech output, and performance measurement. |
| Practical work | Record and replay short WAV files with SoundDevice and NumPy; treat PyAudio as an alternative backend to compare only if device support requires it; print device/sample metadata; make a waveform or simple level meter; compare 16 kHz mono with the device’s native format. |
| Completion criteria | Record, replay, and close the device cleanly; identify sample rate, channels, duration, and clipping; document capture-to-playback latency on the test machine. |
| Priority | Essential. |
| Recommended docs | [SoundDevice documentation](https://python-sounddevice.readthedocs.io/en/latest/), [NumPy beginner guide](https://numpy.org/doc/stable/user/absolute_beginners.html), [Python wave module](https://docs.python.org/3/library/wave.html). |

### 4. Speech recognition and evaluation

| Field | Plan |
|---|---|
| Subject | Speech-to-text (ASR), transcription modes, and measurable evaluation. |
| Subtopics | Utterances and segmentation; language/accent/noise effects; model versus wrapper; batch and streaming recognition; chunk overlap; partial and final results; confidence; Word Error Rate (WER); exact command accuracy; real-time factor; model-load and per-utterance latency. |
| Prerequisites | Audio capture and WAV handling; basic Python modules and exceptions. |
| Purpose | The voice interface needs a replaceable recognizer and evidence about where it works or fails. |
| Application | V0.1 transcription and V0.2 continuous listening. Keep ASR independent from the command engine and LLM. |
| Practical work | Compare Vosk and faster-whisper on the same consented, labeled clips; record model/configuration, WER, command accuracy, RAM/VRAM where available, and latency. Use SpeechRecognition only as a convenient adapter/comparison; it is a wrapper, and some recognizers require a network service. |
| Completion criteria | Transcribe a saved clip and microphone input; report results on a fixed small test set; distinguish an empty transcript, low confidence, timeout, and recognizer failure. |
| Priority | Essential. |
| Recommended docs | [Vosk](https://alphacephei.com/vosk/), [faster-whisper](https://github.com/SYSTRAN/faster-whisper), [OpenAI Whisper](https://github.com/openai/whisper), [SpeechRecognition](https://github.com/Uberi/speech_recognition), [SpeechRecognition package notes](https://pypi.org/project/SpeechRecognition/). |

### 5. Deterministic commands, text-to-speech, and desktop UI

| Field | Plan |
|---|---|
| Subject | A bounded assistant loop that responds and performs predefined actions. |
| Subtopics | Text normalization; exact and fuzzy matching; intent classification; command schemas; routing; command registration; state and history; response construction; TTS; UI states (idle/listening/thinking/speaking/error); cancellations; safe file and time/date operations with os/pathlib; narrowly scoped subprocess adapters for app launch. |
| Prerequisites | Python modules, error handling, test writing, ASR output. |
| Purpose | A predictable command system proves useful interaction without relying on a language model. |
| Application | V0.3 voice assistant. Start with a short allowlist such as time/date, help, stop, and open a harmless local application. |
| Practical work | Implement 5–8 read-only or reversible commands with typed arguments; add pyttsx3 output; expose transcript, state, and cancellation in a small Tkinter interface. |
| Completion criteria | Each command has tests for valid, ambiguous, and invalid input; unknown phrases produce a safe response; no command executes arbitrary transcript text; the user can stop listening and speech. |
| Priority | Essential. |
| Recommended docs | [Tkinter](https://docs.python.org/3/library/tkinter.html), [pathlib](https://docs.python.org/3/library/pathlib.html), [os](https://docs.python.org/3/library/os.html), [subprocess security guidance](https://docs.python.org/3/library/subprocess.html), [pyttsx3](https://github.com/nateshmbhat/pyttsx3). |

### 6. Continuous listening, concurrency, and offline voice

| Field | Plan |
|---|---|
| Subject | Long-running audio loops and local voice processing. |
| Subtopics | Producer/consumer queues; bounded buffers and backpressure; async I/O versus CPU inference; threads/processes; VAD; wake-word detection; chunk size and overlap; interruptions/barge-in; cancellation; local model loading; quantization; CPU/GPU selection; memory and latency profiling; offline fallback. |
| Prerequisites | Audio buffers, deterministic command loop, basic threads/processes and asyncio. |
| Purpose | Prevent dropped audio, runaway memory, and UI freezes while keeping core functions available without internet. |
| Application | V0.2 and V0.4. VAD separates speech from silence; a wake word is optional and should be added only after push-to-talk is reliable. |
| Practical work | Add a bounded audio queue and explicit stop button; run a 30-minute listening soak; compare a Vosk streaming path with chunked faster-whisper; profile model startup and per-clip latency; disconnect the network and exercise local commands. |
| Completion criteria | Queue size remains bounded; errors do not strand the microphone; cancellation releases audio resources; offline test proves which functions do and do not require network. |
| Priority | High. |
| Recommended docs | [asyncio](https://docs.python.org/3/library/asyncio.html), [Threading](https://docs.python.org/3/library/threading.html), [Vosk](https://alphacephei.com/vosk/), [Silero VAD](https://github.com/snakers4/silero-vad), [openWakeWord](https://github.com/pozalabs/openwakeword), [Piper TTS](https://github.com/OHF-Voice/piper1-gpl). |

### 7. Machine-learning and LLM fundamentals

| Field | Plan |
|---|---|
| Subject | Enough ML and LLM knowledge to use inference systems critically. |
| Subtopics | Training versus inference; neural-network and transformer intuition; tokenization; context windows; prompts and system instructions; sampling; quantization; model size and memory; latency; structured outputs; model limitations and hallucination. Training a foundation model is out of scope. |
| Prerequisites | Python and JSON; basic probability/statistics is useful but not a blocker for inference experiments. |
| Purpose | Choose models using measured capability/resource tradeoffs rather than model names or assumptions. |
| Application | Local Ollama or a provider adapter, response generation, tool selection, and optional image understanding. |
| Practical work | Call one local model with fixed prompts; compare responses and timing for the same test set; parse a strict JSON schema; record model, hardware, settings, and failures. |
| Completion criteria | Explain tokens/context and inference versus training; validate output before use; show that a model answer is not evidence that a tool was correctly executed. |
| Priority | High for V0.5; otherwise optional until the deterministic assistant is stable. |
| Recommended docs | [Ollama chat API](https://docs.ollama.com/api/chat), [PyTorch tutorials](https://docs.pytorch.org/tutorials/). |

### 8. Tool calling, task planning, and agent safety

| Field | Plan |
|---|---|
| Subject | Constrained, auditable use of tools by an LLM. |
| Subtopics | Tool registry; names/descriptions and typed inputs; schema validation; planning; one-step execution before multi-step loops; policy checks; user confirmation; permissions; timeouts; idempotency; cancellation; error recovery; action audit records; prompt injection and untrusted tool output. |
| Prerequisites | Deterministic command registry, JSON schemas, API input validation, and basic security boundaries. |
| Purpose | A model can propose an action, but application code must decide whether that action is allowed and safe. |
| Application | V0.5 controlled AI actions and later ecosystem tools. |
| Practical work | Expose three read-only tools (time, search a fixed local note set, list allowed app names); pass model outputs through a Pydantic schema and policy gate; add a confirmation step to any state-changing test tool. |
| Completion criteria | Invalid tool arguments cause no side effects; unknown tools are rejected; all side effects are logged; high-impact actions require explicit confirmation; a model cannot access a generic shell. |
| Priority | Essential before any LLM tool execution. |
| Recommended docs | [Ollama tool calling API](https://docs.ollama.com/api/chat), [Pydantic models](https://pydantic.dev/docs/validation/latest/concepts/models/), [OWASP API Security Top 10](https://devguide.owasp.org/en/07-training-education/07-api-top-ten/). |

### 9. Local memory, databases, and retrieval

| Field | Plan |
|---|---|
| Subject | Conversation state and durable personal knowledge with explicit retention. |
| Subtopics | Relational tables and keys; CRUD; transactions; migrations; SQLite; text search; embeddings; vector similarity; metadata; chunking; retrieval-augmented generation (RAG); source attribution; deletion and retention. |
| Prerequisites | Python data structures and JSON; basic SQL before vector search. |
| Purpose | Keep short-lived context separate from user-approved durable memory and make recalled information traceable. |
| Application | Conversation history, preferences, command audit log, and later knowledge-base retrieval. |
| Practical work | Store conversations and approved memories in SQLite; add full-text search first; prototype an embeddings/vector index only on a small test corpus and compare retrieval against keyword search. |
| Completion criteria | Every stored item has an owner/source and retention rule; users can inspect/delete it; retrieval returns source IDs; the assistant does not silently convert all transcripts into permanent memory. |
| Priority | High for AI; SQLite is the initial choice, vector database is optional. |
| Recommended docs | [Python sqlite3](https://docs.python.org/3/library/sqlite3.html), [SQLite quickstart](https://www.sqlite.org/quickstart.html), [Chroma docs](https://docs.trychroma.com/). |

### 10. Backend APIs and networking

| Field | Plan |
|---|---|
| Subject | A narrow local service for desktop and phone clients. |
| Subtopics | REST resource design; HTTP status codes; Pydantic request/response models; OpenAPI; WebSockets for live status; authentication; authorization; TLS; rate limits; origins/CORS; network binding; health checks; error contracts; reconnects. |
| Prerequisites | Client/server networking, JSON, Python modules, and input validation. |
| Purpose | Create a stable boundary between the assistant engine and device-specific interfaces. |
| Application | Local PC API for the phone companion; future web/mobile UI. |
| Practical work | Build a FastAPI service with health, command submission, and status endpoints; initially bind to localhost; add an authenticated LAN mode only after threat modeling. |
| Completion criteria | API docs describe every request; invalid requests fail safely; unauthorized devices cannot submit commands; a reconnect does not repeat a command; service errors are observable. |
| Priority | High for V0.6. |
| Recommended docs | [FastAPI tutorial](https://fastapi.tiangolo.com/tutorial/), [Pydantic](https://pydantic.dev/docs/validation/latest/concepts/models/), [OWASP API Top 10](https://devguide.owasp.org/en/07-training-education/07-api-top-ten/). |

### 11. Android companion and phone-to-PC communication

| Field | Plan |
|---|---|
| Subject | A lightweight, permission-aware Android client. |
| Subtopics | Android app lifecycle; runtime permissions; microphone/camera permissions; background execution and foreground-service restrictions; local storage; ADB; Termux; REST/WebSocket clients; device identity; reconnection; battery and thermal behavior; TLS; Android UI states. |
| Prerequisites | API concepts and basic client/server debugging. Native Android development can wait until the API contract is stable. |
| Purpose | Use the Infinix Smart 7 as a microphone, speaker, screen, camera, and remote control while inference runs on the PC. |
| Application | V0.6. Begin with push-to-talk and status; camera and background audio are separate, explicit features. |
| Practical work | First prototype with a simple authenticated client; compare a web client, Termux prototype, and native Android app before choosing. Use ADB for development inspection only, not as the production command channel. |
| Completion criteria | Permission denial leaves the rest of the client usable; a device can be revoked; 20 disconnect/reconnect cycles recover without duplicate actions; the main model is not required on the phone. |
| Priority | High for V0.6; native app and always-on background listening are later work. |
| Recommended docs | [Android runtime permissions](https://developer.android.com/training/permissions/requesting), [Foreground service types](https://developer.android.com/about/versions/14/changes/fgs-types-required), [Tailscale Android install](https://tailscale.com/docs/install/android). |

### 12. Computer vision, gesture recognition, and motion capture

| Field | Plan |
|---|---|
| Subject | Camera input and movement interpretation. |
| Subtopics | Pixel arrays and color spaces; image transforms; frame rate and camera latency; calibration; hand/pose landmarks; coordinate systems; tracking; temporal windows; classification; thresholds and smoothing; object detection; sensor fusion. |
| Prerequisites | Python arrays, basic probability, image/video I/O; linear algebra is helpful for 3D work. |
| Purpose | Enable selected visual context and gestures without confusing landmark tracking with recognition or full motion capture. |
| Application | V0.7 gesture controls and V0.8 image-plus-voice interaction. This is a parallel track and must not block V0.4 offline voice. |
| Practical work | Capture one camera stream with OpenCV; display hand landmarks with MediaPipe; classify three gestures from short time windows; test lighting, distance, occlusion, and background variation. |
| Completion criteria | State the distinction: tracking locates landmarks over time; gesture recognition classifies a pose/movement; full motion capture estimates a broader 3D/body motion system and may require calibration or additional sensors. Measure precision/recall and false activations. |
| Priority | Medium; start after a dependable voice core. |
| Recommended docs | [OpenCV tutorials](https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html), [MediaPipe Hand Landmarker for Python](https://developers.google.com/edge/mediapipe/solutions/vision/hand_landmarker/python), [scikit-learn tutorial](https://scikit-learn.org/stable/tutorial/basic/tutorial.html). |

### 13. Multimodal fusion and event processing

| Field | Plan |
|---|---|
| Subject | Combining text, audio, images, gestures, and device events. |
| Subtopics | Vision-language models and image/audio understanding; timestamps; event IDs; modality-specific confidence; sensor fusion and synchronization windows; snapshot versus continuous video; cancellation; bounded queues; asynchronous inference; context selection; result provenance; ambiguity handling. |
| Prerequisites | Stable audio and vision adapters; event/API contracts; basic concurrency and model inference. |
| Purpose | Combine a voice request with a specific, user-authorized snapshot or gesture without treating unrelated sensor data as context. |
| Application | V0.8 “point at an object and ask about it” flow. |
| Practical work | Capture a still image only on request; attach its timestamp and camera ID to the speech event; return a short answer plus uncertainty; run scripted scenarios with and without a usable image. |
| Completion criteria | A response can be traced to the image and transcript used; no continuous camera feed is saved by default; stale/late events are discarded or surfaced; the user can cancel the request. |
| Priority | Medium. |
| Recommended docs | [MediaPipe Hand Landmarker](https://developers.google.com/edge/mediapipe/solutions/vision/hand_landmarker/python), [Ollama chat API](https://docs.ollama.com/api/chat). |

### 14. UI/UX and accessibility

| Field | Plan |
|---|---|
| Subject | Clear interaction and visible system state. |
| Subtopics | Push-to-talk; listening/thinking/speaking states; transcripts; confirmations; error recovery; keyboard and touch access; contrast; focus; Tkinter desktop UI; HTML/CSS/JavaScript web UI; responsive layouts; audio level and latency indicators; privacy controls. |
| Prerequisites | A working command loop and API boundaries. |
| Purpose | Make the assistant understandable, interruptible, and usable when speech recognition fails. |
| Application | Tkinter desktop interface first; web/mobile surfaces after the engine API settles. |
| Practical work | Design a single-screen prototype with PTT, transcript, status, cancel, and a permissions indicator; test it with a quiet-room and noisy-room scenario. |
| Completion criteria | The user can tell when the microphone/camera is active, what was recognized, whether a tool will run, and how to stop it; keyboard interaction covers primary controls. |
| Priority | High for a usable V0.3; advanced visualizations are optional. |
| Recommended docs | [Tkinter](https://docs.python.org/3/library/tkinter.html), [WCAG 2.2](https://www.w3.org/TR/WCAG22/). |

### 15. Hardware, sensors, and IoT

| Field | Plan |
|---|---|
| Subject | Optional sensor and home-device integrations. |
| Subtopics | Microphone/camera selection; USB and serial; GPIO; voltage/current and power budgeting; sensor sampling; microcontrollers; ESP32; MQTT topics and payloads; device discovery; Home Assistant; failure states and safe defaults. |
| Prerequisites | Basic circuits and networking; command authorization and security model must already exist before controlling devices. |
| Purpose | Extend JARVIS to hardware and home systems without coupling device drivers to the assistant core. |
| Application | V1.0 ecosystem integrations, with ESP32 or Home Assistant as optional adapters. |
| Practical work | Simulate an MQTT sensor and a read-only Home Assistant integration; only later expose one reversible device control behind explicit confirmation. |
| Completion criteria | Lost broker/network connection fails safely; topic permissions are scoped; an adapter can be disabled without breaking voice; hardware wiring and power assumptions are documented. |
| Priority | Optional until a specific sensor or device is chosen. |
| Recommended docs | [ESP-IDF for ESP32](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/), [Home Assistant MQTT](https://www.home-assistant.io/integrations/mqtt/). |

### 16. Deployment, packaging, and reliability

| Field | Plan |
|---|---|
| Subject | Reproducible installs, operating-system adapters, updates, and recovery. |
| Subtopics | Windows/Linux/macOS differences; path and process adapters; Python packaging; native audio dependencies; PyInstaller; Docker/Compose for services; CI/CD; configuration; upgrade/rollback; logs and health; backups; restore drills; crash recovery. |
| Prerequisites | Tests, dependency management, architecture boundaries, and a stable first release. |
| Purpose | Deliver one supported deployment reliably before claiming cross-platform support. |
| Application | V0.1–V0.5 on the primary PC; V1.0 for documented host/client deployment. |
| Practical work | Package a small speech-to-text tool for the current PC; add CI for unit tests; containerize only the API/storage pieces if it simplifies deployment. |
| Completion criteria | A clean setup guide works on the declared target; missing model/dependency errors are clear; configuration and secrets stay outside source; restore a test backup; every supported platform has a smoke-test record. |
| Priority | High before public or multi-device release; multiple platforms are optional until selected. |
| Recommended docs | [Python Packaging User Guide](https://packaging.python.org/en/latest/), [PyInstaller](https://pyinstaller.org/en/stable/), [Docker Compose](https://docs.docker.com/get-started/introduction/index.html), [GitHub Actions for Python](https://docs.github.com/en/actions/tutorials/build-and-test-code/python). |

### 17. Security, privacy, and safety engineering

| Field | Plan |
|---|---|
| Subject | Protecting the microphone, camera, personal data, devices, and action surface. |
| Subtopics | Threat modeling; least privilege; API keys and environment variables; device authentication; authorization; TLS; local data at rest; retention and deletion; log redaction; safe subprocess use; input validation; rate limits; prompt injection; confirmation policy; update integrity. |
| Prerequisites | Basic networking, API design, persistence, and tool registry. |
| Purpose | Voice transcripts, images, personal knowledge, and OS actions are sensitive; a confident model response does not establish permission. |
| Application | Every release, with stronger boundaries at V0.5, V0.6, and V1.0. |
| Practical work | Write a threat model listing assets, actors, trust boundaries, and mitigations; test unauthorized phone requests, malformed tool JSON, revoked tokens, and network loss. |
| Completion criteria | Secrets are never committed or logged; tools are allowlisted; destructive/external actions require confirmation; local-only operation is available; microphone/camera state and data retention are visible to the user. |
| Priority | Essential and continuous. |
| Recommended docs | [OWASP API Security Top 10](https://devguide.owasp.org/en/07-training-education/07-api-top-ten/), [Python subprocess](https://docs.python.org/3/library/subprocess.html), [Android permissions](https://developer.android.com/training/permissions/requesting). |

## Evaluation notebook

Keep one small repeatable dataset per modality. Do not upload private speech or images to a cloud service without deliberate consent.

| Area | Record |
|---|---|
| ASR | Model/version, language, sample rate, clip duration, WER, exact-command accuracy, median/p95 inference time, RAM/VRAM, network use. |
| VAD/wake word | Speech detection misses, false activations per hour, CPU use, time to stop, test room/noise conditions. |
| TTS | Startup time, first-audio latency, interruption behavior, pronunciation issues, voice/model license. |
| Tools | Valid/invalid schema rate, safe rejection rate, approval coverage, side effects, audit record completeness. |
| Phone/API | Auth failures, reconnect count, p50/p95 request time, battery/thermal behavior, duplicate request count. |
| Vision | Per-gesture precision/recall, false activations, frame rate, lighting/distance/occlusion, whether any frame was saved. |

## First three learning tasks

1. Build a small Python command-line program using functions, dictionaries, JSON files, exceptions, logging, a virtual environment, and Git.
2. Record and replay a short WAV file with SoundDevice; inspect its sample rate, channels, duration, and clipping.
3. Transcribe the same small set of labeled clips with two candidate ASR engines and record WER and latency before choosing an engine.
