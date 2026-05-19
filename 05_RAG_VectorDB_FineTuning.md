# RAG, Vector Database & Fine Tuning

## The Core Problem

Pretrained LLMs (Llama, GPT, Claude) are trained on general internet data — NOT your company's private documents.

```
Question: "What is our leave policy?"
LLM has no idea → needs your HR policy document

Solution options:
1. Use As-Is     → works only for general tasks
2. RAG           → inject your data at query time
3. Fine Tuning   → bake your data into the model
```

---

## Option 1 — Use As-Is

Just use the pretrained model for general tasks.

**When to use:** Tasks that don't need your private data.
**Example:** HR team using Llama to draft job descriptions — no company data needed.

---

## Option 2 — RAG (Retrieval Augmented Generation)

**Most popular approach in enterprises today.**

You do NOT retrain the model. At query time:
1. Search your documents for relevant content
2. Inject that content into the prompt as context
3. LLM answers using both its training + your data

### RAG is a PATTERN — not just for documents:

| Source | Type |
|---|---|
| Documents/PDFs | Document RAG |
| Conversation history | Memory RAG |
| Database records | Structured RAG |
| Web search results | Web RAG |
| Emails/Calendar | Personal RAG |

**Any external data retrieved and injected into prompt = RAG**

---

## RAG — Phase 1: One Time Setup

```
Step 1 → Collect documents
         PDFs, databases, emails, SOPs

Step 2 → Chunk documents
         Split into ~500 word pieces
         Why? Model context window has limits

Step 3 → Convert chunks to Embeddings
         Each chunk → mathematical vector
         "Leave policy allows 20 days..."
         → [0.23, 0.87, 0.45, 0.12, ...]
         Done by Embedding Model (separate from LLM)

Step 4 → Store in Vector Database
         Vectors + original text stored together
         Examples: Pinecone, ChromaDB,
                   Weaviate, Elasticsearch
```

---

## RAG — Phase 2: Every User Query

```
User asks: "How many annual leave days do I get?"
        ↓
Convert question to vector (same embedding model)
        ↓
Similarity Search in Vector DB
Find chunks whose vectors are CLOSEST
to question vector = semantic search
        ↓
Retrieve top 3-5 most relevant chunks
        ↓
Build prompt with context:
"Using the following company documents:
[Chunk 1 text]
[Chunk 2 text]
Answer: How many annual leave days?"
        ↓
Send to LLM (Llama/GPT/Claude)
        ↓
LLM answers using YOUR data
        ↓
Return answer to user
```

---

## RAG Eagle View Architecture

```
[User Question]
      ↓
[Embedding Model] → converts question to vector
      ↓
[Vector Database] → finds similar document chunks
      ↓
[Prompt Builder]  → question + retrieved chunks
      ↓
[LLM]             → generates answer
      ↓
[User gets answer grounded in company data]
```

---

## RAG vs Fine Tuning — When to Use Which?

| Situation | Best Choice |
|---|---|
| Data changes frequently | RAG ✅ |
| Data is stable, rarely changes | Fine Tuning ✅ |
| Need model to learn your writing style | Fine Tuning ✅ |
| Need latest company docs | RAG ✅ |
| Budget is limited | RAG ✅ |
| Need deep domain terminology | Fine Tuning ✅ |

**Most enterprises combine both:**
- Fine tune for domain terminology and tone
- RAG for live, changing company data

---

## Why RAG Preferred Over Fine Tuning for Dynamic Data

```
Company policy updated today

Fine Tuning approach:
→ Must retrain model again
→ Takes days + costs money
→ Policy updated again next week
→ Retrain again...

RAG approach:
→ Just update document in database
→ Done. No retraining needed.
→ Next query automatically picks new policy
```

---

## Option 3 — Fine Tuning

Take pretrained model and **additionally train it on your specific data.**

```
Pretrained Llama (general knowledge)
        +
Your company data (additional training)
        =
Fine tuned model (general + your domain)
```

### Fine Tuning Steps:
```
Step 1 → Extract text from PDFs
         Tools: PyPDF2, Apache Tika, pdfplumber

Step 2 → Clean the data
         Remove headers, footers, encoding issues

Step 3 → Format into Q&A training pairs
         {
           "question": "How to restart server?",
           "answer": "Requires admin approval via ticket"
         }
         Hundreds/thousands of pairs needed

Step 4 → Fine Tune the Model
         Framework: Hugging Face, Unsloth, LLaMA-Factory
         Takes hours to days on GPU

Step 5 → Evaluate the model
         Test if model answers correctly

Step 6 → Deploy fine tuned model
```

### PEFT — Parameter Efficient Fine Tuning
Instead of retraining ALL billions of parameters — retrain only a tiny fraction.

```
Fine Tune:
Retrains all parameters → expensive, days
Needs 100,000+ data points

PEFT (e.g. LoRA):
Retrains 100s-1000s of parameters only
Much cheaper and faster
Same quality result
```

---

## Vector Database Deep Dive

Stores data as mathematical vectors enabling **similarity/semantic search** — not keyword matching.

```
"annual leave days" will match
"yearly vacation entitlement"
even though words are different
= semantic understanding
```

### Tools:
| Tool | Type | Notes |
|---|---|---|
| Pinecone | Cloud | Managed, easy to start |
| ChromaDB | Local | Simplest, runs locally |
| Weaviate | Both | Lightweight, local friendly |
| Elasticsearch | Both | You already know this! Native vector search |

**Interesting:** Elasticsearch has native vector search — your ELK expertise is directly applicable to RAG pipelines.

---

## Local RAG Stack — 100% On-Premise

| Component | Tool |
|---|---|
| LLM | Ollama (Llama/Mistral) |
| Embedding Model | nomic-embed-text via Ollama |
| Vector Database | ChromaDB or Elasticsearch |
| Orchestration | LangChain or LlamaIndex |
| UI | Open WebUI |
| PDF Extraction | PyPDF2 or pdfplumber |

**Zero cloud dependency. Zero data leaves your infrastructure.**
