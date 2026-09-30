# Choosing an ASR Model

A decision guide for picking speech-to-text in the LLM era. Last reviewed 2026-09-30.

## Start with your constraints

1. **Live or batch?** If you need partial results while the user is still speaking (voice agents, live captions), you need a streaming architecture — see [Streaming & Real-Time ASR](../README.md#streaming--real-time-asr). Chunked offline models (plain Whisper) add seconds of latency.
2. **Budget: $0 or usage-based?** Hosted APIs ([Commercial STT APIs](../README.md#commercial-stt-apis)) win on time-to-value; open models ([Foundation Models](../README.md#foundation-models)) win on marginal cost and data control.
3. **Where does the audio live?** Regulated data, on-device requirements, or offline operation point to [Edge & On-Device](../README.md#edge--on-device) (whisper.cpp, sherpa-onnx, Vosk, Moonshine).
4. **Which languages?** English-only: Parakeet TDT is the open accuracy leader. Multilingual: Whisper large-v3/turbo, Canary, MMS (1,000+ languages, non-commercial). Always check the [Open ASR Leaderboard](https://huggingface.co/spaces/hf-audio/open_asr_leaderboard) for current numbers rather than trusting marketing.

## Accuracy vs. speed vs. cost

- **Best open English accuracy:** NVIDIA Parakeet TDT 0.6B v3 (transducer, non-autoregressive-friendly).
- **Best open multilingual accuracy:** Whisper large-v3; large-v3-turbo keeps ~parity at ~8x speed.
- **Fastest cheap inference:** faster-whisper (CTranslate2) or whisper.cpp (quantized, CPU-friendly).
- **Cheapest at scale:** self-hosted open model. Hosted APIs charge per audio-minute/hour; at high volume the crossover favors self-hosting quickly.
- **Lowest latency live:** purpose-built streaming models/APIs (Deepgram Nova-3/Flux, AssemblyAI realtime, Soniox) or local streaming stacks (whisper_streaming, sherpa-onnx streaming, Silero STT).

## Open vs. API: the honest trade-offs

| | Open models | Hosted APIs |
|---|---|---|
| Data control | Audio never leaves your infra | Audio sent to vendor |
| Cost shape | Fixed GPU cost, ~$0 marginal | Per-minute, scales linearly |
| Customization | Fine-tune on your domain ([guide](https://huggingface.co/blog/fine-tune-whisper)) | Limited to vendor options |
| Ops burden | You serve, scale, monitor | Vendor handles it |
| Extras | DIY | Diarization, punctuation, PII redaction often bundled |

## Licensing traps (read before you ship)

- **CC-BY-NC-4.0 / CC-BY-NC-SA-4.0** (SeamlessM4T, MMS, Silero STT): research/non-commercial only. Not for commercial products.
- **CC-BY-4.0** (Parakeet, Canary, FastConformer weights): commercial OK, but attribution is legally required.
- **AGPL-3.0** (whisper-timestamped, aeneas): network use counts as distribution — strong copyleft.
- **Gated model terms** (pyannote.audio pipelines): code is MIT, but the pretrained diarization models on Hugging Face sit behind custom terms — check before commercial use.
- **Custom/non-OSI licenses** (MERaLiON-AudioLLM): read the actual license text; "public license" ≠ OSI-approved.
- **GigaSpeech**: repo tagged Apache-2.0 but access is restricted to non-commercial research — check terms before training on it.

## Multilingual notes

- Whisper covers 99 languages; quality varies — verify on FLEURS or your target language's Common Voice split.
- MMS covers 1,000+ languages but is non-commercial.
- Code-switching (e.g., Singlish/Manglish) is a specialty niche — MERaLiON-AudioLLM targets it explicitly.
- For domain jargon (medical, legal), fine-tuning beats model-swapping: see [Training & Fine-Tuning](../README.md#training--fine-tuning).

## Diarization, punctuation, timestamps

Raw ASR gives you words. Usable transcripts need:
- **Word timestamps:** WhisperX, whisper-timestamped, Montreal Forced Aligner, aeneas.
- **Speaker labels:** pyannote.audio, WeSpeaker, 3D-Speaker (or vendor diarization add-ons).
- **Punctuation:** deep-multilingual-punctuation, or LLM post-processing (Canary-Qwen has a punctuation mode).

## The LLM-era shortcut

Audio LLMs (GPT-4o audio, Gemini transcription models, Qwen3-Omni, Phi-4-multimodal, Ultravox, Voxtral) skip the separate ASR stage: audio goes straight into the LLM. This shines for speech *understanding* (summaries, Q&A over audio) but is usually pricier per minute than a dedicated ASR model for pure transcription. Evaluate on [AudioBench](https://github.com/AudioLLMs/AudioBench) for understanding tasks and the Open ASR Leaderboard for raw transcription.
