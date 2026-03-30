# COMP 3610 — Assignment 3: LLM-Powered Applications & Distributed Computing

## Overview

This project builds an intelligent data analytics system that combines distributed computing with LLM-powered retrieval and query handling. It is structured across three main parts:

- **Part 1** — Distributed data processing with Apache Spark over NYC Yellow Taxi trip records (January 2024)
- **Part 2** — A RAG pipeline over a curated corpus of NYC taxi and transportation policy PDFs
- **Part 3** — An integrated natural-language interface with LLM-powered query routing
- **Part 4** — Documentation, code quality, and repository organisation

---

## Repository Structure

```
.
├── assignment3.ipynb      # Main notebook (all code and outputs)
├── docs/                  # PDF corpus (TLC reports, DOT publications)
├── requirements.txt       # Python dependencies
├── README.md              # This file
└── .gitignore             # Excludes data files, chroma_db/, __pycache__/
```

The NYC Taxi Parquet file and `chroma_db/` are excluded from version control. The notebook downloads the dataset programmatically on first run.

---

## Setup Instructions

### Running on Google Colab (recommended)

1. Upload `assignment3.ipynb` to [colab.research.google.com](https://colab.research.google.com)
2. Upload your PDF documents to the `docs/` folder using the cell provided in Task 2.1
3. Set your API key in the imports cell where it says `LLM_API_KEY = "YOUR_API_KEY_HERE"`
4. Run all cells in order (Runtime → Run all)

Cell 1 automatically detects the environment and configures Java and Hadoop paths — no manual setup is needed on Colab.

### Running locally (Jupyter / VSCode)

**Requirements:**
- Python 3.9+
- Java 11 or 17 (JDK, not JRE)
  - Windows: [Eclipse Adoptium JDK 11](https://adoptium.net/temurin/releases/?version=11)
  - Linux/macOS: `apt install openjdk-17-jdk` or `brew install openjdk@17`

```bash
git clone <your-repo-url>
cd <repo-name>
pip install -r requirements.txt
jupyter notebook assignment3.ipynb
```

On Windows, Cell 1 will automatically download `winutils.exe` if it is not already present at `C:\hadoop\bin\`.

### API Key

The notebook uses the course Synapse LLM server. Set your key in the imports cell:

```python
LLM_API_KEY = "your-key-here"
```

### PDF Documents

Place your PDF files in the `docs/` directory before running Part 2. The notebook expects 5–10 documents related to NYC taxi and transportation policy. The following were used in this submission:

| Document | Source |
|---|---|
| NYC TLC Annual Report 2022 | nyc.gov/tlc |
| NYC TLC Annual Report 2023 | nyc.gov/tlc |
| NYC TLC Annual Report 2024 | nyc.gov/tlc |
| NYC TLC Electrification Report | nyc.gov/tlc |
| NYC TLC Driver Expense Report | nyc.gov/tlc |
| NYC TLC OFS Annual Report 2023 | nyc.gov/tlc |
| NYC DOT Strategic Plan 2016 | nyc.gov/dot |

---

## Technologies

| Category | Tool |
|---|---|
| Distributed Computing | PySpark (local mode) |
| Document Processing | PyPDF, LangChain |
| Embeddings | sentence-transformers (all-MiniLM-L6-v2) |
| Vector Database | ChromaDB (persistent) |
| LLM | Synapse LLM server (llama3.3-70b-instruct) |
| Visualisation | Matplotlib, Seaborn |

---

## Notes

- `random_state=42` is used for all operations requiring reproducibility
- All Spark operations use the DataFrame API or Spark SQL — the full dataset is never converted to Pandas
- ChromaDB collections persist to `chroma_db/` so embeddings survive notebook restarts

---
