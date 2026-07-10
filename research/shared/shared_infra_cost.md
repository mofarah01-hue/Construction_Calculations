# shared_infra_cost.md
## Cloud and Inference Infrastructure Cost per User per Month

Governed by `00_framework.md` (sections 4, 5, 8). Scope: recurring cloud and model inference cost to operate the shared technical spine (passive sensing plus fusion plus language model interpretation) for one active subscriber, at three scale tiers. Hardware BOM, NRE, and headcount are out of scope and live in the concept briefs. Cross references the LLM interpretation layer workload (`shared_llm_layer.md`, not yet produced; the inference assumptions below are provisional and must reconcile with it when it lands).

Prices are US list (us-east-1 or provider default region) unless marked. Committed use, savings plans, and enterprise discounts are noted separately and not applied to the headline bands. Date of pricing: 2026-07-10.

---

## 1. Scale tiers and representative user counts

| Tier | Definition | Modeled active users | Rationale |
|------|-----------|----------------------|-----------|
| Small | Hundreds | 300 | G4 pilot to early G5. Fixed platform overhead dominates. |
| Mid | Thousands | 5,000 | G5 limited commercial. Overhead amortizing, variable cost visible. |
| Large | Tens of thousands or more | 50,000 | G6. Variable cost, principally inference, dominates. |

Representative counts are used only to amortize fixed overhead. Variable per user cost is near constant across tiers with a small volume discount at large scale.

---

## 2. The two architectures being compared

| | Concept A (edge heavy) | Concept B (pure cloud SaaS) |
|--|------------------------|------------------------------|
| Vision and sensing inference | On device or on an in home hub. Only derived metrics and events reach the cloud. | Not applicable. Ingests derived metrics from a consumer wearable API; no raw video. |
| Cloud role | Store derived time series, generate caregiver reports, serve on demand conversational queries, push notifications. | Full application. Wearable ingest, rules engine, daily language model generation, retrieval, chat, content delivery. |
| Video or raw sensor egress to cloud | None (metadata only). | None (derived wearable metrics only). |
| Language model call pattern | On demand (caregiver asks, resident check in) plus one daily digest. | Daily generation for every active user plus interactive chat. |

The material cloud infrastructure consequence: Concept A moves continuous vision inference off the cloud bill and onto device COGS. A pure cloud variant of Concept A would carry a continuous GPU video analysis cost that is an order of magnitude above anything in this document, which is the entire economic argument for the edge architecture. The comparison below is cloud infrastructure only and therefore understates Concept A's structural advantage on the sensing layer; the offset is device hardware, costed in the Concept A BOM.

---

## 3. Unit price reference (sourced)

| Line | Service | Unit | List price | Confidence | Source |
|------|---------|------|-----------|-----------|--------|
| Compute | AWS Fargate vCPU | vCPU-hour | $0.04048 | HIGH | AWS Fargate pricing page |
| Compute | AWS Fargate memory | GB-hour | $0.004445 | HIGH | AWS Fargate pricing page |
| Storage | Amazon S3 Standard | GB-month (first 50 TB) | $0.023 | HIGH | AWS S3 pricing page |
| Storage | Cloudflare R2 | GB-month | $0.015 | HIGH | Cloudflare R2 pricing docs |
| Bandwidth | AWS data transfer out to internet | GB (first 10 TB, after 100 GB free) | $0.09 | HIGH | AWS S3 pricing page |
| Bandwidth | Cloudflare R2 and Workers egress | GB | $0.00 (zero egress) | HIGH | Cloudflare R2 pricing docs |
| Database | DynamoDB write (standard) | per 1M WRU | $1.25 | HIGH | AWS DynamoDB pricing page (post 2024-11 50 percent cut) |
| Database | DynamoDB read (eventually consistent) | per 1M RRU | $0.125 | HIGH | AWS DynamoDB pricing page |
| Database | Aurora Serverless v2 | ACU-hour | $0.12 | HIGH | AWS Aurora pricing page |
| Edge requests | Cloudflare Workers paid | per 1M requests after included 10M | $0.30 (plus $5 per month base) | HIGH | Cloudflare Workers pricing docs |
| Inference | Claude Haiku 4.5 | per 1M tokens in / out | $1.00 / $5.00 | HIGH | Anthropic pricing (skill catalog, cached 2026-06-24) |
| Inference | Claude Sonnet 5 | per 1M tokens in / out | $3.00 / $15.00 (intro $2.00 / $10.00 through 2026-08-31) | HIGH | Anthropic pricing (skill catalog, cached 2026-06-24) |
| Inference | Claude Opus 4.8 | per 1M tokens in / out | $5.00 / $25.00 | HIGH | Anthropic pricing (skill catalog, cached 2026-06-24) |
| Inference | Google Gemini 2.5 Flash | per 1M tokens in / out | $0.30 / $2.50 | MEDIUM | Google Gemini API pricing page (July 2026; newer Flash tiers may supersede) |
| Inference | Prompt cache read multiplier | vs base input | approx 0.1x | HIGH | Anthropic prompt caching docs |

Committed use options that reduce the above: DynamoDB and Aurora Database Savings Plans (up to ~35 percent, 1 year commitment); Fargate Compute Savings Plans; Anthropic Batch API (50 percent off, applicable to non interactive daily generation). None are applied to headline bands; all are upside at mid and large tiers.

---

## 4. Per user workload assumptions

All figures are founder and analyst assumptions pending validation against `shared_llm_layer.md`. Stated explicitly per framework section 5.

| Assumption | Concept A | Concept B |
|-----------|-----------|-----------|
| Backend requests per user per month | approx 10,000 (derived metric ingest batched every 5 min plus app usage) | approx 5,000 (hourly wearable sync plus interactive app) |
| Stored data per user (cumulative steady state) | approx 1 GB (derived metric time series, events, reports, occasional event thumbnails; no video) | approx 0.5 GB (wearable metrics, self report logs, chat history, generated content, labs, profile) |
| Egress per user per month | approx 50 to 200 MB (charts, reports, notifications) | approx 200 to 500 MB (content, images, chat) |
| Language model turns per user per month | approx 30 digests plus approx 30 on demand queries | approx 30 daily briefs plus approx 50 chat turns plus 4 weekly summaries |
| Inference tokens per user per month (effective, cache aware) | approx 270K input (approx 180K cached), approx 30K output | approx 462K input (approx 290K cached), approx 57K output |

Retrieval corpus for Concept B (RAG knowledge base) is shared, not per user, and sits in fixed overhead.

---

## 5. Variable cost per user per month (excludes fixed overhead)

Computed from sections 3 and 4. Inference shown as a band across model choice (Haiku 4.5 low end, Sonnet 5 high end), with prompt caching applied to the cached input share.

### Concept A (edge heavy)

| Component | Cost per user per month | Notes |
|-----------|------------------------|-------|
| Compute (Fargate) | approx $0.01 to $0.05 | 10K requests at approx 200 ms, 0.25 vCPU / 0.5 GB |
| Storage (S3 or R2) | approx $0.02 to $0.03 | 1 GB |
| Bandwidth | approx $0.00 to $0.02 | $0.00 on Cloudflare, up to $0.018 on AWS egress |
| Database (DynamoDB) | approx $0.02 to $0.05 | 10K writes plus 20K reads plus small storage |
| Model inference | approx $0.25 to $0.90 | Haiku $0.25 to $0.30; Sonnet $0.55 to $0.80 |
| **Variable subtotal** | **approx $0.40 to $1.10** | Inference is 65 to 85 percent of variable cost |

### Concept B (pure cloud SaaS)

| Component | Cost per user per month | Notes |
|-----------|------------------------|-------|
| Compute (Fargate) | approx $0.01 to $0.05 | 5K requests, interactive |
| Storage (S3 or R2) | approx $0.01 to $0.02 | 0.5 GB |
| Bandwidth | approx $0.00 to $0.05 | $0.00 on Cloudflare, up to $0.045 on AWS egress |
| Database (DynamoDB) | approx $0.02 to $0.08 | mixed write and read |
| Model inference | approx $0.50 to $1.60 | Haiku $0.50; Sonnet 5 $1.00 to $1.50 |
| **Variable subtotal** | **approx $0.65 to $2.70** | Daily generation for every user is the driver |

---

## 6. Fixed platform overhead (amortized per user)

Fixed overhead is the always on cost of running a production platform regardless of user count. It is the single largest swing factor at small scale and the biggest estimation risk in this document. Cloud primitive prices are sourced; third party SaaS tool prices (observability, identity, communications, error tracking) are engineering estimates and are flagged as such. See Open Questions.

| Component | Small tier per month | Large tier per month | Basis |
|-----------|---------------------|----------------------|-------|
| Baseline compute (load balancer, NAT gateway, minimum always on tasks) | $150 to $400 | $800 to $2,000 | AWS primitives, multi AZ at scale (estimate) |
| Managed database baseline (Aurora Serverless v2 floor or DynamoDB provisioned floor) | $175 to $700 | $1,500 to $5,000 | Aurora ACU-hour sourced; sizing estimated |
| Observability and monitoring (Datadog, Grafana Cloud class) | $300 to $1,500 | $2,000 to $6,000 | Estimate, not quoted |
| Identity and auth (Cognito, Auth0 class) | $100 to $800 | $1,000 to $4,000 | Estimate, not quoted |
| Push, SMS, email (FCM, Twilio, SES) | $50 to $500 | $500 to $3,000 | Estimate; volume dependent |
| Error tracking, CI/CD, secrets, WAF, DNS, backups | $200 to $1,000 | $1,000 to $3,000 | Estimate, not quoted |
| **Fixed overhead total** | **approx $1,000 to $5,000** | **approx $7,000 to $23,000** | |
| **Amortized per user** | **$3.30 to $16.70** (at 300 users) | **$0.14 to $0.46** (at 50,000 users) | |

At mid tier (5,000 users) fixed overhead runs approximately $3,000 to $10,000 per month, or $0.60 to $2.00 per user.

Fixed overhead grows sublinearly with scale (redundancy, larger database floor, more observability seats) while per user amortization falls faster. This is why per user cost collapses from tens of dollars to under a dollar between small and large tiers.

---

## 7. Total cost per user per month (variable plus amortized fixed)

| Tier | Concept A (edge heavy) | Concept B (pure cloud SaaS) | Dominant driver |
|------|------------------------|------------------------------|-----------------|
| Small (300 users) | **$7 to $17** | **$7 to $19** | Amortized fixed overhead |
| Mid (5,000 users) | **$1.00 to $3.00** | **$1.50 to $4.50** | Fixed overhead and inference in balance |
| Large (50,000 users) | **$0.50 to $1.50** | **$1.00 to $3.00** | Model inference |

Reading: at small scale, cloud infrastructure cost per user is set almost entirely by how much fixed platform you stand up, not by the product. The two concepts are indistinguishable there. The concept level delta only emerges at mid and large scale, where inference volume separates them.

---

## 8. Delta: edge heavy (A) versus pure cloud (B)

| Dimension | Direction | Magnitude at large tier |
|-----------|-----------|-------------------------|
| Sensing and vision inference | A far cheaper on cloud | A runs vision on device; B has no vision. A pure cloud vision variant would add continuous GPU cost of an order of magnitude more than the entire table above. This is the decisive structural difference and it is hidden because A pays it in hardware COGS, not cloud. |
| Language model inference | A cheaper | A queries on demand plus one daily digest; B generates daily for every user plus chat. B carries roughly $0.50 to $1.50 more per user per month on inference. |
| Storage | A slightly higher | A retains more derived time series; B retains chat and content. Difference under $0.03 per user. |
| Bandwidth | B slightly higher | Content and image delivery. Difference under $0.05 per user. |
| Fixed overhead | Comparable | Both are production SaaS backends. A adds device fleet telemetry and firmware update distribution; B adds a shared retrieval corpus. Roughly offsetting. |
| Net cloud infrastructure delta | A cheaper by approx $0.50 to $1.50 per user per month at scale | Driven by inference call pattern and the absence of any cloud vision path. |

Strategic note for the business case: the edge architecture's cloud saving is real but modest in absolute cloud dollars. Its true value is that it caps the marginal cloud cost of continuous sensing near zero and converts it into a one time device cost, which is what makes a low priced consumer subscription viable. Concept B has no such hidden GPU liability because it never processes video, so its cloud bill, while higher per user on inference, is fully visible and fully bounded.

---

## Register Entries

Sources consulted (also to be appended to `research/registers/sources.md` by the register owner; this file does not edit the registers).

| Source | Publisher | URL | Pub / access date | Used for | Credibility |
|--------|-----------|-----|-------------------|----------|-------------|
| AWS Fargate pricing | Amazon | https://aws.amazon.com/fargate/pricing/ | Accessed 2026-07-10 | vCPU and memory hourly rates | HIGH (primary) |
| Amazon S3 pricing | Amazon | https://aws.amazon.com/s3/pricing/ | Accessed 2026-07-10 | Storage per GB, egress per GB | HIGH (primary) |
| Amazon DynamoDB pricing (on demand) | Amazon | https://aws.amazon.com/dynamodb/pricing/on-demand/ | Accessed 2026-07-10 | Write and read request unit prices | HIGH (primary) |
| Amazon Aurora pricing | Amazon | https://aws.amazon.com/rds/aurora/pricing/ | Accessed 2026-07-10 | Aurora Serverless v2 ACU-hour | HIGH (primary) |
| Cloudflare R2 pricing | Cloudflare | https://developers.cloudflare.com/r2/pricing/ | Accessed 2026-07-10 | Storage, zero egress, operation classes | HIGH (primary) |
| Cloudflare Workers pricing | Cloudflare | https://developers.cloudflare.com/workers/platform/pricing/ | Accessed 2026-07-10 | Edge request pricing, zero egress | HIGH (primary) |
| Anthropic model pricing | Anthropic | https://platform.claude.com/docs/en/pricing | Skill catalog cached 2026-06-24 | Claude Haiku 4.5, Sonnet 5, Opus 4.8 token prices; prompt cache multiplier | HIGH (primary) |
| Google Gemini API pricing | Google | https://ai.google.dev/gemini-api/docs/pricing | Accessed 2026-07-10 | Gemini 2.5 Flash token prices | MEDIUM (primary, model may be superseded) |

No source is older than 18 months. The Anthropic Sonnet 5 introductory price ($2 / $10) expires 2026-08-31; recompute mid tier and large tier inference at standard $3 / $15 for any plan dated after that.

---

## Open Questions

1. **Fixed platform overhead composition is not fully quoted.** Cloud primitives (Fargate, Aurora, DynamoDB, S3, R2) are sourced. Third party SaaS tools (Datadog or Grafana Cloud, Auth0 or Cognito, Twilio, error tracking, CI/CD) are engineering estimates, not vendor quotes. This is the single largest source of uncertainty in the small tier band. Action: obtain seat and volume quotes at 300, 5,000, and 50,000 user scale for the chosen observability, identity, and communications stack.
2. **Inference token volume per user is unvalidated.** The token assumptions in section 4 come from an assumed call pattern, not from a running system. They must be reconciled with `shared_llm_layer.md` once it exists. A 2x error in tokens moves the large tier band materially because inference dominates there.
3. **Model selection is unresolved.** The bands span Haiku 4.5 to Sonnet 5, a 3x swing. The framework guidance for Concept B (rules engine plus language model for presentation only) argues for the cheaper tier, but this is a product decision with quality consequences, not yet made. Gemini 2.5 Flash and Batch API pricing are open cost reduction levers.
4. **Wearable API ingest cost (Concept B) is not included here.** Some vendor APIs meter access or require paid tiers. That cost belongs to `shared_wearable_data_access.md` and must be added to the Concept B per user figure once known.
5. **Data residency, HIPAA eligible service premiums, and encryption or key management (KMS) costs are not modeled.** If the privacy architecture (`shared_privacy_security.md`) forces HIPAA eligible configurations, dedicated tenancy, or per user encryption keys, add a premium. Currently UNKNOWN.
6. **Egress region and CDN strategy unmodeled at scale.** The bands assume Cloudflare zero egress as the low end and AWS egress as the high end. A committed AWS architecture without a zero egress CDN would raise the bandwidth line at large tier.

---

## Assumptions Made

1. Representative user counts (300, 5,000, 50,000) are chosen to amortize fixed overhead. If actual cohort sizes differ, re amortize. Impact if wrong: small tier per user cost is highly sensitive to the exact user count (inverse linear); mid and large are not.
2. Both concepts send no raw video or raw sensor stream to the cloud. This is a founder assumption inherited from the concept descriptions and is load bearing. If Concept A must send video to the cloud for any feature, the entire cost model breaks and a GPU inference line must be added. Impact if wrong: catastrophic to the Concept A economics.
3. Per user storage is steady state cumulative, not monthly incremental. Assumes a retention policy that caps growth. Without a retention policy, storage grows unbounded and the storage line rises over the subscriber lifetime.
4. Prompt caching is available and effective, cutting cached input to approximately 0.1x. Assumes a stable system prompt and shared corpus prefix. If the prompt design defeats caching, inference input cost rises up to 10x on the cached share.
5. Compute is modeled as serverless containers (Fargate). A provisioned always on fleet would move cost from variable into fixed overhead but not change the total materially at mid and large tiers.
6. Fixed overhead scales sublinearly and per user cost therefore collapses with scale. Assumes competent capacity management, not overprovisioning. A naive always on overprovisioned stack would flatten the curve and keep per user cost high.
7. The Concept A cloud figure explicitly excludes the on device or hub compute that performs vision inference. That cost is device COGS in the Concept A BOM, not cloud infrastructure. Comparing cloud bills alone favors A and must not be read as total cost of ownership.

---

## Confidence Summary

Overall confidence: MEDIUM.

Strongest (HIGH): the sourced cloud primitive and model token prices in section 3. These are current primary source list prices.

Moderate (MEDIUM): the variable per user cost in section 5, which depends on assumed workload volumes that are internally consistent but unvalidated against a running system.

Weakest (LOW to MEDIUM): the fixed platform overhead in section 6, because the third party SaaS component is estimated rather than quoted, and it is precisely this line that dominates the small tier headline number. The small tier band ($7 to $19 per user) should be treated as indicative until the SaaS stack is quoted. The mid and large tier bands are firmer because variable cost, built on sourced unit prices, carries more of the total there.

The headline conclusion, that per user cloud cost falls from double digit dollars at small scale to roughly $0.50 to $3.00 at large scale, with model inference as the terminal cost driver and the edge architecture holding a modest but structurally important advantage, is robust to the estimation weaknesses above.
