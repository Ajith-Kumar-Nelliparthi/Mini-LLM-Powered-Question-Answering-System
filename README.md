# Mini LLM-Powered Question-Answering System Using RAG

## Overview
This project implements a Retrieval-Augmented Generation (RAG) system to answer queries from a PDF document (e.g., clinical guidelines) in a 4-hour time-boxed challenge. It handles PDF ingestion, chunking, embedding, vector storage, retrieval, and LLM-based answering.

### Key Features
- **Document Ingestion**: Uses `PyPDFLoader` to extract text from a PDF, fixing `WebBaseLoader` issue.
- **Chunking**: Splits text into ~1000-character chunks with 200-character overlap using `RecursiveCharacterTextSplitter`.
- **Embedding**: `BAAI/bge-small-en-v1.5` for semantic embeddings with cosine similarity.
- **Vector Store**: Chroma for persistent storage, replacing Astra DB.
- **LLM**: `HuggingFaceH4/zephyr-7b-alpha` instead of `ChatGroq`, using `create_retrieval_chain` with custom prompt.
- **Query Interface**: Command-line interface for query input/output.
- **Outputs**: Saves answers and sources to `output/answers.txt`.

### Test Queries
- "Give me the correct coded classification for the following diagnosis: Recurrent depressive disorder, currently in remission"
- "What are the diagnostic criteria for Obsessive-Compulsive Disorder (OCD)?"

### AI Tool Usage
- README generated using Grok 3 (xAI), as permitted.

## Data Schema
- **Input**: A PDF file (`clinical_guidelines.pdf`) from Google Drive, containing medical text (e.g., ICD-10/DSM-5).
- **Assumption**: PDF is downloaded to `C:\Deep Learning Projects\credit_scoring\clinical_guidelines.pdf`.

## Methodology
- **Ingestion**: `PyPDFLoader` extracts text from PDF pages.
- **Chunking**: 1000-character chunks with 200-character overlap.
- **Embedding**: `BAAI/bge-small-en-v1.5` with `normalize_embeddings=True`.
- **Vector Store**: Chroma with persistent storage (`./chroma_db`).
- **LLM**: Zephyr-7B generates answers via `create_retrieval_chain` with custom `ChatPromptTemplate`.
- **Query Interface**: Command-line, outputs answers and source snippets.

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/Ajith-Kumar-Nelliparthi/Mini-LLM-Powered-Question-Answering-System.git
   cd mini_rag

2. Usage
- Notebook:
    ```cmd
    uv run jupyter notebook rag_qa_system.ipynb
3. Outputs:
- output/answers.txt: Query answers and sources.
- chroma_db/: Persistent Chroma vector store.
- Console: Displays answers and sources.

### Design Decisions
- PyPDFLoader: Extracts PDF text, fixing WebBaseLoader issue.
- BAAI/bge-small-en-v1.5: High-quality embeddings per user preference.
- Chroma: Persistent storage.
- Zephyr-7B: Open-source.
- create_retrieval_chain: Uses custom ChatPromptTemplate for precise RAG control.
- Chunking (5000 chars, 400 overlap): Balances context and efficiency.
- Command-line: Prioritizes functionality over GUI.

### LimitationsTime Constraints: Skipped Gradio, caching, reranking due to 4-hour limit.
- PDF Access: Assumes manual download from Google Drive.
- Hardware: Zephyr-7B may require 8GB RAM or GPU; Chroma needs disk space.
- PDF Content: Assumes text-based PDF; image-based PDFs need OCR.

### Sample Outputs
Query: Give me the correct coded classification for the following diagnosis: Recurrent depressive disorder, currently in remission
- Answer: MENTAL AND BEHAVIOURAL DISORDERS
F33.4 Recurrent depressive disorder, currently in remission
Diagnostic guidelines
For a definite diagnosis:
(a) the criteria for recurrent depressive disorder (F33. -) should have
been fulfilled in the past, but the current state should not fulfil
the criteria for depressive episode of any degree of severity or
for any other disorder in F30-F39; and
(b) at least two episodes should have lasted a minimum of 2 weeks
and should have been separated by several months without
significant mood disturbance.
