# Glossary

Speech-recognition terms used across this list. Last reviewed 2026-09-30.

- **ASR (Automatic Speech Recognition)** — converting spoken audio into text. "STT" (speech-to-text) is the same thing.
- **WER (Word Error Rate)** — the standard ASR accuracy metric: (substitutions + insertions + deletions) / words in the reference. Lower is better.
- **CER (Character Error Rate)** — like WER but per character; the meaningful metric for languages without word boundaries (Chinese, Japanese).
- **Encoder-decoder** — architecture (e.g., Whisper) with an audio encoder and an autoregressive text decoder. Accurate, but inherently sequential/slower.
- **Transducer (RNN-T / TDT)** — streaming-friendly architecture that emits tokens as audio arrives (e.g., Parakeet). TDT (Token-and-Duration Transducer) is NVIDIA's duration-modeling variant.
- **CTC (Connectionist Temporal Classification)** — non-autoregressive decoding: fast, parallel, slightly less accurate than attention-based decoding (e.g., Parakeet CTC 0.6B, FastConformer-CTC).
- **VAD (Voice Activity Detection)** — detecting which parts of audio contain speech; used to segment long audio before transcription (WhisperX, Silero VAD).
- **Diarization** — "who spoke when": segmenting audio by speaker (pyannote.audio, WeSpeaker).
- **Forced alignment** — aligning a known transcript to audio to get word/phone timestamps (Montreal Forced Aligner, aeneas, WhisperX's wav2vec2 aligner).
- **Streaming / online ASR** — emitting partial transcripts with low latency while audio is still arriving. Contrast **offline/batch** (whole file first).
- **Realtime factor (RTF)** — processing time divided by audio duration. RTF < 1 means faster than real time.
- **Distillation** — training a small "student" model to mimic a large "teacher" (Distil-Whisper, whisper-large-v3-turbo).
- **Quantization** — shrinking a model to lower precision (e.g., int8) for faster/cheaper inference, usually with small accuracy cost (whisper.cpp's ggml formats).
- **Fine-tuning** — continuing training of a pretrained model on your own data/domain.
- **LoRA / QLoRA** — parameter-efficient fine-tuning: train small adapter matrices instead of the whole model.
- **Self-supervised pretraining** — learning speech representations from unlabeled audio (wav2vec 2.0, XLS-R, MMS).
- **E2E (end-to-end)** — a single neural model mapping audio directly to text, replacing the old acoustic-model + pronunciation + language-model pipeline (Kaldi is the classic non-E2E toolkit).
- **Punctuation restoration** — adding punctuation/casing to raw lowercase ASR output (deep-multilingual-punctuation).
- **Code-switching** — mixing languages mid-utterance (e.g., Singlish); a known hard case for ASR.
- **Audio LLM** — a multimodal LLM that ingests audio directly (GPT-4o audio, Qwen3-Omni, Ultravox) instead of relying on a separate ASR stage.
- **TTS (text-to-speech)** — the reverse direction (text → audio). Out of scope for this list except where a project does both.
- **SPDX** — the standard short identifier for open-source licenses (e.g., `MIT`, `Apache-2.0`) used in `data/asr.json`.
- **Copyleft** — licenses (GPL, AGPL) requiring derivative works to stay open; AGPL additionally triggers on network use.
