# AI Stack, LangChain & Orchestration

## The 5 Layer AI Stack

```
┌─────────────────────────────────────────┐
│  APP LAYER (Top)                        │
│  What users see and interact with       │
├─────────────────────────────────────────┤
│  ORCHESTRATION LAYER                    │
│  Connects everything together           │
├─────────────────────────────────────────┤
│  DATA LAYER                             │
│  Feeds AI with your information         │
├─────────────────────────────────────────┤
│  MODEL LAYER                            │
│  The AI brain (LLM)                     │
├─────────────────────────────────────────┤
│  INFRA LAYER (Bottom)                   │
│  Where everything runs                  │
└─────────────────────────────────────────┘
```

---

## Layer 1 — INFRA (Infrastructure)

### Deployment Options:
```
On-Premise  → Your own data center
              Full control, data never leaves
              High upfront cost

Cloud       → AWS, Azure, GCP
              Scalable, pay as you go
              Data goes to vendor

Local       → Your own laptop/workstation
              Development and testing
```

### Hardware:
- GPUs/TPUs → for model training and inference
- Servers → compute power
- Storage → training data and models
- Kubernetes/Docker → container orchestration

### GPU Memory by Model Size:
```
7B model   → 8GB VRAM
13B model  → 16GB VRAM
70B model  → 80GB+ VRAM
175B model → Multiple GPUs
```

---

## Layer 2 — MODEL

### Open vs Proprietary:

| Open Source (Free) | Proprietary (Paid) |
|---|---|
| Llama (Meta) | GPT-4 (OpenAI) |
| Mistral | Claude (Anthropic) |
| DeepSeek | Gemini (Google) |
| Falcon | IBM Granite (some) |
| You host it yourself | Vendor hosts it |
| Full control | API access only |
| Data stays local | Data goes to vendor |

### Embedded AI — Library vs Application:

| Approach | Data | Cost | Control |
|---|---|---|---|
| Library (on-prem) | Never leaves | Higher upfront | Full control |
| Application (SaaS) | Goes to vendor | Lower upfront | Limited |

---

## Layer 3 — DATA

### Three Components:
```
Data Sources → PDFs, databases, APIs, emails, documents

Pipelines    → Extract → Clean → Chunk → Embed → Store
               Similar to ETL pipelines in IT world

Vector DBs   → Where processed data stored for RAG
+ Retrieval    Similarity search at query time
```

---

## Layer 4 — ORCHESTRATION

### The Agentic Loop:
```
THINK → EXECUTE → REVIEW
  ↑                  |
  └──────────────────┘
  Loop until task complete
```

```
THINK   → LLM reasons about what to do next
EXECUTE → Calls tools via MCP
REVIEW  → LLM evaluates result, loops if needed
```

### Orchestration Tools:

| Tool | Best For |
|---|---|
| LangChain | General purpose, most popular |
| LlamaIndex | RAG heavy applications |
| AutoGen | Multi-agent conversations (Microsoft) |
| CrewAI | Team of specialised agents |
| LangGraph | Complex workflow graphs |
| IBM watsonx | Enterprise, governance focused |

---

## Layer 5 — APP (Application)

### Interfaces:
- Text, Image, Audio, Numerical
- Revisions, Citations

### Integrations:
- **Inputs** → CRM data, documents, databases, user uploads
- **Outputs** → Email, Slack, reports, database updates, API calls

---

## LangChain — What, Where, When

### What LangChain Is:
```
LangChain = Python library (plain software code)
= No GPU needed
= Runs on normal CPU server
= Very lightweight
= Pre-built glue code connecting components
```

### Where LangChain Runs:
```
YOUR APPLICATION SERVER (Normal CPU)    ← LangChain lives here
├── LangChain Python code
├── RAG pipeline code
├── Memory management
├── Tool calling logic
└── Prompt building
           ↓ HTTP API call
LLM SERVER (Heavy GPU)                  ← Model lives here
├── Cloud: Anthropic/OpenAI
└── Local: Ollama on your GPU server
```

**LangChain NEVER runs on Anthropic/OpenAI servers.**

### How LangChain Connects to Model:
```python
# Cloud LLM:
from langchain_anthropic import ChatAnthropic
llm = ChatAnthropic(model="claude-sonnet-4-20250514")

# Local LLM:
from langchain_ollama import OllamaLLM
llm = OllamaLLM(model="llama3", base_url="http://localhost:11434")

# Same LangChain code — just different endpoint
# Switch from cloud to local by changing one line
```

### When LangChain is Needed vs Not:

| Scenario | LangChain Needed? |
|---|---|
| Simple chat with OpenAI/Claude API | ❌ No |
| Simple chat with local Ollama | ❌ No |
| RAG with your own documents | ✅ Yes (or build yourself) |
| Multiple tools (search+email+DB) | ✅ Yes |
| AI Agent with Think/Execute loop | ✅ Yes |
| Multi-step complex workflows | ✅ Yes |
| Memory across sessions | ✅ Yes |

---

## Conversation Memory — What Handles What

### Within Same Session (Turn by Turn):
```
API handles this natively — NOT LangChain

Every request includes full history:
[
  {"role": "user", "content": "What is ML?"},
  {"role": "assistant", "content": "ML is..."},
  {"role": "user", "content": "Give example?"}
]
API reads full history → responds in context
```

### Across Sessions ("remember last week"):
```
Claude.ai / ChatGPT:
Each new chat = fresh start
Zero memory of previous conversations

Solutions:
1. Platform memory (Claude.ai built-in)
   → Key facts only, limited
   → Not full history, not searchable by date

2. Custom app + LangChain:
   → Every conversation saved to database
   → LangChain fetches relevant past chats
   → Injects into context as RAG
   → Full control, full history
```

### Complete Picture:

| Scenario | Who Handles It |
|---|---|
| Turn by turn in same chat | API itself |
| 50 PDFs in one session (fits context) | Context window directly |
| 50 PDFs exceed context window | RAG needed |
| Remember facts across sessions | Platform memory (limited) |
| Full cross-session memory | Custom app + LangChain |

---

## LangChain RAG Code Example

```python
from langchain_anthropic import ChatAnthropic
from langchain_community.vectorstores import Chroma
from langchain_community.embeddings import OllamaEmbeddings
from langchain.chains import RetrievalQA

# Connect to LLM
llm = ChatAnthropic(model="claude-sonnet-4-20250514")

# Connect to Vector DB (already has your PDFs)
vectordb = Chroma(
    persist_directory="./my_documents",
    embedding_function=OllamaEmbeddings()
)

# Build RAG chain — connects retrieval + LLM
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    retriever=vectordb.as_retriever()
)

# Every query automatically:
# → searches vector DB
# → retrieves relevant chunks
# → builds prompt
# → calls Claude
# → returns answer
response = qa_chain.invoke("What is our leave policy?")
```

---

## Fully Local On-Premise Stack

```
[User Interface — Open WebUI]
         ↓
[LangChain — Your App Server (CPU)]
         ↓              ↓
[Ollama API]    [ChromaDB/Elasticsearch]
localhost:11434  localhost:8000
         ↓              ↓
[Llama Model]   [Your PDF vectors]

Everything local. Zero data leaves.
```

---

## MoE — Mixture of Experts

Architecture where multiple specialised sub-models work together.

```
Traditional LLM:
Every query → goes through ALL parameters
Expensive, slow

MoE Model:
Every query → Router decides
├── Expert 1: Science/Math    (87% relevant)
├── Expert 2: Language        (79% relevant)
├── Expert 3: Code            (23% relevant)
└── Expert 4: Reasoning       (12% relevant)
Top-2 activated → outputs weighted + combined
Rest stay idle
= Cheaper, faster, same quality
```

### Multi-topic queries:
- Multiple experts activate simultaneously (Top-K)
- Happens **per token** not per query
- Different tokens can use different expert combinations

### Who Uses MoE:
| Model | Uses MoE? |
|---|---|
| GPT-4 | ✅ Yes (confirmed via leaks) |
| Gemini 1.5/2.0 | ✅ Yes |
| DeepSeek V2/V3 | ✅ Yes (openly documented) |
| Mixtral | ✅ Yes |
| Llama 3 | ❌ Dense model |

### DeepSeek's Real Moat (not just MoE):
```
Better MoE implementation
+ MLA attention compression (less GPU memory)
+ FP8 low precision training (cheaper)
+ Innovation under US chip sanctions
+ Lean team (~150 people)
= Frontier model at 1/30th the cost ($6M vs $100M+)
```
