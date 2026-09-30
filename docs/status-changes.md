# Status Changes

Notable renames, archival notices, dormancy, and license gotchas affecting entries in this list. Last reviewed 2026-09-30.

## Renames / moves

- **NVIDIA NeMo → NVIDIA-NeMo/Speech** — the `NVIDIA/NeMo` repo was renamed; the speech work now lives at `NVIDIA-NeMo/Speech`. Old URLs redirect.
- **Moonshine: UsefulSensors/moonshine → moonshine-ai/moonshine** — repo moved to the `moonshine-ai` org; old URL 301-redirects.
- **WhisperKit: argmaxinc/whisperkit → argmaxinc/argmax-oss-swift** — renamed; actively maintained (pushed 2026-09-24).
- **whisper_streaming** — canonical repo is `ufal/whisper_streaming` (underscore, not hyphen).
- **WeSpeaker** — canonical repo is `wenet-e2e/wespeaker` (`wespeaker/wespeaker` 404s).
- **deep-multilingual-punctuation** — the commonly cited slug with hyphens does not exist; the real repo is `oliverguhr/deepmultilingualpunctuation` (no hyphens).

## Archived / dormant

- **stable-ts** — archived by the maintainer; kept in the list with an explicit archived note.
- **fairseq** — archived (read-only) September 2026; wav2vec2-family coverage in this list goes through Hugging Face checkpoints instead.
- **Kaldi** — in maintenance mode; the predecessor of the modern E2E stacks, kept for historical completeness.
- **Coqui STT** — dormant since March 2024 (company shut down); excluded from the active list.
- **whisper-jax** — dormant since April 2024; maintainers describe it as effectively archived (superseded by Distil-Whisper / faster-whisper); excluded.
- **whisper.spm / SwiftWhisper** — stale since May 2024, superseded by WhisperKit; excluded.

## License gotchas (verified on official sources)

- **SeamlessM4T v2** — `CC-BY-NC-4.0` confirmed verbatim in the repo LICENSE (non-commercial), not MIT as some lists claim.
- **MMS 1B** — `CC-BY-NC-4.0` on the Hugging Face card (non-commercial).
- **Silero STT** — repo LICENSE is `CC-BY-NC-SA-4.0` (non-commercial, share-alike).
- **NVIDIA weights** (Parakeet, Canary, FastConformer) — `CC-BY-4.0`: commercial use allowed, attribution required.
- **whisper-timestamped** — `AGPL-3.0` (strong copyleft; network use counts).
- **aeneas** — `AGPL-3.0`.
- **GigaSpeech** — repo tagged Apache-2.0 but access is restricted to non-commercial research use; check terms before use.
- **pyannote.audio** — code is MIT, but the pretrained diarization pipelines on Hugging Face are gated under custom terms.
- **Moonshine** — GitHub API reports `NOASSERTION`, but the repo LICENSE file states MIT for code and MIT for models by default (with additional sectioned terms); recorded as MIT with this caveat.
- **MERaLiON-AudioLLM** — custom MERaLiON public license (non-OSI); not open source in the OSI sense.

## Model/API naming notes (2026-09-30)

- AssemblyAI's current flagship is **Universal-3.5 Pro** (async + realtime variants); older "Universal-1/2" naming is superseded.
- Speechmatics' current models are **Melia 1** (batch) and **Linden 1** ("Agent STT", real-time); "Flow" is their voice-agent product, not an STT model.
- Deepgram's current family is **Nova-3** (+ Flux conversational models).
- OpenAI's STT API offers the **gpt-4o-transcribe** family (incl. `gpt-4o-transcribe-diarize`) alongside `whisper-1`.
- ElevenLabs **Scribe v2** covers batch and realtime (`scribe_v2_realtime`).
