# Awesome LLM ASR

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Entries](https://img.shields.io/badge/entries-80-blue)](data/asr.json)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A curated list of **LLM-era automatic speech recognition** (speech-to-text): foundation ASR models, commercial STT APIs, audio LLMs, toolkits and runtimes, streaming, edge/on-device inference, benchmarks, training resources, diarization, and post-processing.

> **Scope:** speech-to-text only. TTS-only projects are out of scope (toolkits that do both, like sherpa-onnx, are included).
> **Honesty policy:** every entry was verified on an official source (project repo or official site) as of 2026-09-30 — 80/80 verified. Proprietary APIs and models are explicitly labeled and never presented as open source. Non-commercial licenses (CC-BY-NC-*) are flagged in the entry itself. Machine-readable data lives in [`data/asr.json`](data/asr.json).

## Contents

- [Foundation Models](#foundation-models) — 15 entries
- [Commercial STT APIs](#commercial-stt-apis) — 12 entries
- [Audio LLMs](#audio-llms) — 10 entries
- [Toolkits & Runtimes](#toolkits--runtimes) — 12 entries
- [Streaming & Real-Time ASR](#streaming--real-time-asr) — 6 entries
- [Edge & On-Device](#edge--on-device) — 4 entries
- [Benchmarks & Evals](#benchmarks--evals) — 12 entries
- [Training & Fine-Tuning](#training--fine-tuning) — 3 entries
- [Diarization](#diarization) — 3 entries
- [Post-Processing](#post-processing) — 3 entries

## Choosing the right ASR

New here? Start with the [choosing-an-asr-model](docs/choosing-an-asr-model.md) guide (accuracy vs. speed vs. cost, open vs. API, licensing traps), the [glossary](docs/glossary.md), and [status-changes](docs/status-changes.md) (renames, archival notices, license gotchas).

## Foundation Models

Open-weight and open-source speech models that define the accuracy frontier — the checkpoints everything else builds on. (15 entries)

- [Whisper](https://github.com/openai/whisper) — OpenAI's multilingual encoder-decoder speech model (tiny through large-v3, incl. large-v3-turbo); the de facto reference ASR foundation, with an official PyTorch implementation and CLI. *(MIT · ⭐ 109,801)*
- [whisper-large-v3](https://huggingface.co/openai/whisper-large-v3) — OpenAI Whisper large-v3 weights on Hugging Face; the strongest full Whisper checkpoint before the turbo distillation. *(Apache-2.0)*
- [whisper-large-v3-turbo](https://huggingface.co/openai/whisper-large-v3-turbo) — Distilled, ~8x-faster variant of Whisper large-v3 with near-parity accuracy; drop-in checkpoint for the HF transformers pipeline. *(MIT)*
- [Distil-Whisper large-v3](https://huggingface.co/distil-whisper/distil-large-v3) — Hugging Face distilled Whisper large-v3: 6x faster, 49% smaller, ~1% WER gap; long-form compatible. *(MIT)*
- [Distil-Whisper large-v3.5](https://huggingface.co/distil-whisper/distil-large-v3.5) — Updated Distil-Whisper distillation targeting improved short-form accuracy. *(MIT)*
- [Parakeet TDT 0.6B v3](https://huggingface.co/nvidia/parakeet-tdt-0.6b-v3) — NVIDIA's 0.6B transducer ASR model (TDT decoder); top open English accuracy. Weights CC-BY-4.0 (attribution required). *(CC-BY-4.0)*
- [Parakeet RNN-T 0.6B](https://huggingface.co/nvidia/parakeet-rnnt-0.6b) — RNN-T variant of Parakeet 0.6B for streaming-friendly transducer decoding. Weights CC-BY-4.0. *(CC-BY-4.0)*
- [Parakeet CTC 0.6B](https://huggingface.co/nvidia/parakeet-ctc-0.6b) — CTC-decoded Parakeet 0.6B for fast non-autoregressive, high-throughput inference. Weights CC-BY-4.0. *(CC-BY-4.0)*
- [Canary 1B v2](https://huggingface.co/nvidia/canary-1b-v2) — NVIDIA's 1B multilingual (EN/DE/ES/FR) encoder-decoder ASR/AST model built with NeMo. Weights CC-BY-4.0. *(CC-BY-4.0)*
- [FastConformer-CTC (NeMo)](https://huggingface.co/nvidia/stt_en_fastconformer_ctc_large) — NVIDIA's efficient Conformer-CTC English ASR; the encoder lineage behind Parakeet. Weights CC-BY-4.0. *(CC-BY-4.0)*
- [wav2vec 2.0 XLS-R](https://huggingface.co/facebook/wav2vec2-xls-r-1b) — Meta's self-supervised multilingual speech encoder (128 languages); fine-tune per language for ASR. *(Apache-2.0)*
- [MMS 1B](https://huggingface.co/facebook/mms-1b-all) — Meta Massively Multilingual Speech: wav2vec2-based model covering 1,000+ languages. Research/non-commercial license. *(CC-BY-NC-4.0)*
- [SeamlessM4T v2](https://github.com/facebookresearch/seamless_communication) — Meta's unified speech translation foundation (ASR + translation, 100+ languages). Non-commercial license (CC-BY-NC-4.0, confirmed in the repo LICENSE). *(CC-BY-NC-4.0 · ⭐ 11,883)*
- [Icefall / Zipformer](https://github.com/k2-fsa/icefall) — k2-based speech recipe zoo; home of Zipformer, the parameter-efficient transducer/conformer architecture. *(Apache-2.0 · ⭐ 1,511)*
- [Moonshine](https://github.com/moonshine-ai/moonshine) — Tiny edge-first speech-to-text models with near-Whisper accuracy at a fraction of the size; built for on-device voice agents. MIT code and models (repo moved from UsefulSensors/moonshine to moonshine-ai/moonshine). *(MIT · ⭐ 11,162)*

## Commercial STT APIs

Hosted speech-to-text APIs. All proprietary with usage-based pricing — listed for completeness, never as open source. (12 entries)

- [Deepgram](https://deepgram.com/pricing) — Real-time and batch speech-to-text API built around the Nova-3 model family, plus Flux conversational models; usage-based pricing. *(proprietary)*
- [AssemblyAI](https://www.assemblyai.com/pricing/) — Speech AI API with Universal-3.5 Pro (async and realtime) models, diarization, and audio-intelligence add-ons; usage-based pricing. *(proprietary)*
- [OpenAI Speech-to-Text API](https://platform.openai.com/docs) — Speech-to-text API with the gpt-4o-transcribe family (including gpt-4o-transcribe-diarize) and whisper-1; usage-based pricing. *(proprietary)*
- [Speechmatics](https://www.speechmatics.com/pricing) — Speech-to-text API with Melia 1 (batch) and Linden 1 (Agent STT, real-time) models, plus on-premise options; usage-based pricing. *(proprietary)*
- [Rev AI](https://www.rev.ai/pricing) — Speech-to-text API (async and streaming) with Reverb models and optional human transcription services; usage-based pricing. *(proprietary)*
- [Fireworks AI](https://Fireworks.ai/blog/audio-transcription-launch) — Fast Whisper (v3 large/turbo) transcription API for batch and streaming audio; usage-based pricing. *(proprietary)*
- [ElevenLabs Scribe](https://elevenlabs.io/docs/models) — Speech-to-text API with Scribe v2 (batch) and scribe_v2_realtime models, diarization and word-level timestamps; usage-based pricing. *(proprietary)*
- [Cartesia](https://docs.cartesia.ai/build-with-cartesia/stt/latest) — Speech-to-text API with Ink models (Ink-2 streaming, ink-whisper batch) built for voice agents; usage-based pricing. *(proprietary)*
- [Gladia](https://www.Gladia.io/product/async-transcription) — Multilingual speech-to-text API (Solaria-1/3 models) with diarization and audio intelligence bundled in; usage-based pricing. *(proprietary)*
- [Soniox](https://soniox.com/pricing) — Streaming and async speech-to-text API (stt-rt-v5 / stt-async-v5) with bundled diarization and translation; usage-based pricing. *(proprietary)*
- [Symbl.ai](https://docs.symbl.ai/docs/conversation-api/messages) — Conversation-intelligence API with built-in real-time and async transcription plus summaries, entities, and sentiment; usage-based pricing. *(proprietary)*
- [Vatis Tech](https://vatis.tech/speech-to-text/hindi-speech-to-text) — Speech-to-text API and transcription platform with real-time and on-premise options; usage-based pricing. *(proprietary)*

## Audio LLMs

Multimodal LLMs with native transcription ability — end-to-end speech understanding without a separate ASR stage. (10 entries)

- [GPT-4o audio](https://openai.com/index/hello-gpt-4o/) — OpenAI's multimodal GPT-4o with audio input for transcription and speech understanding via the API; API-only, no open weights. *(proprietary)*
- [Gemini 3.5 Transcribe](https://ai.google.dev) — Google's dedicated transcription models (gemini-3.5-transcribe / transcribe-live) on the Gemini API and Vertex AI; API-only. *(proprietary)*
- [Qwen3-Omni](https://huggingface.co/Qwen) — Alibaba's omni-modal LLM (text, image, audio, video) with speech-to-text ability; weights released under Apache 2.0. *(Apache-2.0)*
- [Phi-4-multimodal](https://huggingface.co/microsoft/Phi-4-multimodal-instruct) — Microsoft's small (5.6B) multimodal model handling speech, vision, and text with strong ASR performance; released under MIT. *(MIT)*
- [Ultravox](https://ultravox.ai/) — Open-weight multimodal speech LLM by Fixie that feeds audio directly into the LLM without a separate ASR stage; MIT. *(MIT · ⭐ 4,574)*
- [SALMONN](https://github.com/bytedance/SALMONN) — Multimodal LLM family by ByteDance and Tsinghua for general audio understanding including speech recognition; Apache-2.0. *(Apache-2.0 · ⭐ 1,538)*
- [Voxtral](https://huggingface.co/mistralai/Voxtral-Mini-4B-Realtime-2602) — Mistral's open-weight audio LLM family for transcription and voice understanding, including a streaming Realtime variant; Apache-2.0. *(Apache-2.0)*
- [Granite Speech](https://huggingface.co/ibm-granite/granite-speech-4.1-2b) — IBM's speech LLM for ASR and speech translation (Granite Speech 4.1 2B variants, including speaker-attributed Plus); Apache-2.0. *(Apache-2.0)*
- [NVIDIA Canary-Qwen](https://huggingface.co/nvidia/canary-qwen-2.5b) — English ASR pairing a FastConformer encoder with a Qwen LLM, with ASR-only and LLM post-processing modes (punctuation/capitalization). Weights CC-BY-4.0. *(CC-BY-4.0)*
- [MERaLiON-AudioLLM](https://huggingface.co/MERaLiON/AudioLLM) — Whisper + SEA-LION based speech-text model by AI Singapore tuned for Singaporean accents and code-switching; custom MERaLiON public license (non-OSI). *(custom (MERaLiON public license, non-OSI))*

## Toolkits & Runtimes

Libraries, servers, and frameworks for running, serving, and integrating ASR models. (12 entries)

- [whisper.cpp](https://github.com/ggml-org/whisper.cpp) — Port of Whisper to plain C/C++ with no dependencies; runs on CPU, Metal, CUDA and Vulkan with a built-in server, and ships ggml-format models for all Whisper sizes. *(MIT · ⭐ 54,045)*
- [faster-whisper](https://github.com/SYSTRAN/faster-whisper) — CTranslate2-based Whisper reimplementation: up to ~4x faster with lower memory; SYSTRAN ships ct2-converted Whisper checkpoints on Hugging Face. *(MIT · ⭐ 25,647)*
- [WhisperX](https://github.com/m-bain/whisperX) — Whisper plus VAD and wav2vec2-based forced alignment for fast, word-level-timestamped, diarizable long-form transcription. *(BSD-2-Clause · ⭐ 24,318)*
- [NVIDIA NeMo](https://github.com/NVIDIA-NeMo/Speech) — NVIDIA's scalable framework for speech AI research, training, and deployment; home of the Parakeet/Canary/FastConformer recipes and the ASR fine-tuning workflow. Repo moved from NVIDIA/NeMo to NVIDIA-NeMo/Speech. *(Apache-2.0 · ⭐ 18,531)*
- [SpeechBrain](https://github.com/speechbrain/speechbrain) — PyTorch speech toolkit with full ASR recipes (LibriSpeech, Common Voice, multilingual) and pretrained models; recipe-first, reproducibility-focused. *(Apache-2.0 · ⭐ 11,849)*
- [whisper-timestamped](https://github.com/linto-ai/whisper-timestamped) — Multilingual Whisper transcription with word-level timestamps and confidence scores. *(AGPL-3.0 · ⭐ 2,851)*
- [stable-ts](https://github.com/jianfch/stable-ts) — stable-whisper fork for transcription, forced alignment and audio indexing; the repo is archived (no longer maintained). *(MIT · ⭐ 2,281)*
- [transformers](https://github.com/huggingface/transformers) — Hugging Face automatic-speech-recognition pipelines plus the model hub behind dozens of ASR checkpoints. *(Apache-2.0 · ⭐ 166,860)*
- [ESPnet](https://github.com/espnet/espnet) — End-to-end speech processing toolkit covering ASR, TTS, speech translation and diarization. *(Apache-2.0 · ⭐ 9,976)*
- [WeNet](https://github.com/wenet-e2e/wenet) — Production-oriented end-to-end speech recognition toolkit with streaming (U2/U2++) support. *(Apache-2.0 · ⭐ 5,243)*
- [FunASR](https://github.com/modelscope/FunASR) — Alibaba ModelScope open-source speech toolkit: training, inference, streaming ASR, VAD, punctuation and diarization. *(MIT · ⭐ 20,559)*
- [Kaldi](https://github.com/kaldi-asr/kaldi) — Classic HMM/DNN speech recognition toolkit; largely in maintenance mode and the predecessor of the modern stacks. *(Apache-2.0 · ⭐ 15,490)*

## Streaming & Real-Time ASR

Low-latency, streaming-first transcription for live audio and voice agents. (6 entries)

- [whisper_streaming](https://github.com/ufal/whisper_streaming) — Real-time streaming transcription and translation with Whisper using a self-adaptive latency policy. *(MIT · ⭐ 3,674)*
- [WhisperLive](https://github.com/collabora/WhisperLive) — Nearly-live Whisper transcription server and client communicating over websockets. *(MIT · ⭐ 4,303)*
- [RealtimeSTT](https://github.com/KoljaB/RealtimeSTT) — Low-latency speech-to-text library with advanced VAD and wake-word activation. *(MIT · ⭐ 10,158)*
- [Pipecat](https://github.com/pipecat-ai/pipecat) — Open-source framework for real-time voice agents and multimodal apps with pluggable STT services. *(BSD-2-Clause · ⭐ 16,090)*
- [LiveKit Agents](https://github.com/livekit/agents) — Framework for building realtime voice AI agents; STT is provided via livekit-plugins-* packages (Deepgram, OpenAI, etc.). *(Apache-2.0 · ⭐ 14,434)*
- [Silero STT](https://github.com/snakers4/silero-models) — Small streaming-capable pre-trained STT models; the repo LICENSE is CC-BY-NC-SA 4.0 (non-commercial). *(CC-BY-NC-SA-4.0 · ⭐ 6,124)*

## Edge & On-Device

Offline, small-footprint transcription for phones, laptops, and embedded devices. (4 entries)

- [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) — On-device speech-to-text (plus TTS, diarization, VAD, enhancement) via ONNX Runtime, including streaming and edge builds. *(Apache-2.0 · ⭐ 15,060)*
- [Vosk](https://github.com/alphacep/vosk-api) — Offline speech recognition API for Android, iOS, Raspberry Pi and servers with small-footprint models. *(Apache-2.0 · ⭐ 15,158)*
- [WhisperKit](https://github.com/argmaxinc/argmax-oss-swift) — On-device Whisper inference via Core ML for Apple platforms (Swift); repo renamed from argmaxinc/whisperkit to argmax-oss-swift. *(MIT · ⭐ 6,385)*
- [mlx-whisper](https://github.com/ml-explore/mlx-examples/tree/main/whisper) — Apple MLX port of Whisper for Apple Silicon, shipped as an example in mlx-examples (also a pip package); the star count is the parent repo's. *(MIT · ⭐ 8,985)*

## Benchmarks & Evals

Datasets, corpora, and leaderboards used to measure ASR quality — plus the papers behind them. (12 entries)

- [LibriSpeech](https://www.openslr.org/12) — The canonical ~960-hour read-speech benchmark of audiobook recordings; the default WER touchstone for ASR research, including LLM-era systems. Paper: arXiv 1504.04374. *(CC-BY-4.0)*
- [FLEURS](https://huggingface.co/datasets/google/fleurs) — Google's massively multilingual speech benchmark covering 102 languages, used to evaluate the multilingual ability of speech models. Paper: arXiv 2205.12446. *(CC-BY-4.0)*
- [Earnings-21](https://github.com/revdotcom/speech-datasets) — ~39 hours of US earnings calls released by Rev for ASR benchmarking; a real-world spontaneous-speech eval set. Paper: arXiv 2104.11348. *(CC-BY-SA-4.0)*
- [Earnings-22](https://github.com/revdotcom/speech-datasets) — ~119 hours of accented global earnings calls (125 files) released by Rev for domain-robustness ASR evaluation. Paper: arXiv 2203.15591. *(CC-BY-SA-4.0)*
- [Common Voice](https://commonvoice.mozilla.org/en/datasets) — Mozilla's crowdsourced multilingual speech corpus (v27.0, ~295 locales), a workhorse training and evaluation source for open ASR; downloads moved to the Mozilla Data Collective. CC0 public domain. *(CC0-1.0)*
- [TED-LIUM 3](https://www.openslr.org/51) — 452 hours of TED-talk recordings for ASR evaluation, a standard long-form prepared-speech benchmark. Note the restrictive license. Paper: arXiv 1805.04699. *(CC-BY-NC-ND-3.0)*
- [VoxPopuli](https://github.com/facebookresearch/voxpopuli) — Meta's multilingual corpus: 100K hours of unlabeled speech (23 languages) plus 1.8K hours of transcribed speech (16 languages). License terms vary by subset; the transcribed ASR subset is distributed under CC0 per the HF ESB card. Paper: arXiv 2101.00390. *(terms vary — see notes)*
- [GigaSpeech](https://github.com/SpeechColab/GigaSpeech) — 10,000 hours of transcribed English speech from audiobooks, podcasts and YouTube — one of the largest open ASR corpora. Licensing caveat: the repo is tagged Apache-2.0 but actual access is restricted to non-commercial research use; check terms before use. *(terms vary — see notes)*
- [Open ASR Leaderboard](https://huggingface.co/spaces/hf-audio/open_asr_leaderboard) — The Hugging Face community leaderboard for ASR models, run with NVIDIA, Mistral and Cambridge: 60+ models ranked across 11+ datasets in English, multilingual and long-form tracks. *(terms vary — see notes)*
- [SUPERB](https://arxiv.org/abs/2105.01051) — The frozen-self-supervised-learning speech benchmark, probing how well upstream representations serve downstream tasks including ASR. Paper: arXiv 2105.01051. *(terms vary — see notes)*
- [ML-SUPERB](https://arxiv.org/abs/2305.10615) — The multilingual extension of SUPERB, benchmarking self-supervised speech representations across many languages. Paper: arXiv 2305.10615. *(terms vary — see notes)*
- [AudioBench](https://github.com/AudioLLMs/AudioBench) — A universal benchmark for audio-capable LLMs across speech, sound and music understanding — the audio-LLM-era eval standard. Paper: arXiv 2406.16020. *(terms vary — see notes)*

## Training & Fine-Tuning

Guides, data tooling, and recipes for adapting ASR models to your domain. (3 entries)

- [Lhotse](https://github.com/lhotse-speech/lhotse) — The next-generation Kaldi-style speech data-preparation library: efficient, iterable corpus management for large-scale ASR training. Paper: arXiv 2110.12561. *(Apache-2.0 · ⭐ 1,154)*
- [Fine-Tune Whisper (Hugging Face guide)](https://huggingface.co/blog/fine-tune-whisper) — Hugging Face's official end-to-end guide to fine-tuning Whisper for multilingual ASR with Transformers — the standard starting point for Whisper adaptation. *(terms vary — see notes)*
- [SLAM-LLM](https://github.com/X-LANCE/SLAM-LLM) — The canonical implementation of the SLAM-ASR recipe: an encoder-adapter-LLM design that wires speech encoders into frozen LLMs for strong ASR. Paper: arXiv 2402.08846. *(MIT · ⭐ 1,066)*

## Diarization

“Who spoke when” — speaker segmentation and attribution for multi-speaker audio. (3 entries)

- [pyannote.audio](https://github.com/pyannote/pyannote-audio) — The standard open-source neural speaker diarization toolkit, currently v4. Code is MIT; the pretrained segmentation/embedding pipelines on Hugging Face are gated under custom terms, so check before commercial use. *(MIT · ⭐ 10,607)*
- [WeSpeaker](https://github.com/wenet-e2e/wespeaker) — WeNet's speaker verification and diarization toolkit with pretrained models for embeddings, VAD and clustering pipelines. *(Apache-2.0 · ⭐ 1,426)*
- [3D-Speaker](https://github.com/modelscope/3D-Speaker) — ModelScope's speaker toolkit for diarization, verification and multi-speaker ASR, supporting multi-device and multi-channel scenarios. *(Apache-2.0 · ⭐ 3,160)*

## Post-Processing

Punctuation restoration and forced alignment to turn raw transcripts into usable text. (3 entries)

- [deep-multilingual-punctuation](https://github.com/oliverguhr/deepmultilingualpunctuation) — Python library that restores punctuation and sentence segmentation to raw ASR transcripts (English, German, French, Italian), built on the FullStop model for spoken language. *(MIT · ⭐ 170)*
- [Montreal Forced Aligner](https://github.com/MontrealCorpusTools/Montreal-Forced-Aligner) — The standard open-source forced aligner, producing word- and phone-level timestamps needed for subtitling and ASR postprocessing. *(MIT · ⭐ 1,898)*
- [aeneas](https://github.com/readbeyond/aeneas) — Forced aligner focused on synchronizing audio with text to generate subtitles and audio-book timings; widely used in ASR postprocessing pipelines. Note the AGPL license. *(AGPL-3.0 · ⭐ 2,868)*

## Notable exclusions

Projects that look relevant but were deliberately left out, with evidence:

| Project | Why excluded |
|---|---|
| Otter.ai | Meeting-transcription product; no developer speech-to-text API. |
| Descript | Podcast/video editor product, not a standalone transcription API. |
| Murf | TTS-first voice platform; transcription is not a core offering. |
| Coqui STT | Dormant since March 2024 (company shut down); not an active project. |
| whisper-jax | Dormant since April 2024; maintainers describe it as effectively archived. |
| fairseq | Archived (read-only) September 2026; wav2vec2 coverage goes through Hugging Face checkpoints. |
| NVIDIA Riva | Core server is proprietary (NGC); the open checkpoints (Parakeet, FastConformer) are listed instead. |
| Picovoice Leopard | Proprietary on-device SDK with a free tier, not open source. |
| whisper.spm / SwiftWhisper | Stale since May 2024; superseded by WhisperKit. |
| SPGISpeech | Restrictive user agreement (research/internal only, no redistribution). |
| Kimi-Audio / MiniCPM-o / Step-Audio / GLM-ASR / Baichuan-Audio | Existence or license terms unconfirmable on official sources as of 2026-09-30; held back rather than listed on rumor. |
| Whisper small/base as standalone entries | Folded into Whisper / whisper.cpp (same upstream checkpoints; separate entries would be padding). |
| Speechmatics Flow | Voice-agent product built on Agent STT, not a speech-to-text model itself. |
| YAMNet / AudioSet | Audio classification, not speech-to-text. |
| Apple Speech framework | Platform API, not a listable project. |

## Related

More curated lists from [Awesome-llms-labs](https://github.com/Awesome-llms-labs):

- [Awesome-llm-tts](https://github.com/Awesome-llms-labs/Awesome-llm-tts) — LLM-era text-to-speech, the synthesis sibling of this recognition list.
- [awesome-AI-agent-orchestration](https://github.com/Awesome-llms-labs/awesome-AI-agent-orchestration) — AI agent orchestration frameworks and platforms (voice agents build on STT).
- [awesome-oss-macos](https://github.com/Awesome-llms-labs/awesome-oss-macos) — open-source macOS applications.
- [awesome-startup-credits](https://github.com/Awesome-llms-labs/awesome-startup-credits) — startup credit programs (many STT APIs offer startup tiers).

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) — entries must be real, verified on official sources, and honestly licensed. No invented licenses, star counts, or benchmark numbers.

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

This list is released under the [MIT License](LICENSE). The projects listed keep their own licenses, noted per entry.
