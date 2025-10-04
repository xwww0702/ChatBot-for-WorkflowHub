# ChatBot-for-WorkflowHub

This project provides a full pipeline for building a **history-aware RAG chatbot** for WorkflowHub metadata, including preprocessing `.jsonld` files, extracting CWL files, embedding documents into a vector database, answering questions using a local LLM, and evaluating answer quality.

---

## Project Structure

| File                      | Description                                                                                                                                                                              |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `history_chatbot.ipynb`   | Main notebook to **run the chatbot**. It handles rewriting user questions based on history, retrieving documents via a retriever (with reranker), and invoking a local LLM (via Ollama). |
| `processJsonLd.ipynb`     | Script to **process and flatten** the BioSchemas `.jsonld` metadata, converting it into structured documents for RAG ingestion.                                                          |
| `RAG_evaluate.ipynb`      | Notebook to **evaluate chatbot responses** using [RAGAS](https://github.com/explodinggradients/ragas). Supports Gemini and other LLMs.                                                   |
| `extract_cwl_files.ipynb` | Notebook for **extracting raw CWL workflow files** and metadata from JSON or RDF sources. Helpful for linking source files to chatbot context.                                           |
| `requirements.txt`        | List of required Python packages. Run `pip install -r requirements.txt` before use.                                                                                                      |
| `results.md`              | Partial results from chatbot evaluation, including generated answers, scores, and discussion.                                                                                            |

---

## Getting Started

### 1. Install Dependencies

Make sure you are in a virtual environment (optional), then run:

```bash
pip install -r requirements.txt
```

Ensure you have Python 3.10+.

### 2. Download LLM in Ollama

Before using the chatbot, make sure you have an LLM running locally via Ollama. For example:

ollama run llama3

Or change to your preferred local model in ChatOllama(...) if needed.

⸻

## How to Run

### Run the Chatbot (with History)

Open and execute:

history_chatbot.ipynb

This notebook supports:
• Question rewriting via history
• Document retrieval + reranking
• RAG response generation via a local LLM (Ollama)

### Preprocess Workflow Metadata

Run:

processJsonLd.py

This script will:
• Load workflows-bioschemas-dump (1).jsonld
• Flatten nested metadata structure
• Convert to LangChain/LlamaIndex document format
• Save into memory or vectorstore for further use

### Evaluate Responses

Open and execute:

RAG_evaluate.ipynb

This evaluates the generated answers using:
• RAGAS metrics (e.g. Faithfulness, Context Precision, Answer Relevancy)
• Gemini or other LLMs (via LangchainLLMWrapper)
• Ground truth can be derived from conversation or manually added

### Partial evaluation results can be found in:

results.md

## Notes

- You may customize the embedding model (BAAI/bge-small-en-v1.5) or reranker (CohereRerank) depending on access.
- For Gemini-based evaluation, make sure you have a valid Google Generative AI API key.
- chat_history can be modified to retain different lengths or formats of memory during multi-turn QA.
