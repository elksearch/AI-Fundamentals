# AI / ML / DL / GenAI — Fundamentals

## The Hierarchy

```
AI (outermost)
└── Machine Learning (ML)
    └── Deep Learning (DL)
        └── Foundation Models
            └── LLM (Large Language Models)
                └── Your Application
```

---

## Artificial Intelligence (AI)

- Machine simulating human intelligence
- **Rules-based AI** — humans write explicit rules, machine follows them
- Example: Airport security system flagging suspicious behaviour based on programmed rules
- **Limitation** — rules only cover what you thought of in advance, cannot scale, breaks when something new appears

---

## Machine Learning (ML)

- Machine learns rules itself from data
- You give examples (labelled or unlabelled), machine finds patterns
- Example: Bank trains model on past approved/rejected loans → predicts new loan approval
- **Key difference from AI** — you don't write rules manually, machine derives them

---

## Deep Learning (DL)

- ML using brain-like structure (Neural Networks)
- Machine finds its own features from raw data automatically
- Handles unstructured data — images, audio, raw text
- Example: Detecting tumour in X-ray, voice recognition, self-driving cars

---

## Comparison Table

| | Who writes rules? | Who picks features? |
|---|---|---|
| AI (rules-based) | You | You |
| ML | Machine | You |
| DL | Machine | Machine |

---

## Generative AI (GenAI)

- AI that **generates** new content token by token
- Always doing one thing: **predict the most likely next token**
- Same mechanism whether writing email, answering question, writing code
- Examples: ChatGPT, Claude, Gemini, DeepSeek

### All tasks = next token prediction:

| Task | What's happening |
|---|---|
| "Virat → Kohli" | Predicting next token |
| Answering a question | Predicting next token |
| Writing code | Predicting next token |
| Translating language | Predicting next token |
| Summarising document | Predicting next token |

---

## Foundation Models

Large pre-trained DL models — base for everything

| Type | What it handles | Example |
|---|---|---|
| LLM | Text | Claude, GPT, DeepSeek |
| Vision | Images | Google Vision, CLIP |
| Speech | Audio | Whisper, Google Speech |
| Diffusion | Image generation | DALL-E, Stable Diffusion |

---

## Major LLM Companies

| Company | Model | Unique Angle |
|---|---|---|
| Anthropic | Claude | Safety focused, Constitutional AI |
| OpenAI | GPT | First mover, largest ecosystem |
| Google | Gemini | Multimodal from ground up |
| Meta | Llama | Open source, free to use |
| DeepSeek | DeepSeek | Built at fraction of cost |

---

## Types of AI by Capability

```
Narrow AI → Limited Memory (where we are today)
AGI        → Theory of Mind (partially emerging)
Super AI   → Self Aware (purely theoretical)
```

| Type | Status | Example |
|---|---|---|
| Reactive Machine | ✅ Exists | Chess engines, rule-based systems |
| Limited Memory | ✅ Exists | All LLMs, self-driving, recommendations |
| Narrow AI | ✅ Exists | Every AI product today |
| AGI | ⚠️ Partial | LLMs simulate but don't truly understand |
| Super AI | ❌ Does not exist | Purely theoretical |

---

## Realized vs Theoretical AI

- **Realized AI** — Exists today: Narrow AI, Limited Memory
- **Theoretical AI** — Does not fully exist: AGI, ASI

---

## Three Types of Intelligence

| Type | Description | Example |
|---|---|---|
| Artificial | Machine only, no human | Highway self-driving |
| Human | Human only, no machine | Driving narrow village lanes |
| Augmented | Human + Machine together | Driver + collision detection |

**Key insight:** Most real-world AI today is Augmented Intelligence — not full replacement but enhancement of human capability.

---

## 5 Myths of AI

| # | Myth | Reality |
|---|---|---|
| 1 | Shortcuts work | Foundation models need proper training |
| 2 | Only DL is AI | Traditional ML still valid and powerful |
| 3 | AI answers everything | Explainability is critical |
| 4 | AI = cost cutting | AI creates new capabilities beyond cost |
| 5 | AI = fraud detection | AI spans every industry |

---

## DIKW Framework

```
🔺 WISDOM    → Requires Judgement (AI struggles here)
   KNOWLEDGE → Requires Interpretation
   INFO      → Requires Context
   DATA      → Raw numbers (AI handles perfectly)
```

Where AI sits today:
- Data, Information, Knowledge → ✅ Handles well
- Wisdom (Judgement) → ❌ Still a genuine challenge
