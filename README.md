# Hybrid RAG System - Quick Guide

This repository provides a **Hybrid Retrieval-Augmented Generation (RAG)** system for sparse municipal environments, combining semantic vector search (ChromaDB), structured Knowledge Graphs (Neo4j), and Large Language Models (Meta Llama 3.1).

## Key Files & Directories

- **Jupyter Notebook:**
  - All main steps are orchestrated in `https://github.com/berkantcnr/Hybrid-RAG-for-Sparsed-Municipal-Environments/blob/main/Hybrid_RAG_System.ipynb`.

- **Data Folder:**
  - Raw and processed PDFs are stored in `data/municipal_pdfs/`.
  - (PDFs are generated after web scraping and cleaning.)

- **Vector Database:**
  - ChromaDB persistent storage is in the `chroma_db/` directory.
  - (Both PDF and Knowledge Graph embeddings are stored here.)

- **Knowledge Graph (Ontology):**
  - Neo4j connection details are managed via the `.env` file.
  - The ontology/graph itself is hosted externally on a Neo4j instance.

- **Assets:**
  - Fonts and other assets for PDF generation are in the `assets/` folder.

## Workflow Overview

1. **Data Collection & PDF Generation:**
   - Municipal websites are scraped, cleaned, and converted to PDFs (`data/municipal_pdfs/`).

2. **Vector DB & Embedding:**
   - PDFs are embedded into ChromaDB (`chroma_db/`).
   - The Knowledge Graph (Neo4j) is also embedded for hybrid retrieval.

3. **Query & Answering:**
   - User questions are answered by retrieving from both the vector DB and the KG, then generating a final answer with the LLM.

## Important Notes

- A `.env` file is required for credentials (Huggingface and Neo4j access).
- All paths are set dynamically in the notebook; no manual changes are needed.
- ChromaDB and PDF folders are created automatically as the notebook runs.

---

## Requirements

```
langchain==1.2.0
langchain-community==0.4.1
langchain-text-splitters==1.1.0
langchain-core==1.2.6
sentence-transformers==5.2.0
chromadb==1.4.0
transformers==4.57.3
accelerate==1.12.0
bitsandbytes==0.49.0
torch==2.9.0+cu126
neo4j==6.0.3
pypdf==6.5.0
fpdf2==2.8.5
requests==2.32.5
beautifulsoup4==4.13.5
python-dotenv==1.2.1
ipykernel==6.17.1
```

---
This README provides a concise summary of the project structure and data locations for users. For detailed usage, see the original notebook.
