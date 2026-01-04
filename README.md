# Hybrid RAG for Sparse Municipal Environments 🏙️

**Master's Thesis Project** | *Friedrich-Alexander-Universität Erlangen-Nürnberg*
**Author:** Berkant Cinar

---

## 📌 Abstract
This research presents a **Hybrid Retrieval-Augmented Generation (RAG)** architecture designed to address the challenges of information retrieval in municipal domains characterized by sparse and unstructured data. By integrating a semantic vector search engine (**ChromaDB**) with a structured Knowledge Graph (**Neo4j**), the system enables context-aware question answering using Large Language Models (**Meta Llama 3.1**).

---

## ⚙️ System Architecture & Methodology

The project implementation is divided into four distinct phases:

### 1. Data Acquisition and Preprocessing
**Rationale:** In municipal administrative domains, data is mostly unstructured and sparsed across various web portals. To address this, a custom data pipeline was established.
* **Source Corpus:** 14 primary institutional websites were targeted. A recursive web scraping algorithm traversed these domains, resulting in 53 processed URLs.
* **Processing:** Data extraction was executed using **BeautifulSoup4**, followed by a rigorous cleaning phase to remove noise (cookies, social media widgets). The output was standardized into PDF documents for vector ingestion.

### 2. Knowledge Graph Construction (Ontology)
**Rationale:** To capture the hierarchical and administrative relationships often lost in pure text, a structured Knowledge Graph was implemented.
* **Ontology:** A custom ontology based on **CIDOC-CRM** was developed to map municipal entities (e.g., *Facilities, Groups, Events*).
* **Implementation:** The structural data is stored in **Neo4j**, allowing for Cypher-based graph traversals that answer complex queries such as "Who owns this facility?" or "What acts does this department perform?".

### 3. Hybrid Retrieval Engine
**Rationale:** Standard RAG systems often fail to retrieve exact relational facts. This system employs a dual-retrieval strategy:
* **Vector Branch (Unstructured):** Utilizes `sentence-transformers/paraphrase-multilingual-mpnet-base-v2` within **ChromaDB** to find semantic matches in PDF documents.
* **Graph Branch (Structured):** Utilizes `all-MiniLM-L6-v2` to map user queries to graph entities, executing recursive Cypher queries to fetch relational context.
* Results from both branches are normalized and concatenated to form a rich context window.

### 4. Generative Response (LLM Integration)
**Rationale:** To synthesize the retrieved information into coherent, natural language responses.
* **Model:** **Meta Llama 3.1-8B-Instruct** (quantized via BitsAndBytes) is employed as the reasoning engine.
* **Pipeline:** The model receives the context from the Hybrid Retrieval Engine and generates precise answers acting as a "Municipal Expert".

---

## 📂 Repository Structure

| Directory | Description |
| :--- | :--- |
| `chroma_db/` | Persistent vector database containing municipal PDF embeddings. |
| `data/` | Raw dataset (Cleaned PDFs scraped from municipal sources). |
| `notebooks/` | Source code for the system. **(Main File: `Hybrid_RAG_System.ipynb`)** |
| `ontology/` | RDF/XML files defining the semantic relationships. |
| `assets/` | Supplementary files (fonts, images). |
| `requirements.txt` | List of Python dependencies. |

---

## 🚀 Installation & Usage

### Prerequisites
* Python 3.10+
* Neo4j Database (Local or AuraDB)
* Hugging Face API Token (for Llama 3.1)

### Setup Steps

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/berkantcnr/Hybrid-RAG-for-Sparsed-Municipal-Environments.git](https://github.com/berkantcnr/Hybrid-RAG-for-Sparsed-Municipal-Environments.git)
    cd Hybrid-RAG-for-Sparsed-Municipal-Environments
    ```

2.  **Install Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Configure Environment:**
    Create a `.env` file in the root directory:
    ```ini
    HUGGINGFACEHUB_API_TOKEN=your_token
    NEO4J_URI=neo4j+s://your-instance-url
    NEO4J_USERNAME=neo4j
    NEO4J_PASSWORD=your_password
    ```

4.  **Run the System:**
    Open `notebooks/Hybrid_RAG_System.ipynb` in VS Code, select your Python kernel, and execute the cells.

---

## 🎓 Acknowledgments
This project was developed as part of the Master's Thesis at **Friedrich-Alexander-Universität Erlangen-Nürnberg**.