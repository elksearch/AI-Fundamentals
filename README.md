# 🤖 AI Knowledge Repository

Started from absolute zero — no prior AI/ML knowledge.

---

## 📚 Contents — In Learning Order

| # | File | Topics Covered |
|---|---|---|
| 01 | [01_AI_History_Timeline.md](01_AI_History_Timeline.md) | Turing Test, ELIZA, Deep Blue, Watson, ChatGPT, AI timeline 1950-2025 |
| 02 | [02_AI_ML_DL_GenAI_Fundamentals.md](02_AI_ML_DL_GenAI_Fundamentals.md) | AI/ML/DL hierarchy, GenAI, Foundation Models, Types of AI, DIKW, 5 Myths |
| 03 | [03_ML_Learning_Types.md](03_ML_Learning_Types.md) | Supervised, Unsupervised, Semi-Supervised, Reinforcement, Self-Supervised, Model size |
| 04 | [04_NLP_Transformers_Embeddings.md](04_NLP_Transformers_Embeddings.md) | NLP/NLU/NLG, Tokenization, Stemming, Lemmatization, Transformer, Attention, Context Window |
| 05 | [05_RAG_VectorDB_FineTuning.md](05_RAG_VectorDB_FineTuning.md) | RAG pattern, Vector DB, Fine Tuning, PEFT, LoRA, Local RAG stack |
| 06 | [06_MCP_gRPC_API_Protocols.md](06_MCP_gRPC_API_Protocols.md) | REST API, MCP, gRPC, HTTP/1.1 vs HTTP/2, Protocol comparison, Claude end-to-end flow |
| 07 | [07_AI_Stack_LangChain_Orchestration.md](07_AI_Stack_LangChain_Orchestration.md) | 5 Layer AI Stack, LangChain, Orchestration tools, MoE, DeepSeek |
| 08 | [08_AI_Terminology_QuickReference.md](08_AI_Terminology_QuickReference.md) | Agentic AI, LRM, ASI, Hallucination, Prompt Engineering, All concepts connected |

---

## 🗺️ Why This Order?

```
01 — History first
     Understand HOW and WHY AI evolved
     Sets context for everything that follows

02 — Fundamentals
     What is AI, ML, DL, GenAI?
     The hierarchy and relationships

03 — How Machines Learn
     Supervised, Unsupervised, Reinforcement
     Training types and techniques

04 — How Language is Processed
     NLP pipeline, Transformers, Embeddings
     The engine behind LLMs

05 — How to Add Your Own Data
     RAG, Vector DB, Fine Tuning
     Connecting AI to your private data

06 — How AI Talks to the World
     MCP, gRPC, REST API
     Protocols connecting AI to external systems

07 — The Full AI Stack
     Infrastructure to Application
     LangChain, Orchestration, MoE

08 — Quick Reference
     All terminology in one place
     Use this for revision
```

---

## 🔑 Key Mental Models

### The Hierarchy:
```
AI → ML → DL → Foundation Models → LLM → Your App
```

### GenAI is always:
```
Predicting the next most likely token
(whether answering questions, writing code, or translating)
```

### RAG is a pattern:
```
Any external data retrieved + injected into prompt at query time
Not just for documents — works for chat history, databases, web
```

### Protocol layers:
```
HTTPS/REST → You talking to Claude (simple, readable)
MCP        → Claude talking to external tools (AI purpose built)
gRPC       → Internal microservices talking to each other (fast, binary)
```

### Where things run:
```
LLM Model   → Heavy GPU (cloud or on-prem)
LangChain   → Lightweight CPU (your app server)
Vector DB   → CPU with good RAM and SSD
```

### Larger ≠ Better:
```
Right LLM = Right use case match
Not biggest model available

Domain specific task → Small domain-tuned model
General reasoning    → Larger general model
```

---

## 📅 Learning Status

- [x] 01 — AI History Timeline
- [x] 02 — AI/ML/DL/GenAI Fundamentals
- [x] 03 — ML Learning Types
- [x] 04 — NLP, Transformers, Embeddings
- [x] 05 — RAG, Vector DB, Fine Tuning
- [x] 06 — MCP, gRPC, API Protocols
- [x] 07 — AI Stack, LangChain, Orchestration
- [x] 08 — AI Terminology Quick Reference
- [ ] AI Academy playlist (in progress)
- [ ] AI Technical Tutorials playlist
- [ ] AI Agents Explained playlist

---

## 🛠️ Tools & Frameworks Referenced

| Category | Tools |
|---|---|
| Local LLM | Ollama, LM Studio |
| Orchestration | LangChain, LlamaIndex, CrewAI, AutoGen, LangGraph |
| Vector DB | ChromaDB, Pinecone, Weaviate, Elasticsearch |
| Embedding | nomic-embed-text, Sentence-BERT, OpenAI Embeddings |
| Fine Tuning | Hugging Face, Unsloth, LLaMA-Factory |
| PEFT | LoRA, QLoRA |
| PDF Processing | PyPDF2, pdfplumber, Apache Tika |
| Protocols | REST/HTTP, MCP (JSON-RPC 2.0), gRPC |

---

## 📖 Source

IBM Technology YouTube — AI Fundamentals Playlist
https://www.youtube.com/playlist?list=PLOspHqNVtKADfxkuDuHduUkDExBpEt3DF

*Personal notes — not official IBM documentation*
