# Generative AI & Agentic Systems Engineering Lab

[![CI](https://github.com/Sai-juttu-1/genai-work/actions/workflows/main.yml/badge.svg)](https://github.com/Sai-juttu-1/genai-work/actions/workflows/main.yml)
![Python 3.12](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)
![uv](https://img.shields.io/badge/uv-package%20management-DE5FE9?style=flat)
![pytest](https://img.shields.io/badge/tested%20with-pytest-0A9EDC?style=flat&logo=pytest&logoColor=white)

> An applied AI engineering repository exploring LLM fundamentals, embeddings, model selection, multi-provider inference, local models, multimodal AI, structured outputs, and reliable AI system development.

This project focuses on understanding what happens **behind modern Generative AI applications** and how those components can be engineered into reliable software systems.

Rather than treating models as black boxes, the repository explores the complete engineering layer around them:

**Tokens → Embeddings → Models → Providers → Structured Outputs → Validation → Testing → AI Systems**

---

## Architecture Overview

```text
                         AI APPLICATION
                              │
                              ▼
                  ┌───────────────────────┐
                  │   Application Layer   │
                  └───────────┬───────────┘
                              │
             ┌────────────────┼────────────────┐
             ▼                ▼                ▼
       Structured         Provider          Multimodal
         Output            Routing              AI
             │                │                │
             └────────────────┼────────────────┘
                              ▼
                    Inference Abstraction
                              │
                 ┌────────────┴────────────┐
                 ▼                         ▼
            Cloud Models              Local Models
                 │                         │
        Gemini / Groq / OpenAI           Ollama
```

---

## Engineering Focus

This repository focuses on the engineering challenges that appear when building applications around Large Language Models:

- **LLM Foundations:** Tokenization, BPE, context windows, token economics, and embeddings.
- **Vector Engineering:** High-dimensional vector spaces, cosine similarity, PCA, SVD, and dimensionality reduction.
- **Model Engineering:** Comparing models based on capability, latency, throughput, context, and cost.
- **Provider Abstraction:** Building unified interfaces across Gemini, Groq, OpenAI, and local Ollama inference.
- **AI Reliability:** Converting probabilistic model responses into validated, machine-readable structures using Pydantic and schemas.
- **Multimodal AI:** Processing images and documents and extracting structured information.
- **Test-Driven AI Development:** Using offline fixtures, unit tests, and CI to verify AI application components.

---

## Core Concepts & Implementations

| Area | Engineering Focus | Implementation | Tests |
|---|---|---|---|
| **Tokens & Embeddings** | BPE tokenization, context budgeting, token-to-byte ratios, pricing estimation | [`s09_tokens.ipynb`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/s09_tokens.ipynb) · [`tokens_utils.py`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/tokens_utils.py) | `tests/test_s09.py` |
| **Model Landscape** | Model comparison, latency, throughput, capability tiers | [`s10_model_matrix.ipynb`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/s10_model_matrix.ipynb) · [`landscape_utils.py`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/landscape_utils.py) | `tests/test_s10.py` |
| **Provider Routing** | Unified provider interfaces, temperature experiments, fallback strategies | [`s11_providers.ipynb`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/s11_providers.ipynb) · [`providers_utils.py`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/providers_utils.py) | `tests/test_s11.py` |
| **Local Models** | Ollama inference, latency evaluation, cloud vs local trade-offs | [`s12_local_models.ipynb`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/s12_local_models.ipynb) · [`local_models_utils.py`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/local_models_utils.py) | `tests/test_s12.py` |
| **Vision & Structured Output** | Multimodal extraction, document parsing, strict Pydantic validation | [`s13_vision_structured.ipynb`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/s13_vision_structured.ipynb) · [`vision_utils.py`](https://github.com/lowkey999-netizen/genai-course-work/blob/main/module01/vision_utils.py) | `tests/test_s13.py` |

---

## Key Engineering Takeaways

### Vector Geometry & High-Dimensional Representations

Embedding models represent text as vectors in high-dimensional spaces.

For example:

```text
Text
  ↓
Embedding Model
  ↓
[0.12, -0.84, 0.31, ..., 0.07]
  ↓
High-dimensional vector
```

The repository explores cosine similarity, Euclidean distance, distance concentration, PCA, and SVD to understand how semantic representations can be compared and visualized.

Cosine similarity is particularly useful for semantic applications because it focuses on the orientation of vectors rather than their absolute magnitude.

---

### Context Window Economics

LLMs process tokenized input rather than raw text.

Pre-computing token counts locally helps applications:

- estimate request size
- prevent context overflow
- estimate API costs
- control prompt budgets
- design retrieval limits

This becomes especially important when building RAG and agentic systems where prompts can grow dynamically.

---

### Structured Output Reliability

LLM responses are probabilistic, while downstream software requires predictable data.

Using Pydantic models, enums, regex constraints, and structured schemas creates a validation boundary:

```text
LLM
 │
 ▼
Probabilistic Response
 │
 ▼
Schema Validation
 │
 ├── Valid ──────→ Application
 │
 └── Invalid ────→ Error / Retry / Recovery
```

This approach helps reduce failures caused by:

- malformed JSON
- missing fields
- incorrect data types
- invalid enum values
- unexpected model output

---

### Cloud vs Local AI

Cloud models provide access to powerful inference infrastructure, while local models provide greater control over data and execution.

The repository explores both approaches:

```text
                AI Application
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
       Cloud                  Local
          │                     │
 Gemini / Groq / OpenAI      Ollama
          │                     │
   Scale / Capability       Privacy / Control
```

A practical AI platform can route requests based on:

- task complexity
- data sensitivity
- latency requirements
- cost constraints
- model availability

---

## Interactive Browser Visualizers

The repository includes standalone browser-based visualizers for understanding the mathematics behind embeddings and dimensionality reduction.

### 🔬 Complete Embedding & SVD Pipeline

[**Open Embedding & SVD Pipeline Visualizer**](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/pipeline_visualizer.html)

Interactive pipeline:

```text
Word
 ↓
Vector Sliders
 ↓
768D Representation
 ↓
PCA
 ↓
SVD
 ↓
2D Projection
```

---

### 📊 Interactive Embedding & PCA Journey

[**Open Embedding & PCA Visualizer**](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/interactive_embedding_pca_journey.html)

Explore how high-dimensional semantic representations can be projected into lower-dimensional spaces.

---

### 📐 Embeddings & Dimensions Visualizer

[**Open Embeddings & Dimensions Visualizer**](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/embeddings_visualizer.html)

Explore vector dimensions, coordinate changes, angles, and cosine similarity.

---

## Architecture & Engineering Practices

### Automated CI

Every commit can be verified through GitHub Actions.

The repository currently includes **65+ automated unit and logic tests** covering core functionality, validation, and AI-related utilities.

[**View GitHub Actions**](https://github.com/lowkey999-netizen/genai-course-work/actions)

---

### Modern Python Toolchain

The project uses [`uv`](https://docs.astral.sh/uv/) for:

- virtual environment management
- dependency resolution
- reproducible installations
- lock-file based dependency management

The project uses Python 3.12.

---

### Provider-Agnostic Architecture

The provider layer is designed to keep application logic independent from individual model providers.

Supported experimentation includes:

- Gemini
- Groq
- OpenAI
- Ollama

This makes it easier to compare models and change inference backends without rewriting the entire application layer.

---

### Offline-First Testing

Core logic can be tested without requiring live API calls.

This provides:

- faster development
- reproducible tests
- lower API usage
- easier CI execution
- fewer external dependencies during development

Live provider tests can be executed separately when real model behavior needs to be evaluated.

---

## Repository Structure

```text
.
├── module01/
│   ├── s09_tokens.ipynb
│   ├── tokens_utils.py
│   │
│   ├── s10_model_matrix.ipynb
│   ├── landscape_utils.py
│   │
│   ├── s11_providers.ipynb
│   ├── providers_utils.py
│   │
│   ├── s12_local_models.ipynb
│   ├── local_models_utils.py
│   │
│   ├── s13_vision_structured.ipynb
│   ├── vision_utils.py
│   │
│   ├── pipeline_visualizer.html
│   ├── interactive_embedding_pca_journey.html
│   └── embeddings_visualizer.html
│
├── tests/
│   ├── test_s09.py
│   ├── test_s10.py
│   ├── test_s11.py
│   ├── test_s12.py
│   └── test_s13.py
│
├── showcase/
├── pyproject.toml
├── uv.lock
└── README.md
```

---

## Quickstart

### Prerequisites

- Python 3.12+
- Git
- [`uv`](https://docs.astral.sh/uv/)

Optional:

- Ollama
- Gemini API key
- Groq API key
- OpenAI API key

---

### 1. Clone the Repository

```bash
git clone https://github.com/lowkey999-netizen/genai-course-work.git
cd genai-course-work
```

---

### 2. Sync the Environment

```bash
uv sync
```

---

### 3. Run the Offline Test Suite

Run the core test suite without requiring API keys:

```bash
uv run pytest tests/ showcase/ --ignore=tests/test_setup.py -k "not live and not estimate_matches and not test_model_answers" -v
```

This verifies the repository's deterministic logic, validation, and test fixtures.

---

### 4. Run Live Provider Tests

For experiments requiring real model providers:

```bash
cp .env.example .env
```

Add the required API keys to `.env`.

Then run:

```bash
uv run pytest
```

Live tests are separated from the offline verification path so normal development does not depend on external model availability.

---

## Technical Coverage

```text
LLM Foundations
├── Tokens
├── BPE
├── Context Windows
└── Cost Estimation

Embeddings
├── Vector Representations
├── Cosine Similarity
├── High-Dimensional Geometry
├── PCA
└── SVD

Model Engineering
├── Model Selection
├── Latency
├── Throughput
├── Provider Abstraction
└── Routing

Inference
├── Cloud Models
├── Local Models
├── Ollama
└── Fallback Strategies

AI Reliability
├── Structured Outputs
├── Pydantic
├── JSON Schemas
├── Validation
└── Automated Testing

Multimodal AI
├── Vision Models
├── Document Processing
├── OCR-style Extraction
└── Structured Parsing

Engineering
├── Python
├── pytest
├── uv
├── Git
└── GitHub Actions
```

---

## Engineering Direction

This repository is being extended toward larger **Generative AI and Agentic AI systems**, including:

- Retrieval-Augmented Generation (RAG)
- Vector databases
- Advanced embedding pipelines
- Tool calling
- Agent workflows
- Stateful agents
- Agent evaluation
- Guardrails
- MCP integrations
- API orchestration
- AI observability
- Production-oriented AI services

The long-term direction is to move from individual AI components toward **modular, testable, reliable AI systems**.

---

## About

This repository represents hands-on work toward **AI Engineering, Generative AI, and Agentic AI system development**.

The engineering approach is:

> **Understand → Build → Measure → Validate → Test → Automate**

The objective is to understand not only how to use AI models, but how to build the reliable software systems around them.

---

## 🔗 Project Links

- [GitHub Repository](https://github.com/lowkey999-netizen/genai-course-work)
- [GitHub Actions / CI](https://github.com/lowkey999-netizen/genai-course-work/actions)
- [Interactive Embedding Visualizer](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/pipeline_visualizer.html)
- [Embedding & PCA Visualizer](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/interactive_embedding_pca_journey.html)
- [Dimensions Visualizer](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/embeddings_visualizer.html)


