📄 Multimodal RAG System (Text + Tables + Images)


📌 Project Overview
This project implements a Multimodal Retrieval-Augmented Generation (RAG) system that allows users to ask questions over PDF documents containing text, tables, and images.



The pipeline is built using open-source and free tools only, without relying on OpenAI APIs.

🎯 Key Features

📄 PDF ingestion with structured parsing

🧱 Intelligent chunking using document titles

📊 Table extraction and usage in answers

🖼️ Image extraction and storage (for reference)

🔍 Semantic search using vector embeddings

💾 Persistent vector storage (no re-ingestion on every query)


🧠 How the System Works (High Level)


Phase 1: Ingestion (EveryTime because i use FAISS)

PDF is parsed into elements (text, tables, images)

Elements are grouped into meaningful chunks

Chunks are summarized for retrieval efficiency

Text embeddings are generated

Embeddings are stored in a vector database



Phase 2: Querying (Repeated)

User question is converted into an embedding

Vector database retrieves the most relevant chunks

LLM generates an answer using retrieved context

Images/tables are returned as supporting metadata



🧰 Tech Stack & Libraries (with Reasoning)

🔹 Document Processing
unstructured
Parses PDFs into text, tables, and images
Preserves document structure
Handles complex academic and enterprise PDFs

poppler-utils
Required for high-resolution PDF parsing
Provides tools like pdfinfo used internally

🔹 Chunking
unstructured.chunking.title
Splits documents based on semantic titles
Prevents context loss compared to naive chunking

🔹 Embeddings
sentence-transformers (all-MiniLM-L6-v2)
Free, lightweight, high-quality text embeddings
Optimized for semantic similarity search
No API key required

🔹 Vector Store
FAISS
Fast in-memory vector search engine
Used to index and search embeddings efficiently
Pickle / FAISS persistence
Embeddings and metadata are saved to disk
Prevents re-ingestion on every query

Note: FAISS is used as a vector index. Persistence is handled explicitly.


🔹 Language Model
TinyLlama (TinyLlama-1.1B-Chat)
Open-source, lightweight LLM
No authentication or API keys required
Suitable for RAG-style grounded responses

🔹 Supporting Libraries
torch – model inference
numpy – vector operations
json / pickle – metadata storage


⚠️ Current Limitations

❌ No direct image reasoning (text-only LLM)

❌ No OCR (assumes digital PDFs)

❌ Single-document ingestion (can be extended)

These are intentional trade-offs to keep the system free and lightweight.

🚀 Future Improvements
Add OCR for scanned PDFs
Integrate vision-language models (e.g. LLaVA)
Multi-document ingestion
Streamlit or web UI
Replace FAISS with Chroma for automatic persistence