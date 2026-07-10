# shared_llm_layer.md
## LLM Interpretation Layer Decision

Scope: the language model layer that turns fused sensor features into care context (daily digests, anomaly narration, education, conversational assistant, safety escalation phrasing) for Concept A (Elder Home Monitoring) and Concept B (Pregnancy and Parenting Companion). Conventions inherited from `00_framework.md`. Prices verified 2026-07-10.

---

## 1. On Device vs API Tradeoff

| Dimension | On device (edge) | API (cloud) | Which wins |
|-----------|------------------|-------------|------------|
| Marginal cost per interaction | ~$0 (electricity, amortized silicon) | $0.0003 to $0.02 per interaction | Edge at scale |
| Data leaving the home | Nothing needs to leave | Prompt payload leaves the device | Edge |
| Reasoning quality / nuance | 1B to 8B class, materially weaker | Frontier class | API |
| Grounding / factual health education | Parametric only unless local RAG built | Retrieval plus frontier model | API |
| Offline / connectivity resilience | Functions with no network | Fails without network | Edge |
| Latency (first token) | 0.3 to 2 s local, no network hop | 0.4 to 2 s plus network round trip | Edge for narration, parity for chat |
| Update cadence / model refresh | Firmware push, per fleet | Instant, provider managed | API |
| Engineering burden | Runtime, quantization, per SoC tuning | Single HTTPS integration | API |
| Regulatory blast radius | Small (no PHI egress) | Large (PHI egress, BAA, state biometric law) | Edge |

Conclusion: the two axes that dominate this product category are privacy blast radius and marginal cost, both of which push edge, set against reasoning quality and grounding, both of which push API. Neither pole is correct alone. See Section 8.

---

## 2. API Model Options and Token Pricing

Interpretation/assistant workload is short context, high frequency: a fused-feature summary plus persona plus retrieved snippet in, a few hundred tokens of narration out. The relevant tier is small-to-mid, not frontier flagship, except for the safety-critical escalation path.

### Claude family (current, primary source, HIGH)

| Model | Model ID | Input $/MTok | Output $/MTok | Cache read $/MTok | Batch in/out $/MTok | Context |
|-------|----------|-------------|---------------|-------------------|---------------------|---------|
| Claude Haiku 4.5 | `claude-haiku-4-5` | 1.00 | 5.00 | 0.10 | 0.50 / 2.50 | 200K |
| Claude Sonnet 5 (intro to 2026-08-31) | `claude-sonnet-5` | 2.00 | 10.00 | 0.20 | 1.00 / 5.00 | 1M |
| Claude Sonnet 5 (from 2026-09-01) | `claude-sonnet-5` | 3.00 | 15.00 | 0.30 | 1.50 / 7.50 | 1M |
| Claude Opus 4.8 | `claude-opus-4-8` | 5.00 | 25.00 | 0.50 | 2.50 / 12.50 | 1M |

Cache read is 0.1x base input; batch is 50 percent off both directions. Source: Anthropic pricing docs, accessed 2026-07-10. Note: Sonnet 5 / Opus 4.7+ use a newer tokenizer that emits ~30 percent more tokens for the same text, which offsets part of the headline per-token advantage. Factor this into any Sonnet-vs-Haiku comparison.

### Alternative 1: OpenAI GPT-5 family (aggregator sources, MEDIUM)

| Model | Input $/MTok | Output $/MTok | Context |
|-------|-------------|---------------|---------|
| GPT-5 Nano | 0.05 | 0.40 | 400K |
| GPT-5 Mini | 0.25 | 2.00 | 400K |
| GPT-5.6 Luna (Jul 2026) | 1.00 | 6.00 | UNKNOWN |

Primary page `developers.openai.com/api/docs/pricing` returned 403 to the fetch tool; figures are from pricing aggregators, accessed 2026-07-10. Confirm against the primary page before any contract commitment.

### Alternative 2: Google Gemini family (aggregator sources, MEDIUM)

| Model | Input $/MTok | Output $/MTok | Context |
|-------|-------------|---------------|---------|
| Gemini 2.5 Flash-Lite | 0.10 | 0.40 | 1M |
| Gemini 2.5 Flash | 0.30 | 2.50 | 1M |
| Gemini 2.5 Pro | 1.25 | 10.00 | 1M |

Primary page `ai.google.dev/gemini-api/docs/pricing` returned 403 to the fetch tool; figures from aggregators, accessed 2026-07-10. A Gemini 3 Flash preview (~$0.50/MTok) is referenced but not confirmed from primary source. Gemini 2.5 models released mid-2025; pricing is current but the model line is over 12 months old, flag as approaching stale.

Read across: for a short-context interpretation workload, the cheap tiers (Nano, Flash-Lite, Haiku) span roughly $0.05 to $1.00 input. Claude Haiku is the most expensive of the cheap tier but is the incumbent with the strongest safety posture and the cache/batch economics above. GPT-5 Nano and Gemini Flash-Lite are 10x to 20x cheaper on raw tokens and are credible for non-safety-critical narration.

---

## 3. On Device Small Model Options

| Model | Sizes for edge | SPDX / license | Commercial | Runtime | RAM (Q4) | Notes |
|-------|----------------|----------------|------------|---------|----------|-------|
| Qwen3 | 0.6B, 1.7B, 4B | `Apache-2.0` (standard SPDX) | Yes, unrestricted | llama.cpp / Ollama | ~3 GB (4B) | Cleanest license; strong coding/reasoning for class |
| Phi-4-mini | 3.8B | `MIT` (standard SPDX) | Yes, unrestricted | llama.cpp / Ollama | ~3 GB | Best small reasoner on 8 GB hardware |
| Mistral Small | 24B (too large for phone) | `Apache-2.0` | Yes | llama.cpp / vLLM | >14 GB | Edge server, not handset |
| Gemma 3 | 1B, 4B | `LicenseRef-Gemma-Terms-of-Use` (custom, NOT OSI/SPDX standard) | Yes with use restrictions | llama.cpp / Ollama | ~4.2 GB (4B) | Prohibited-use clause; multimodal, 140+ languages |
| Llama 3.2 | 1B, 3B (text only) | `LicenseRef-Llama-3.2-Community-License` (custom, NOT OSI/SPDX standard) | Yes if <700M MAU | llama.cpp / Ollama | ~4 to 11 GB (3B) | EU multimodal carve-out does not bind the text-only 1B/3B; 700M MAU cap irrelevant at our scale |

License caveat per framework Section 9: `Apache-2.0` and `MIT` are OSI-approved standard SPDX identifiers and carry no field-of-use restriction. `Gemma` and `Llama 3.2 Community` are vendor custom licenses with no standard SPDX identifier and both include acceptable-use restrictions; they are recorded with the `LicenseRef-` convention and flagged. License text was read from vendor pages via search; direct fetch of the Hugging Face and vendor license files returned 403 and is an open item (see Open Questions).

Runtime: `llama.cpp` (`MIT`) is the de facto edge inference engine; `Ollama` (`MIT`) wraps the same ggml backend for packaging. Both permit commercial redistribution.

Hardware demand (measured, MEDIUM, aggregator benchmarks 2026): 4B Q4 model ~3 GB RAM, 5 to 8 tokens/s on ARM SBC/handset class silicon (Qualcomm/MediaTek/RK3588 class); 30 to 50 tokens/s on a mid desktop GPU. A 4B class model at 5 to 8 tokens/s produces a 100-token narration in 12 to 20 s, acceptable for a scheduled digest, marginal for interactive chat.

---

## 4. Grounding / RAG Posture (Parametric vs Retrieval)

| Output type | Posture | Rationale |
|-------------|---------|-----------|
| Sensor narration ("walking speed down 18 percent this week") | Parametric | The number comes from the fusion layer; the model only phrases it. No retrieval needed. |
| Health education / normalization ("resting heart rate typically rises across pregnancy") | Retrieval (RAG) | FTC substantiation (framework Section 2) requires claims be backed by competent and reliable evidence. Parametric recall is not a citable source. Ground on a vetted content corpus. |
| Safety-critical escalation phrasing | Retrieval plus hard-coded template | Must be deterministic and auditable, not generative improvisation. |
| Conversational Q&A | Hybrid | Retrieve when the answer is factual/medical; parametric for chit-chat. |

Design rule: the interpretation layer must never assert a health fact from parametric memory. Retrieval binds every educational claim to a citable, substantiable source and converts the FTC substantiation question into a content-licensing line item rather than a model-quality gamble. A vetted RAG corpus is portable across both edge and API topologies.

---

## 5. Latency

| Path | First token | Full 100-token narration | Topology push |
|------|-------------|--------------------------|---------------|
| Edge 4B Q4 (ARM class) | 0.3 to 2 s | 12 to 20 s at 5 to 8 tok/s | Edge, no network dependency |
| Edge 4B (desktop GPU class hub) | <0.5 s | 2 to 4 s at 30 to 50 tok/s | Edge, if a hub with a GPU exists |
| API (Claude/GPT/Gemini small tier) | 0.4 to 2 s incl. network | 1 to 4 s streamed | API, when connected |

Interactive chat needs sub-2 s first token; an edge handset-class model meets first-token latency but is slow on throughput, so long outputs feel sluggish. A cloud API streams faster once the network hop is paid. For scheduled/background interpretation, edge latency is a non-issue. Confidence MEDIUM (throughput figures are aggregator benchmarks, not our silicon).

---

## 6. Privacy Posture (What Leaves the Home)

| Topology | What leaves the device | Regulatory trigger |
|----------|------------------------|--------------------|
| Full edge | Nothing. Fused features and narration stay local. | Minimal. No PHI egress, no BAA required for the LLM layer. |
| API, features only | Derived numeric features plus prompt text | State biometric law (BIPA, CUBI, MHMD) if features are biometric identifiers; likely HIPAA BAA if a covered-entity path exists. |
| API, raw context | Any raw sensor context in the prompt | Maximum. Continuous-home-derived data is among the most regulated categories (framework Section 8). |

Framework Section 8 is explicit: "we only send metadata, not video" is a claim the architecture must enforce, not intend. The LLM layer is where that enforcement is tested, because a prompt is the easiest place for raw context to leak into egress. An edge interpretation layer removes the question entirely for routine output. Detailed HIPAA/BIPA analysis is owned by `shared_privacy_security.md`; this file records only that the LLM topology choice is a first-order privacy determinant.

---

## 7. Cost per User per Month

Token assumptions per interaction (one request/response), blended across scheduled digests and conversational turns:

- Input: 2,500 tokens (system/persona + fused-feature summary + retrieved snippet + short history)
- Output: 350 tokens (narration)

Interaction volume tiers per user per month:
- Low: 30 interactions (~1/day)
- Medium: 150 interactions (~5/day)
- High: 600 interactions (~20/day)

Per-interaction cost = (2,500 x input$)/1e6 + (350 x output$)/1e6. Caching and batch discounts NOT applied in the base table (they only reduce API cost further; see note).

| Model | $/interaction | Low (30) | Medium (150) | High (600) |
|-------|--------------|----------|--------------|------------|
| GPT-5 Nano | $0.000265 | $0.008 | $0.040 | $0.16 |
| Gemini 2.5 Flash-Lite | $0.00039 | $0.012 | $0.059 | $0.23 |
| GPT-5 Mini | $0.001325 | $0.040 | $0.20 | $0.80 |
| Gemini 2.5 Flash | $0.001625 | $0.049 | $0.24 | $0.98 |
| Claude Haiku 4.5 | $0.00425 | $0.13 | $0.64 | $2.55 |
| Claude Sonnet 5 (intro) | $0.0085 | $0.26 | $1.28 | $5.10 |
| Claude Opus 4.8 | $0.02125 | $0.64 | $3.19 | $12.75 |
| Edge 4B (Qwen3/Phi-4-mini) | ~$0 marginal | ~$0 | ~$0 | ~$0 |

Caching note (Claude, HIGH): if ~1,500 of the 2,500 input tokens are a stable cached prefix (persona + few-shot + system), those bill at 0.1x, cutting per-interaction input cost roughly in half. Batch API halves both directions for non-interactive scheduled digests. Applied together, Claude Haiku high-volume drops from $2.55 toward ~$1.30 to $1.60 per user per month.

Edge note: marginal cost is electricity only; the real cost is one-time model integration NRE plus the incremental BOM (RAM/NPU) to run a 4B model, both of which belong in the hardware registers, not here. Flag: edge is not free, its cost is capitalized rather than metered.

Bottom line range for the interpretation layer: roughly $0.01 to $3.00 per user per month at medium volume depending on model tier and topology; sub-$1 is readily achievable with a cheap API tier or edge, and only the frontier-on-every-turn choice exceeds $3.

---

## 8. Topology Push by Concept and Recommendation

| Concept lever | Pushes toward |
|---------------|---------------|
| Video/biometric data in the home (privacy) | Edge |
| Real-time anomaly narration (latency) | Edge |
| Offline resilience (elder falls, no wifi) | Edge |
| High interaction volume at scale (cost) | Edge |
| FTC-substantiated health education (grounding) | API + RAG |
| Nuanced multi-signal care reasoning (quality) | API |
| Safety-critical escalation reliability | API + hard-coded template |
| Fast model refresh / iteration velocity | API |

Recommended layer: hybrid, routed by sensitivity and complexity. Run a quantized 4B edge model (`Qwen3-4B`, `Apache-2.0`, or `Phi-4-mini`, `MIT`, both clean licenses) on device for routine narration, always-on availability, and anything touching raw in-home context, keeping that data local. Route complex reasoning, RAG-grounded education, and safety escalation phrasing to a cloud API using a small-to-mid tier (Claude Haiku 4.5 or Sonnet 5 for safety-aligned output; GPT-5 Nano or Gemini Flash-Lite for cost-sensitive non-critical narration). Send only vetted derived features to the API, never raw context. This keeps cost per user per month under ~$1 at medium volume, minimizes PHI egress, and reserves frontier reasoning for the few turns that need it.

---

## Register Entries

### sources

| Title | Org | URL | Pub date | Accessed | Used for | Credibility |
|-------|-----|-----|----------|----------|----------|-------------|
| Pricing (Claude models) | Anthropic | https://platform.claude.com/docs/en/about-claude/pricing | current | 2026-07-10 | Claude token, cache, batch pricing | HIGH (primary) |
| claude-api skill (bundled) | Anthropic | (local skill, cached 2026-06-24) | 2026-06-24 | 2026-07-10 | Claude model IDs, context, pricing cross-check | HIGH (primary) |
| OpenAI API pricing guide 2026 | DevTk.AI | https://devtk.ai/en/blog/openai-api-pricing-guide-2026/ | 2026 | 2026-07-10 | GPT-5 family pricing | MEDIUM (aggregator) |
| OpenAI pricing (July 2026) | AI Pricing Guru | https://www.aipricing.guru/openai-pricing/ | 2026-07 | 2026-07-10 | GPT-5.6 Luna/Terra/Sol pricing | MEDIUM (aggregator) |
| GPT-5 Nano / Mini pricing | pricepertoken.com | https://pricepertoken.com/pricing-page/model/openai-gpt-5-nano | 2026 | 2026-07-10 | Nano/Mini token pricing | MEDIUM (aggregator) |
| Gemini 2.5 Flash pricing | pricepertoken.com | https://pricepertoken.com/pricing-page/model/google-gemini-2.5-flash | 2026 | 2026-07-10 | Gemini Flash/Pro pricing | MEDIUM (aggregator) |
| Gemini 2.5 Flash-Lite pricing | devtk.ai | https://devtk.ai/en/models/gemini-2-5-flash-lite/ | 2026-05 | 2026-07-10 | Flash-Lite token pricing | MEDIUM (aggregator) |
| Best Small Language Models 2026 | BentoML | https://www.bentoml.com/blog/the-best-open-source-small-language-models | 2026 | 2026-07-10 | Edge SLM sizes, RAM, licenses | MEDIUM |
| SLM enterprise edge comparison | Meta-Intelligence | https://www.meta-intelligence.tech/en/insight-slm-enterprise | 2026 | 2026-07-10 | Phi-4/Gemma/Llama license + RAM | MEDIUM |
| Llama 3.2 edge/mobile blog | Meta | https://ai.meta.com/blog/llama-3-2-connect-2024-vision-edge-mobile-devices/ | 2024 | 2026-07-10 | Llama 3.2 1B/3B edge positioning | MEDIUM (vendor, stale >18mo) |
| Llama 3.2 Community License | Meta | https://www.llama.com/llama3_2/license/ | 2024 | 2026-07-10 | Llama license terms | MEDIUM (fetch blocked; from search) |
| llama.cpp repo | ggml-org | https://github.com/ggml-org/llama.cpp | 2026 | 2026-07-10 | Runtime license MIT, tok/s | MEDIUM |
| Running LLMs locally 2026 | daily.dev | https://daily.dev/blog/running-llms-locally-ollama-llama-cpp-self-hosted-ai-developers/ | 2026 | 2026-07-10 | Ollama/llama.cpp edge throughput | MEDIUM |
| Run LLMs on ARM RK3588 | turingpi.com | https://turingpi.com/run-llm-locally-arm-rk3588-ollama-llama-cpp/ | 2026 | 2026-07-10 | ARM tokens/s benchmarks | MEDIUM |

### oss

| Name | Repo/source | SPDX license | Commercial | Runtime/hardware | Does | Does not | Confidence |
|------|-------------|--------------|------------|------------------|------|----------|------------|
| Qwen3 (0.6B/1.7B/4B) | huggingface.co/Qwen | `Apache-2.0` | Yes, unrestricted | llama.cpp/Ollama; ~3 GB Q4 | Edge narration/chat, tool calls | Frontier reasoning | MEDIUM (license from search, HF fetch 403) |
| Phi-4-mini (3.8B) | Microsoft | `MIT` | Yes, unrestricted | llama.cpp/Ollama; ~3 GB Q4 | Best small reasoner @8 GB | Multimodal/vision | MEDIUM |
| Gemma 3 (1B/4B) | Google | `LicenseRef-Gemma-Terms-of-Use` (custom, non-standard) | Yes, with prohibited-use clause | llama.cpp/Ollama; ~4.2 GB Q4 (4B) | Multimodal, 140+ langs | Unrestricted use | MEDIUM (custom license, not read from file) |
| Llama 3.2 (1B/3B text) | Meta | `LicenseRef-Llama-3.2-Community-License` (custom, non-standard) | Yes if <700M MAU | llama.cpp/Ollama; ~4 to 11 GB | On-device text gen, tool calls | EU multimodal (n/a to text 1B/3B) | MEDIUM (license from search) |
| Mistral Small (24B) | Mistral | `Apache-2.0` | Yes | vLLM/llama.cpp; >14 GB | Edge-server reasoning | Handset deployment | LOW (size cross-check only) |
| llama.cpp | github.com/ggml-org/llama.cpp | `MIT` | Yes | CPU/GPU/ARM | Edge inference engine | Managed hosting | MEDIUM |
| Ollama | ollama.com | `MIT` | Yes | wraps llama.cpp | Packaging/serving | New inference backend | MEDIUM |

---

## Open Questions

1. Primary-source pricing for OpenAI (`developers.openai.com/api/docs/pricing`) and Google (`ai.google.dev/gemini-api/docs/pricing`) both returned 403 to the fetch tool. All non-Claude prices are from aggregators and must be confirmed against the primary pages before any commercial commitment. UNKNOWN: exact GPT-5.6 context windows.
2. Exact SPDX/license text for Qwen3, Gemma 3, and Llama 3.2 was not read directly from the license file (Hugging Face and vendor pages returned 403). Framework Section 9 requires reading the license file. This must be closed before any model is selected for shipment.
3. On-device throughput (tokens/s) figures are aggregator benchmarks on generic ARM silicon, not our chosen SoC. Real latency depends on the compute module selected in the hardware phase.
4. RAG corpus for FTC-substantiated health education is unscoped: content source, licensing cost, and update cadence are UNKNOWN and are a real line item (framework Section 2).
5. Whether the elder-monitoring hub carries a GPU/NPU capable of >30 tok/s, or only a handset-class CPU at 5 to 8 tok/s, is a hardware-phase input that determines whether interactive edge chat is viable.

## Assumptions Made

1. Interaction token profile (2,500 in / 350 out) is a founder-level estimate, not measured. If real prompts are larger (more history, larger retrieved context), API cost scales linearly. Impact if wrong: cost table off by the ratio.
2. Volume tiers (30/150/600 per month) are assumed, not derived from a product usage model. Impact: cost per user scales linearly with volume.
3. Caching benefit assumes a ~1,500-token stable cacheable prefix. If the prefix churns per request, the caching discount does not apply.
4. "Edge marginal cost ~$0" ignores capitalized BOM and NRE, which are accounted in the hardware/software registers, not here.
5. Treated the interpretation/assistant workload as small-to-mid tier appropriate; the safety-escalation path is assumed to warrant a higher tier and a hard-coded template rather than free generation.

## Confidence Summary

Overall: MEDIUM-HIGH. Claude pricing and the caching/batch structure are HIGH (primary Anthropic source, current). The recommended hybrid topology and the topology-push analysis are HIGH-confidence reasoning grounded in the framework. Weakest elements: (a) all non-Claude API prices are aggregator-sourced, MEDIUM, pending primary confirmation; (b) open-model licenses were not read from the license file as the framework requires, MEDIUM, and the two custom licenses (Gemma, Llama) carry non-standard restrictions that must be verified before selection; (c) edge throughput/latency figures are generic benchmarks, MEDIUM, and will move with the SoC chosen downstream. The biggest single unknown is the RAG content corpus for substantiable health education, which is unscoped and cross-cuts both concepts.
