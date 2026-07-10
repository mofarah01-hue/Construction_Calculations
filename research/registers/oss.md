# oss.md

Every open source project, model, and library evaluated, per framework section 9. EXACT SPDX license. Where the license was read directly from the LICENSE file it is marked "read from file"; where inferred from a model card, README, or secondary source it is flagged as an open item. Deduplicated across shared_llm_layer, A Phase 4, B Phase 2, B Phase 3.

Columns: Name | Repo / source | SPDX license | License read from file? | Maintenance / last commit | Commercial use permitted? | Runtime / hardware | Does | Does not | Integration effort | Selected/rejected | Source phase

## Language models (edge and RAG)

| Name | Repo / source | SPDX license | Read from file? | Maintenance | Commercial? | Runtime / hardware | Does | Does not | Integration effort | Selected/rejected | Source phase |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Qwen3 (0.6B/1.7B/4B) | huggingface.co/Qwen | `Apache-2.0` | NO (HF fetch 403, from search) | Active | YES, unrestricted | llama.cpp/Ollama; ~3 GB Q4 | Edge narration/chat, tool calls | Frontier reasoning | Low-medium | CANDIDATE (edge assistant) | Shared LLM, A P4 |
| Phi-4-mini (3.8B) | Microsoft | `MIT` | NO (from search) | Active | YES, unrestricted | llama.cpp/Ollama; ~3 GB Q4 | Best small reasoner at 8 GB | Multimodal/vision | Low-medium | CANDIDATE (edge assistant) | Shared LLM, A P4 |
| Gemma 3 (1B/4B) | Google | `LicenseRef-Gemma-Terms-of-Use` (custom, non-standard) | NO (custom license, not read) | Active | YES with prohibited-use clause | llama.cpp/Ollama; ~4.2 GB Q4 (4B) | Multimodal, 140+ langs | Unrestricted use | Medium | FLAGGED (custom restrictions, verify before ship) | Shared LLM |
| Llama 3.2 (1B/3B text) | Meta | `LicenseRef-Llama-3.2-Community-License` (custom, non-standard) | NO (from search) | Active | YES if <700M MAU | llama.cpp/Ollama; ~4-11 GB | On-device text gen, tool calls | EU multimodal | Medium | FLAGGED (MAU cap, custom license) | Shared LLM |
| Mistral Small (24B) | Mistral | `Apache-2.0` | NO (size cross-check only) | Active | YES | vLLM/llama.cpp; >14 GB | Edge-server reasoning | Handset deployment | Medium | REJECTED (too large for handset) | Shared LLM |
| llama.cpp | github.com/ggml-org/llama.cpp | `MIT` | NO (repo metadata) | Active | YES | CPU/GPU/ARM | Edge inference engine | Managed hosting | Low | SELECTED (edge runtime) | Shared LLM, B P3 |
| Ollama | ollama.com | `MIT` | NO (repo metadata) | Active | YES | wraps llama.cpp | Packaging/serving | New inference backend | Low | SELECTED (edge packaging) | Shared LLM |

Note (B P3): V1 grounded generation for Concept B runs on the cloud API tier (Claude Haiku 4.5), so an edge model is not a V1 dependency for Concept B; the above are recorded for the shared spine and Concept A edge assistant.

## Pose, detection, and biomechanics (Concept A vision)

| Name | Repo / source | SPDX license | Read from file? | Maintenance | Commercial? | Runtime / hardware | Does | Does not | Integration effort | Selected/rejected | Source phase |
|---|---|---|---|---|---|---|---|---|---|---|---|
| MoveNet | Google (TF Hub / Kaggle) | `Apache-2.0` | NO (model card) | Active | YES, unrestricted | TFLite/ONNX; any silicon incl. IMX500/Hailo/Rockchip | Fast single-person pose, edge | Multi-person crowd, 3D | Low | SELECTED (recommended pose backbone) | A P4 |
| MediaPipe BlazePose | Google | `Apache-2.0` | YES (read from file) | Active | YES, unrestricted | TFLite/MediaPipe; mobile/edge | 33 3D landmarks on device | Heavy multi-person | Low | CANDIDATE (clean, usable) | A P4 |
| RTMPose / RTMO (MMPose) | OpenMMLab | `Apache-2.0` | YES (read from file) | Active | YES, unrestricted | ONNX/TensorRT/ncnn/OpenVINO; any silicon | SOTA accuracy per compute, real time | n/a | Medium | SELECTED (alt pose backbone) | A P4 |
| ViTPose | ViTAE-Transformer | `Apache-2.0` | YES (read from file) | Active | YES, unrestricted | PyTorch/ONNX; GPU leaning | Highest accuracy class | Cheap edge | High | CANDIDATE (accuracy ceiling, GPU) | A P4 |
| YOLO-Pose (YOLOv8/11-pose) | Ultralytics | `AGPL-3.0` | YES (read from file) | Active | NO without paid Enterprise License (~$5k/yr reported, unverified) | ONNX/TensorRT/TFLite; any silicon | Strong pose + detect | Closed-source use without paying | Low | REJECTED (AGPL copyleft; avoid via MoveNet/RTMPose) | A P4 |
| OpenPose | CMU | Custom CMU non-commercial | YES (read from file) | Legacy | NO, prohibited (separate CMU license required) | CUDA leaning | Multi-person 2D pose | Any commercial use | n/a | REJECTED (non-commercial, unusable as shipped) | A P4 |
| BodyPoseNet / BodyPose3DNet / TRTPose | NVIDIA | NVIDIA model/NGC license | model card | Active | YES (model) but runtime NVIDIA-only | TensorRT/DeepStream; Jetson/NVIDIA GPU only | Commercial pose on NVIDIA | Run off NVIDIA silicon | Medium | REJECTED (locks silicon to Jetson; contradicts IMX500) | A P4 |
| Grounding DINO | IDEA-Research | `Apache-2.0` | YES (read from file) | Active | YES | PyTorch/ONNX; GPU/strong NPU | Open-vocabulary detection | Edge on a camera SoC | High | CANDIDATE (scene memory, v2 only) | A P4 |
| OWL-ViT | Google Research | `Apache-2.0` | NO (model card/repo metadata) | Active | YES | HF/Scenic; GPU | Open-vocabulary detection | Edge | High | CANDIDATE (v2) | A P4 |
| Detic | Meta | Code `Apache-2.0`; some weights inherit ImageNet-21K non-commercial | YES code (read from file); weights caveat | Active | Code YES; check weights per checkpoint | GPU | Large-vocabulary detection | Ship ImageNet-21K weights commercially | High | FLAGGED (weight license caveat; v2 only) | A P4 |
| YOLO-World | Tencent AILab | `GPL-3.0` | YES (read from file) | Active | NO in closed source (copyleft) | ONNX; edge capable | Real-time open-vocab detection | Proprietary product without source disclosure | Medium | REJECTED (GPL copyleft) | A P4 |
| OpenCap | Stanford | `Apache-2.0` class (open source) | NO | Active | YES | 2 cameras + cloud | Reference biomech/gait validation | Single-node edge runtime | High | REFERENCE only (validation, not v1 runtime) | A P4 |

## Speech, wake word, STT (Concept A assistant)

| Name | Repo / source | SPDX license | Read from file? | Maintenance | Commercial? | Runtime / hardware | Does | Does not | Integration effort | Selected/rejected | Source phase |
|---|---|---|---|---|---|---|---|---|---|---|---|
| openWakeWord | dscripka | Code `Apache-2.0`; bundled models `CC-BY-NC-SA-4.0` | YES (read from file) | Active | Code YES; models NO (retrain required) | On device | Wake word framework | Ship bundled models commercially | Medium | FLAGGED (retrain models to ship) | A P4 |
| Picovoice Porcupine | Picovoice | Repo `Apache-2.0`; production custom keywords paid | model card/site | Active | Paid for production custom keywords | On device | Enterprise wake word | Free custom production keywords | Low | CANDIDATE (paid path) | A P4 |
| whisper.cpp (+ Whisper weights) | ggml-org / OpenAI | `MIT` | NO (repo metadata) | Active | YES | CPU/Metal/CUDA/Vulkan; ARM/Pi | On-device STT | Real time on tiny MCU | Low | SELECTED (on-device STT) | A P4 |
| Vosk | Alphacephei | `Apache-2.0` | YES (COPYING read from file) | Active | YES | Kaldi; CPU/Pi/mobile/embedded | Low-latency streaming STT | High accuracy on noisy/accented | Low | CANDIDATE (streaming STT) | A P4 |
| Moonshine | Moonshine AI | Code `MIT`; English models `MIT`; non-English Community License (non-comm <$1M) | YES (read from file) | Active | English YES; non-English gated | Python/iOS/Android/Pi/MCU | Low-latency STT | Non-English commercial without registration | Low | CANDIDATE (English STT clean) | A P4 |

## Data / storage / retrieval (Concept B architecture)

| Name | Repo / source | SPDX license | Read from file? | Maintenance | Commercial? | Runtime / hardware | Does | Does not | Integration effort | Selected/rejected | Source phase |
|---|---|---|---|---|---|---|---|---|---|---|---|
| pgvector | github.com/pgvector/pgvector | `PostgreSQL` (permissive; verify from file) | NO (Open Question) | Active | YES | PostgreSQL extension | Vector similarity search + HNSW for RAG corpus | Large corpus > ~1M vectors efficiently | Low | SELECTED (sufficient under ~1M vectors) | B P3 |
| SQLCipher (community edition) | github.com/sqlcipher/sqlcipher | `BSD-3-Clause` (community; verify from file; commercial edition exists) | NO (Open Question) | Active | YES (community edition) | Mobile client | AES-256 full-database-file encryption for sensitive tier | n/a | Low-medium | SELECTED (client-side sensitive tier) | B P3 |
| React Native | github.com/facebook/react-native | `MIT` | NO (not read from file) | Active | YES | Cross-platform mobile | Cross-platform client | HIPAA compliance alone | Medium | CANDIDATE (RN vs Flutter is a hiring decision) | B P3 |
| Metriport | metriport.com/medical | UNKNOWN (open source; SPDX not read) | NO (Open Question) | Active | UNKNOWN pending license read | Cloud FHIR API | Open-source FHIR API, lab notifications | Not adopted as dependency this phase | UNKNOWN | FLAGGED (read license before adoption) | B P2 |
</content>
