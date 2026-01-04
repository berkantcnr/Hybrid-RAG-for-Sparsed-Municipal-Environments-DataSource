# Hybrid RAG for Sparse Municipal Environments

**Master's Thesis Project** | *Friedrich-Alexander-Universität Erlangen-Nürnberg*  
**Author:** Berkant Cinar

---

## Overview

A **Hybrid Retrieval-Augmented Generation (RAG)** system that combines semantic vector search (**ChromaDB**), structured Knowledge Graphs (**Neo4j**), and Large Language Models (**Meta Llama 3.1**) to answer questions about municipal data.

The system uses a pre-built Knowledge Graph ontology (created during thesis) stored in Neo4j to provide structured context alongside vector search results.

### Architecture
- **Stage 1-2**: Data ingestion and PDF generation from web sources
- **Stage 3**: Vector database creation with semantic embeddings
- **Stage 4**: Knowledge Graph serialization and embedding (from pre-built ontology)
- **Stage 5**: Dual-channel retrieval (PDF + KG)
- **Stage 6**: LLM-based response generation

---

## Running on Google Colab

2. **Open the main notebook**:
   - Use `Hybrid_RAG_System.ipynb` 
   - Execute cells sequentially.
   - Huggingface and Neo4j credentials needed to connect knowledge graph and downloading llm model. 

3. **Configure credentials** (.env):
   ```
   HUGGINGFACEHUB_API_TOKEN=hf_your_token
   NEO4J_URI=neo4j+s://your-instance
   NEO4J_USERNAME=neo4j
   NEO4J_PASSWORD=your_password
   ```

4. **Run all cells** - the system automatically:
   - Scrapes municipal websites
   - Creates vector embeddings
   - Embeds knowledge graph data
   - Tests dual-channel retrieval
   - Generates answers with source attribution

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

## Citation

```bibtex
@thesis{cinar2026hybrid,
  author={Cinar, Berkant},
  title={Hybrid Retrieval-Augmented Generation for Sparse Municipal Environments},
  school={Friedrich-Alexander-Universität Erlangen-Nürnberg},
  year={2026},
  type={Master's Thesis}
}
```
