# xAI / Grok Model Inventory

This document catalogs known xAI Grok models, with a focus on technical traits relevant for prompt design and provider-level research.

- Provider: xAI (Grok)
- API base: `https://api.x.ai` (OpenAI-compatible surface; also exposed via X API v2 in some environments)
- Modalities: text, code, vision/multimodal (varies by model family)
- Key dimensions tracked here:
  - Model family and role (reasoning, fast, mini, code, legacy)
  - Context window and output behavior
  - Primary use cases and positioning
  - Research priority (whether this repo will deeply characterize the model)

---

## Legend

- **Family**: High-level group (Grok 4.1 Fast, Grok 4, Grok 3, Grok 3 Mini, Grok 2 / legacy, Code / specialized).
- **Tier**: Frontier reasoning vs. fast/cost-optimized vs. legacy.
- **Context**: Approximate max context window, in tokens.
- **Modality**: Text-only, code-tuned, or multimodal (vision / image).
- **Role**: xAI's own positioning (general reasoning, fast chat, coding, long-context, etc.).
- **Research**: Your intent for this repo (`core`, `secondary`, `document-only`).

---

## Frontier 4.1 Fast family

These are the latest fast frontier models positioned for agentic workflows and tool use, with very large context windows.

### `grok-4-1-fast-reasoning`

- **Family**: Grok 4.1 Fast
- **Tier**: Frontier reasoning, fast variant
- **Context**: ~2M token context (frontier long-context tier)
- **Modality**: Text, strong tool/agent support; multimodal support varies by deployment
- **Role**: High-end reasoning with fast, agentic tool calling for complex tasks and workflows
- **Aliases**: `grok-4-1-fast`, `grok-4-1-fast-latest` (provider/SDK dependent)
- **Research**: `core` (target for deep strengths/weaknesses mapping)

### `grok-4-1-fast-non-reasoning`

- **Family**: Grok 4.1 Fast
- **Tier**: Fast / cost-optimized, minimal reasoning tokens
- **Context**: ~2M token context
- **Modality**: Text; tuned for quick, low-latency responses
- **Role**: High-throughput drafting, simple Q&A, low-latency applications without heavy chain-of-thought
- **Aliases**: Sometimes exposed via simplified IDs or "fast" presets in SDKs
- **Research**: `secondary` (characterize mainly in contrast to reasoning variant)

---

## Grok 4 family

Grok 4 is the mainline reasoning model with strong multimodal and long-context capabilities.

### `grok-4-0709`

- **Family**: Grok 4
- **Tier**: Frontier reasoning
- **Context**: ~256K tokens (with "extended context" pricing above ~128K)
- **Modality**: Multimodal (text + images; some deployments emphasize coding)
- **Role**: Flagship reasoning model for long-context tasks, analysis, and multimodal understanding
- **Aliases**: Often surfaced as `grok-4` or via dated suffixes like `grok-4-YYYYMMDD`
- **Research**: `core` (primary non-fast frontier target)

### `grok-4-fast` (family)

- **Family**: Grok 4 Fast
- **Tier**: Fast frontier reasoning / long-context
- **Context**: ~2M tokens, with extended-context pricing tiers
- **Modality**: Text and multimodal support (varies by integration)
- **Role**: Long-context workloads that need both speed and high reasoning performance (e.g., code bases, large documents)
- **Aliases / variants**: Several dated or "fast" IDs (e.g., `grok-4-fast-YYYYMMDD`), plus provider-specific prefixes like `xai:grok-4-fast-reasoning`
- **Research**: `core` (compare against 4.1 Fast and Grok 3 family)

---

## Grok 3 family

Grok 3 models are widely described as prior-generation frontier models with strong reasoning and large context, now partly superseded by Grok 4.x.

### `grok-3`

- **Family**: Grok 3
- **Tier**: Frontier reasoning (previous generation)
- **Context**: Up to ~1M tokens in some deployments; commonly cited 1M window in public comparisons
- **Modality**: Text; some multimodal variants exist under related IDs
- **Role**: High-end reasoning and long-context, now a baseline for comparing Grok 4/4.1
- **Aliases**: `grok-3-beta`, environment-specific aliases in SDKs and platforms
- **Research**: `secondary` (mainly for historical and regression comparisons)

### `grok-3-fast`

- **Family**: Grok 3
- **Tier**: Fast / cost-optimized reasoning
- **Context**: ~131K tokens in common hosted configurations
- **Modality**: Text
- **Role**: Fast flagship model for latency-sensitive apps that still need nontrivial reasoning
- **Aliases**: `grok-3-fast-beta` and similar fast IDs
- **Research**: `secondary`

### `grok-3-mini`

- **Family**: Grok 3 Mini
- **Tier**: Small / cost-efficient reasoning
- **Context**: ~128–131K tokens, depending on provider integration
- **Modality**: Text
- **Role**: Lightweight general model, good for non-domain-heavy tasks and background reasoning with lower cost
- **Aliases**: `grok-3-mini-beta` and integration-specific IDs
- **Research**: `document-only` (useful as a point of reference, but not a core focus)

---

## Grok 2 and earlier / legacy

Older Grok models still appear in SDKs and third-party platforms, but are generally not recommended for new work.

### `grok-2`, `grok-2-vision-*`, `grok-beta`, etc.

- **Family**: Grok 2 / legacy
- **Tier**: Legacy general models
- **Context**: Typically ≤131K tokens depending on host platform
- **Modality**: Text; some early VLM / vision endpoints under `*-vision-*` IDs
- **Role**: Historical / compatibility endpoints; useful mainly for regression and migration testing
- **Aliases**: `x-ai/grok-beta`, `grok-2-vision-1212`, and similar IDs via aggregators and SDKs
- **Research**: `document-only`

---

## Code-focused and specialized models

xAI and third-party catalogs list code-optimized and specialized Grok variants.

### `grok-code-fast-*` and related IDs

- **Family**: Grok Code Fast
- **Tier**: Fast code / reasoning hybrid
- **Context**: Long-context (hundreds of thousands of tokens) in most hosted environments
- **Modality**: Text, code-focused; optimized for repositories and tooling integrations
- **Role**: Code completion, refactoring, repository-level reasoning, and agentic code tools
- **Aliases**: Environment-specific names such as `xai:grok-code-fast-1` and dated variants
- **Research**: `core` (for your use case, code-focused traits are relevant to prompt scaffolding)

---

## Notes and open questions

- **Exact context windows and pricing**: Values here are approximate and may vary by deployment; definitive numbers should be pulled from the current xAI docs or your own account.
- **Modality details**: Vision/multimodal behavior can differ between Grok 4, 4 Fast, and 4.1 Fast; confirm in live testing and provider docs.
- **Tool and agent capabilities**: 4.x and 4.1 Fast families are explicitly positioned for server-side tools and agentic workflows; later you may want a dedicated tool-capability matrix.

Once this inventory looks right to you, it can be converted into a structured JSON schema + instance with explicit fields for strengths, weaknesses, and recommended prompt tactics per model.
