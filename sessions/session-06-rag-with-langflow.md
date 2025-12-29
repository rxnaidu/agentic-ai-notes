# Session 6: Building RAG with No-Code Platform (LangFlow)

## Objective
Build a Retrieval-Augmented Generation (RAG) chatbot using **LangFlow**, a no-code / low-code visual workflow tool, and understand how it maps to standard RAG architecture and real-world deployment.

---

## What is LangFlow?
- No-code UI for building LLM workflows using **drag-and-drop**
- Built by **DataStax** (Astra DB), now part of **IBM**
- Uses LangChain concepts under the hood
- Best suited for:
  - Learning
  - Prototyping
  - POCs / demos
- Not yet enterprise-scale or fully production-hardened (still in public review / beta)

---

## Related Stack Context
- **LangChain** → Code-based RAG & workflows
- **LangGraph** → Agentic workflows & orchestration
- **LangSmith** → Observability, evaluation, tracing
- **LangFlow** → Visual builder (separate from LangChain stack)
- **Astra DB** → Vector database used by LangFlow

---

## Vector Database: Astra DB
- Managed vector DB from DataStax
- Stores:
  - Embeddings (e.g., 1536-dim OpenAI vectors)
  - Metadata (file path, chunk info, timestamps)
- Concepts:
  - Database
  - Keyspace
  - Collection
- Supports cosine similarity search
- Auth via **Application Token**

---

## High-Level RAG Architecture (Same as Code-Based)
1. **Ingestion**
   - Upload files (PDF, directory, etc.)
   - Split text into chunks
   - Generate embeddings
   - Store in vector database

2. **Query-Time**
   - User query
   - Query embedding
   - Vector DB retrieval
   - Prompt = context + question
   - LLM generates answer
   - Response returned to UI/API

LangFlow visually wires these components instead of writing code.

---

## LangFlow UI Concepts
- **Canvas**: Drag-and-drop workflow builder
- **Components**:
  - File loaders
  - Text splitters
  - Embedding models
  - Vector DBs (Astra, Chroma, etc.)
  - Prompt templates
  - LLMs (OpenAI, Anthropic, etc.)
  - Chat input/output
- **Connections**: Output of one component → input of another
- **Code View**: Auto-generated Python code for each component

---

## Building the RAG Workflow (Bottom → Top)

### 1. Data Ingestion Flow
- File Upload (PDF / directory)
- Text Splitter
  - Chunk size
  - Chunk overlap
- Embedding Model (e.g., OpenAI)
- Astra DB (collection creation & storage)

This runs once or periodically to populate the vector DB.

---

### 2. Chatbot / Query Flow
- Chat Input (user question)
- Query passed to:
  - Prompt (directly)
  - Embedding model → Vector DB retriever
- Retrieved chunks parsed
- Prompt constructed (context + question)
- LLM invoked (e.g., GPT-4.1)
- Output sent to Chat Output

---

## Playground & Testing
- Built-in chat playground
- Ask questions like:
  - “What skills are in the resume?”
  - “Summarize projects in bullet points”
- Responses depend heavily on:
  - Chunking strategy
  - Overlap
  - Retrieval quality

Missing answers usually indicate chunking/retrieval issues, not model failure.

---

## Deployment Model
- LangFlow generates an **API endpoint**
- Authentication via generated token
- Can be invoked from:
  - Python
  - JavaScript
  - UI apps (FastAPI, Streamlit, React, etc.)
- Similar to deploying any backend service:
  - Endpoint
  - Auth
  - Scaling via containers / Kubernetes

---

## Security Model
- Vector DB secured via tokens & access control
- Models accessed via secured endpoints (OpenAI, Azure OpenAI, etc.)
- LangFlow itself is not exposed to end users
- End users interact only with secured APIs
- Same security principles as:
  - AWS
  - Azure
  - Snowflake
  - Informatica

---

## LangFlow vs Code-Based RAG (Reality Check)

### LangFlow
- Great for learning & POCs
- Fast iteration
- Visual understanding
- Limited production adoption today

### Production Reality
- Most enterprises still use:
  - Python / Java
  - LangChain / CrewAI / AutoGen
  - Custom APIs
  - Cloud-native deployment (AWS / Azure)
- No-code tools may mature later (similar to ETL evolution)

---

## Key Takeaways
- LangFlow = **visual RAG builder**
- Same architecture as LangChain, just abstracted
- Excellent learning tool
- Not a replacement for production-grade engineering (yet)
- Understanding the architecture matters more than the tool

---

## Suggested Practice (Holiday Homework)
- Re-run provided notebooks
- Try different:
  - Documents
  - Chunk sizes
  - Embedding models
  - Vector DBs
- Build a RAG chatbot for a new use case (not resume screening)
- Focus on **understanding failures** (retrieval > model)

---

## What’s Next
- Agentic workflows
- LangGraph
- CrewAI / AutoGen
- Observability & evaluation
- Guardrails
- MCP servers
- End-to-end projects

---
