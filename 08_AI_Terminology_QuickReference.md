# AI Terminology — Quick Reference

## 7 Key AI Terminologies

| # | Term | One Line |
|---|---|---|
| 1 | Agentic AI | AI that acts autonomously across multiple steps |
| 2 | LRM (Large Reasoning Model) | AI that thinks step by step before answering |
| 3 | Vector DB | Stores meaning as numbers for similarity search |
| 4 | RAG | LLM + your own data retrieved at query time |
| 5 | MCP | Standard protocol connecting AI to external tools |
| 6 | MoE | Multiple specialist models, router picks right one |
| 7 | ASI | Theoretical AI smarter than humans in every way |

---

## Agentic AI

AI that can plan, decide and act autonomously across multiple steps.

```
Normal AI:
You ask → AI answers → Done

Agentic AI:
"Book me cheapest flight to Dubai next week"
→ AI searches flights
→ Compares prices
→ Checks your calendar
→ Books the ticket
→ Sends confirmation email
→ All by itself, no hand-holding
```

---

## LRM — Large Reasoning Model

Models that think step by step before answering.

```
Normal LLM: Question → Instant answer (fast, can be wrong)

LRM: Question → thinks... → thinks... → structured reasoning
     → then answers (slower but far more accurate)
```

**Examples:** OpenAI o1, o3, DeepSeek R1, Claude with extended thinking

---

## ASI — Artificial Super Intelligence

```
Current AI (ANI):  Excellent at specific tasks
AGI (coming?):     Can do anything a human can do
ASI (theoretical): Exceeds human in EVERY domain
```

**Status:** Does not exist. Purely theoretical.

---

## Types of LLMs by Input/Output

| Input → Output | Type | Example |
|---|---|---|
| Text → Text | Q&A, Chatbot, Summary, Translation | Claude, GPT |
| Text → Image | Image Generation | DALL-E, Midjourney |
| Image → Text | Vision/Image Understanding | GPT-4V, Claude |
| Text → Audio | Text to Speech | ElevenLabs |
| Audio → Text | Speech Recognition | Whisper |
| Text → Video | Video Generation | Sora, Runway |
| Text → Code | Code Generation | Copilot, CodeLlama |
| Any → Any | Multimodal | GPT-4o, Claude 3, Gemini |

**2025 Trend:** One powerful multimodal model replacing many specialised ones.

---

## Confidence Level in AI

```
0% confidence  → AI has no idea → ignore it → low success
50% confidence → uncertain → human reviews → medium success
70-80%         → sweet spot → human + AI → highest success
100% confidence → blindly trust it → dangerous → success drops
```

**Key insight:** High AI confidence ≠ correct answer. AI can be confidently wrong.

### Cognitive Bias:
- **Forced Display** → AI shows recommendation first → human subconsciously follows even if wrong
- **Optional Display** → Human decides first, then checks AI → better independent thinking

---

## Hallucination

AI confidently gives wrong answer.

```
Cause: Gap or error in training data
       NOT a context misunderstanding problem
       (Transformer handles context well)

Prevention:
→ RAG (ground answers in your documents)
→ RLHF (human feedback training)
→ RAG chaining (verify against multiple sources)
→ Always verify critical AI answers
```

---

## Prompt Engineering

How you write your question directly impacts:
- Quality of answer
- Number of tokens consumed (cost)
- Accuracy of response

**Token = Prompt (input) + Completion (output) = Total cost**

---

## AI Timeline

```
1950s-1970s → AI (Expert Systems, LISP/Prolog)
              Rules written by humans
              Machine ≥ Human at chess, logic

1980s       → Expert Systems peak (still rule based)

2000s       → ML + DL emerge
              Neural Networks start working
              SVM, Decision Trees, Random Forest

2017        → Transformer introduced ("Attention Is All You Need")

2020s       → Foundation Models
              LLM, Audio, Video, GenAI
              ChatGPT changes everything (2022)

2024-2025   → Agentic AI, MoE, Reasoning Models
              AI agents acting autonomously
```

---

## All Concepts Connected — Hospital AI Example

```
AI layer
→ Rules: if patient age > 60 + smoker → flag for screening

ML layer
→ Supervised: trained on 1M patient records
  predicts readmission risk

DL layer
→ Analyses X-ray images for tumour detection
→ Transcribes doctor's voice notes to text

Foundation Model layer
→ Pre-trained medical LLM (like Med-PaLM)

GenAI layer
→ Generates patient discharge summary
→ Answers doctor's queries about drug interactions

RAG layer
→ Pulls latest hospital treatment protocols
  into LLM context at query time

Chatbot layer
→ Patient facing bot answers queries 24/7

Anomaly Detection
→ Flags unusual vital signs in ICU data

MCP layer
→ Books follow-up appointments
→ Sends discharge summary to patient email

gRPC layer
→ Internal microservices communicating:
  Patient DB ↔ Lab System ↔ Pharmacy ↔ Billing
```

**All concepts — one system — working together.**

---

## Key Relationships to Remember

```
RAG is a PATTERN:
Any external data retrieved + injected into prompt

LangChain is a TOOL:
Pre-built code implementing RAG and other patterns

MCP is a PROTOCOL:
Standard way for AI to discover + call external tools

gRPC is a TRANSPORT:
Fast binary protocol for internal service communication

Transformer is an ARCHITECTURE:
Neural network design that reads entire context at once

Embedding is a REPRESENTATION:
Text converted to numbers capturing meaning

Vector DB is a STORAGE:
Stores embeddings, enables similarity search

Foundation Model is a BASE:
Pre-trained on massive data, others build on top

Fine Tuning is SPECIALISATION:
Adapting foundation model to specific domain

PEFT is EFFICIENT FINE TUNING:
Retraining tiny fraction of parameters only
```

---

## DIKW vs AI Capability

| Level | Example | AI Status |
|---|---|---|
| Data | 10, 5, 4, 3, 8 | ✅ Handles perfectly |
| Information | "These are ages" | ✅ Handles well |
| Knowledge | "If age < 21, cannot enter" | ✅ Handles well |
| Wisdom | "Should I let this person in?" | ❌ Still a challenge |

---

## Current AI Limits (2025)

```
✅ Achieved:
- Reasoning (basic to advanced)
- NLP (since 1965, matured 2011)
- Creation (text, image, code, audio, video)
- Robotics assistance

⚠️ Questionable:
- EQ (Emotional Intelligence)
- Hallucination (improving but not solved)
- Common sense
- Judgement

❌ Not achieved:
- AGI (Theory of Mind)
- ASI (Self Aware)
- True emotional understanding
- Micro/Macro goals
- Deep sensations
- Sustainability at scale
```
