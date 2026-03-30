# COMP 3610 — Assignment 3: LLM-Powered Applications & Distributed Computing

> Semester II, 2025/2026 | Due: March 30, 2026

## Overview

This project builds a complete intelligent data analytics system combining:

- **Part 1** — Distributed data processing with Apache Spark over NYC Yellow Taxi trip records (Jan 2024)
- **Part 2** — RAG pipeline over a curated corpus of NYC taxi/transportation policy PDFs
- **Part 3** — Integrated natural-language interface with LLM-powered query routing
- **Part 4** — Documentation, code quality, and repository organisation

---

## Repository Structure

```
.
├── assignment3.ipynb      # Main Jupyter notebook (all code + outputs)
├── docs/                  # Curated PDF corpus (5–10 documents)
├── requirements.txt       # Python dependencies
├── README.md              # This file
└── .gitignore             # Excludes data files, chroma_db, __pycache__
```

> **Note:** The NYC Taxi Parquet file and `chroma_db/` are excluded from version control.  
> The notebook downloads the data programmatically on first run.

---

## Setup Instructions

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd <repo-name>
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
source venv/bin/activate        # Linux / macOS
venv\Scripts\activate           # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set your LLM API key

The notebook uses the Anthropic API (or substitute your course LLM server URL).

```bash
export ANTHROPIC_API_KEY="your-api-key-here"
```

Alternatively, edit the `LLM_API_KEY` variable at the top of `assignment3.ipynb`.

### 5. Add PDF documents to `docs/`

Place 5–10 publicly available PDFs related to NYC taxi / transportation policy in the `docs/` directory before running Part 2.  Suggested sources:

| Document | URL |
|---|---|
| NYC TLC Annual Report 2022 | https://www.nyc.gov/site/tlc/about/annual-reports.page |
| NYC TLC Annual Report 2023 | same as above |
| NYC DOT Strategic Plan | https://www.nyc.gov/html/dot/html/about/stratplan.shtml |
| MTA Facts & Figures | https://new.mta.info/transparency/data |
| Academic paper on FHVHV regulation | Google Scholar |

### 6. Run the notebook

```bash
jupyter notebook assignment3.ipynb
```

Run all cells in order (Kernel → Restart & Run All).

---

## Technologies Used

| Category | Tools |
|---|---|
| Distributed Computing | PySpark (local mode) |
| Document Processing | PyPDF, LangChain |
| Embeddings | sentence-transformers (all-MiniLM-L6-v2) |
| Vector Database | ChromaDB (persistent) |
| LLM | Anthropic Claude (or course LLM server) |
| Visualisation | Matplotlib, Seaborn |

---

## Notes

- `random_state=42` is used for all operations requiring reproducibility.
- All Spark operations use the DataFrame API or Spark SQL — no large-scale Pandas conversions.
- ChromaDB collections persist to `chroma_db/` (excluded from git) so embeddings survive notebook restarts.
