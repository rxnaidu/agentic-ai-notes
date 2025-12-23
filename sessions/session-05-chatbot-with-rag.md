# Session 5 — Building a Chatbot with RAG Architecture

## Objective
Extend **semantic search** into a **production-style chatbot** using **Retrieval-Augmented Generation (RAG)** by adding an LLM on top of embeddings and a vector database.

---

## 1. Recap: Where We Left Off
Previous sessions covered:
- GenAI architecture & ecosystem
- LLMs and limitations
- Prompt engineering
- Embeddings & vector databases
- **Semantic search**

### Semantic Search Summary
- Query → Embeddings → Vector DB → Similar chunks
- Meaning-based retrieval (not keyword/SQL)
- Output = raw chunks (not user-friendly)

---

## 2. From Semantic Search → Chatbot
To build a chatbot:
- Add an **LLM (Generator)** on top of semantic search
- Combine:
  - User query
  - Retrieved chunks (context)
- Send both to the LLM
- LLM returns a **formatted, natural-language answer**

This completes the **RAG architecture**.

---

## 3. RAG Architecture (Core Flow)

**RAG = Retriever + Augmenter + Generator**

1. **Retriever**
   - Converts query to embeddings
   - Retrieves top-K chunks from vector DB

2. **Augmenter**
   - Injects retrieved chunks + user query into prompt

3. **Generator (LLM)**
   - Produces grounded response
   - Uses provided context only (if instructed)

---

## 4. Why RAG Matters
RAG addresses LLM limitations:
- ❌ No access to internal/company data
- ❌ Knowledge cutoff
- ❌ Hallucinations

RAG enables:
- Internal enterprise chatbots (HR, policies, IT)
- Customer support bots (manuals, FAQs)
- Legal, healthcare, research assistants
- Resume screening & enterprise search

---

## 5. Enterprise Security Model
- RAG app runs **inside enterprise network**
- Models accessed via **secured endpoints**
- AuthN/AuthZ enforced
- Users see only authorized data
- Guardrails applied pre- and post-response

➡️ Data is **not blindly sent to public models**

---

## 6. RAG Variants
As complexity grows:
- **Hybrid RAG**
  - Vector search + SQL filtering
- **Graph-based RAG**
  - Knowledge graphs + relationships
- **Multi-source RAG**
  - Structured + unstructured data

---

## 7. Framework Used: LangChain
LangChain stitches components together:
- Document loaders
- Text splitters
- Embeddings
- Vector stores
- Prompt templates
- Chains (orchestration)

Related ecosystem:
- LangChain → RAG
- LangGraph → Agents
- LangSmith / LangFuse / LangWatch → Observability

---

## 8. Talking to LLMs via API
- Use OpenAI / Anthropic via API (not chat UI)
- Keys stored securely (secrets manager)
- Control:
  - Model
  - Temperature
  - Max tokens
  - Timeouts & retries

### Token Control
- `max_tokens` limits output length
- Billing based on tokens generated
- Inference costs are low (pennies)

---

## 9. LLM Limitations Demonstrated
- ❌ Cannot answer real-time questions
- ❌ Cannot access private data
- ✅ Can answer historical/general knowledge

➡️ Add **tools** → model becomes an **agent**  
➡️ Add **RAG** → access private/internal data

---

## 10. Prompt Structure (Critical)

### Message Types
1. **System Message**
   - Instructions, role, constraints
2. **User Message**
   - Actual question
3. **AI Message**
   - Model response (conversation memory)

System messages **override** user intent.

---

## 11. Prompt Templates & Chaining
- Prompts can be parameterized
- Example variables:
  - Input language
  - Output language
  - Question
- Prompt + Model = **Chain**

This is the foundation of LangChain workflows.

---

## 12. Hands-On Demo: Resume Screening Chatbot

### Pipeline
- PDF resume → chunks
- OpenAI embeddings
- Vector DB (FAISS / Chroma / Pinecone)
- Retriever (Top-K search)
- Prompt with strict instructions
- GPT-mini as LLM

### Key System Instructions
- Answer only from provided context
- If info missing → say so
- Be concise
- Do not hallucinate

---

## 13. Why Results May Be Wrong
If answers are poor:
- Chunking strategy incorrect
- Context split mid-concept
- Top-K too high/low
- Prompt too weak
- Model choice suboptimal

---

## 14. Chunking Strategies (Very Important)

There is **no single best strategy**.

Common approaches:
- Fixed-size (with overlap)
- Sentence-based
- Paragraph-based
- Page-based
- Section-based (ideal for resumes/reports)
- Entity-based
- Table-aware
- Token-based
- Hybrid chunking

➡️ Chunking must match **document structure**

---

## 15. Evaluation & Tuning Loop
Production RAG requires evaluation:

1. Create ground truth manually
2. Ask same questions to RAG app
3. Compare outputs
4. Use **LLM-as-a-Judge**
5. Measure:
   - Accuracy
   - Completeness
   - Faithfulness
6. Tune:
   - Chunking
   - Retrieval
   - Prompt
   - Model

---

## 16. Guardrails
Applied before input & output:
- Mask PII (email, phone)
- Block sensitive data
- Enforce tone
- Prevent prompt injection

Tools mentioned:
- LlamaGuard (Meta)
- Proctor.ai
- Regex + ML scanners

---

## 17. UI & Deployment
Backend can be exposed via:
- Streamlit
- FastAPI / Flask
- AWS Lambda / Azure Functions
- Docker + Kubernetes

➡️ RAG app = standard web service

---

## 18. From RAG → Agentic Systems
Resume chatbot = **single-agent**

Future evolution:
- Resume ingestion agent
- Job description analysis agent
- Matching & scoring agent
- Interview scheduling agent
- Calendar & email integration
- Decision support agent

➡️ This is where **Agentic AI begins**

---

## 19. Key Takeaways
- RAG is foundational for enterprise AI
- Semantic search alone is insufficient
- Retrieval + chunking quality matters more than model size
- Evaluation & guardrails are mandatory
- RAG naturally evolves into multi-agent systems

---

## 20. Next Steps
- Add UI
- Add observability
- Add guardrails
- Expand into multi-agent workflows
