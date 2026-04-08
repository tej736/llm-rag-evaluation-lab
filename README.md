# LLM Evaluation & RAG Experimentation Lab

A portfolio-grade, provider-agnostic RAG playground for comparing model stacks and evaluating retrieval quality with RAGAS.

## Repository naming (recommended)

If you want a clearer portfolio identity than `rag-with-ragas-example`, use one of these names:

- `llm-rag-evaluation-lab` (recommended)
- `provider-agnostic-rag-lab`
- `rag-experiments-ragas-analytics`

## Why this fork stands out

- Added **OpenAI + Hugging Face** support for both embeddings and generation
- Added **side-by-side experiment mode** in Streamlit to compare two RAG configurations
- Added **RAGAS evaluation workflow** with configurable test-set distributions
- Added **experiment tracking** (`runs.jsonl`, `runs.csv`) for query and eval runs
- Added **dataset ingestion/version registry** (`manifest.jsonl`, `ingestions.csv`)
- Added **analytics views** for latency, metric drift, and failure-case exploration

## Key capabilities

### 1) RAG query lab
- Upload PDFs/TXTs and add URLs as sources
- Configure chunking, overlap, token model, top-k retrieval
- Run one config or two configs side-by-side
- Inspect retrieved chunks with similarity scores

### 2) RAGAS evaluation lab
- Generate evaluation test sets with custom simple/reasoning/multi-context distributions
- Score runs on context relevancy, context precision, context recall, faithfulness, and answer relevancy
- Persist results to CSV for reproducible comparisons

### 3) Experiment analytics
- Track all run metadata and outputs in SQL-friendly artifacts
- Visualize latency by provider/model and quality drift across eval runs
- Export run history CSV and markdown experiment summary

## Project structure

- `app/rag.py` – provider-agnostic embedding/generation + retrieval logic
- `app/eval.py` – RAGAS test-set generation and evaluation pipeline
- `app/streamlit.py` – interactive lab UI + analytics dashboard
- `app/tracking.py` – experiment tracker and dataset registry
- `app/data/` – local source documents
- `app/output/` – generated artifacts and experiment outputs
- `tests/` – config/tracking unit tests

## Getting started

### Option A: Docker (recommended)

```sh
docker compose up --build
```

Open: http://localhost:8080

### Option B: Local Python setup

```sh
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
streamlit run app/streamlit.py
```

## Environment variables

Set one or both depending on the provider you use:

```sh
OPENAI_API_KEY=your_openai_key
HUGGINGFACE_API_TOKEN=your_hf_token
```

## Reproducible outputs

- Query/eval run logs: `app/output/experiments/runs.jsonl`, `app/output/experiments/runs.csv`
- Dataset ingestion registry: `app/output/datasets/manifest.jsonl`, `app/output/datasets/ingestions.csv`
- Evaluation artifacts: `app/output/testset.csv`, `app/output/generated_dataset.csv`, `app/output/evaluation_results.csv`

## Validation

```sh
python -m compileall app tests
python -m unittest discover -s tests -v
```

## Acknowledgements

- [Modular Rag and chat implementation from URLs, PDFs and txt files. | Patreon](https://www.patreon.com/posts/modular-rag-and-106461497)
- [Coding-Crashkurse/RAG-Evaluation-with-Ragas](https://github.com/Coding-Crashkurse/RAG-Evaluation-with-Ragas)
