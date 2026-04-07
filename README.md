# IS469 RAG Comparison Project

This repository contains an academic comparison of multiple Retrieval-Augmented Generation (RAG) approaches evaluated on shared datasets:

- Naive RAG
- Reranking RAG
- Graph RAG
- Agentic RAG
- Self-RAG

All experiments are notebook-based and executed through Jupyter (no standalone backend service is required).

## Repository Structure

- `datasets/`: corpus files used across methods
  - `wiki_corpus.json`
  - `sci_wiki_unprocessed.jsonl`
  - `nba_rules_raw.json`
- `test_questions_*.json`: evaluation question sets at repository root
- `naiverag/`: Naive RAG notebooks
- `reranking rag/`: reranking notebooks
- `graphrag/`: graph-based retrieval notebooks
- `agenticrag/`: agentic pipeline notebooks
- `selfrag/`: Self-RAG notebook
- `PDF_to_JSON/`: PDF preprocessing notebook for NBA rules

## Local Setup

### 1) Clone the repository

```bash
git clone <your-repo-url>
cd is469_rag
```

### 2) Create and activate a Python environment

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
```

### 3) Install dependencies

Use the following superset installation to cover all notebooks:

```bash
pip install \
  jupyterlab notebook ipykernel \
  numpy pandas tqdm \
  cohere openai python-dotenv \
  sentence-transformers faiss-cpu transformers torch \
  networkx pdfplumber \
  chromadb \
  langchain langchain-community langchain-core langchain-text-splitters \
  langchain-cohere langchain-chroma langchain-openai \
  langgraph
```

### 4) Configure API keys

Create a `.env` file in the repository root:

```bash
cat > .env << 'EOF'
COHERE_API_KEY=your_cohere_key_here
OPENAI_API_KEY=your_openai_key_here
TAVILY_API_KEY=your_tavily_key_here
EOF
```

`COHERE_API_KEY` is required by most notebooks. `OPENAI_API_KEY` and `TAVILY_API_KEY` are required for the agentic notebooks.

### 5) Start Jupyter

```bash
jupyter lab
```

Open notebooks from their respective folders and run cells from top to bottom.

## Recommended Execution Order

1. Baseline methods:
   - `naiverag/naiverag_singletopic.ipynb`
   - `reranking rag/reranking_ai_wiki.ipynb`
   - `graphrag/graphrag.ipynb`
2. Advanced methods:
   - `agenticrag/agentic_rag_wiki.ipynb`
   - `selfrag/selfrag_proj.ipynb`

For full comparison, run the dataset-specific variants (`*_wiki`, `*_sci`, `*_nba`) for each method where available.

## Path Standardization

Notebook file paths are standardized as follows:

- Corpus files: `../datasets/...`
- Evaluation files: `../test_questions_*.json`

This allows consistent execution from inside each notebook folder.

## Notes and Limitations

- Python 3.11+ is recommended.
- Some notebooks include legacy placeholder key snippets; prefer `.env` loading for all keys.
- Self-RAG may run slowly on CPU-only hardware; GPU acceleration is beneficial when available.
- After package installation in a notebook, restart the kernel if imports fail.

