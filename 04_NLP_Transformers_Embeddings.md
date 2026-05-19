# NLP, Transformers & Embeddings

## NLP — Natural Language Processing

NLP converts unstructured human language to structured data and back.

```
Unstructured Input → [NLP] → Structured Data → [AI Model] → Structured Output → [NLP] → Unstructured Response
```

### NLU — Natural Language Understanding
Converts **unstructured → structured**

Example:
```
"Add eggs and milk to my shopping list"
→ <shopping_list>
    <item>eggs</item>
    <item>milk</item>
  </shopping_list>
```

### NLG — Natural Language Generation
Converts **structured → unstructured**

Steps:
1. **Content Planning** → decide what to say
2. **Sentence Planning** → decide how to structure
3. **Lexical Choice** → pick the right words
4. **Grammar & Syntax** → apply proper grammar
5. **Surface Realisation** → final human-readable text

**Every LLM response you read is NLG in action.**

---

## NLP Pipeline Flow

```
Raw Text
    ↓
Tokenization → break text into tokens
    ↓
Stop Word Removal → remove "the", "and", "were"
    ↓
Stemming OR Lemmatization
    ↓
Part of Speech Tagging
    ↓
NER (Named Entity Recognition)
    ↓
Feed clean tokens into AI model
```

---

## Tokenization

Breaking text into tokens (chunks the model understands).

```
"instance * are located on unhealthy allocator(s)"
→ ["instance", " *", " are", " located", " on",
   " unhealthy", " alloc", "ator", "(s)"]
```

Every token converted to a **number (token ID)** — model only understands numbers.

### Token Size Reference:
```
1 word     ≈ 1-2 tokens
1 sentence ≈ 15-20 tokens
1 page     ≈ 400-500 tokens
50 pages   ≈ 20,000-25,000 tokens
```

---

## Stemming vs Lemmatization

Both are text reduction techniques — same goal, different approach.

### Stemming — crude, fast, chops the word
```
running  → run
flies    → fli    ← not a real word (doesn't matter)
studies  → studi  ← not real
caring   → car    ← wrong meaning!
```

### Lemmatization — smart, finds root meaning
```
running  → run    ✅
flies    → fly    ✅ correct root
studies  → study  ✅ correct root
caring   → care   ✅ correct root
better   → good   ✅ understands comparative
```

**One line:** Stemming chops blindly. Lemmatization understands.

| | Stemming | Lemmatization |
|---|---|---|
| Speed | Fast | Slower |
| Accuracy | Lower | Higher |
| Real words | Not always | Always |
| Use when | Speed matters | Meaning matters |

---

## NLP Applications

1. Machine Translation
2. Virtual Assistants / Chatbots
3. Sentiment Analysis
4. Spam Detection

---

## Embeddings

Converting text/words into **mathematical vectors** (lists of numbers) that capture **meaning**.

```
"Server is down" → [0.23, 0.87, 0.45, 0.12, ... 1536 numbers]
```

### Embedding Dimensions by Model:
| Model | Dimensions |
|---|---|
| OpenAI embeddings | 1536 |
| Google embeddings | 768 |
| Sentence-BERT | 384 |
| Custom small models | 64-128 |

### Why so many numbers?
Each number captures a different aspect of meaning — topic, sentiment, context, domain, relationships. More dimensions = richer meaning captured.

### Semantic Similarity:
```
"Server crashed"     → [0.23, 0.87, 0.45...]
"System went down"   → [0.24, 0.85, 0.46...]
                             ↑
                       Very close numbers
                       = similar meaning
```

---

## Transformer Architecture

Introduced by Google in 2017 — paper: **"Attention Is All You Need"**

### Problem with pre-Transformer models:
```
"The bank by the river was steep"
Read word by word:
The → bank → by → the → river...
By time it reaches "steep" — lost context of "river"
= "bank" misinterpreted as financial bank
```

### Transformer solution — Attention Mechanism:
Reads **everything simultaneously** — understands relationships between ALL words at once.

```
"The bank by the river was steep"
Attention sees: bank ←→ river (strong connection)
= river bank ✅

"The bank approved my loan yesterday"
Attention sees: bank ←→ loan ←→ approved
= financial bank ✅

Same word, different meaning — correctly identified from context
```

---

## Real World Transformer Examples

### 1. Text Generation (Claude, GPT)
Legal document drafting — understands "NDA" + "software startup" context simultaneously

### 2. Translation (Google Translate)
Reads entire sentence, not word by word — context-aware output

### 3. Code Generation (GitHub Copilot)
Comment → complete working function with parameter validation

### 4. Image Recognition (Vision Transformer)
Looks at entire image at once — attention focuses on suspicious shapes

### 5. Medical Diagnosis (BioBERT)
Reads all symptoms simultaneously — recognises patterns across entire patient profile

### 6. Search (Google BERT)
Understands search intent, not just keywords

---

## Transformer vs Hallucination — Important Distinction

```
Transformer solved → context understanding within sentence
                     "bank" near "river" = river bank ✅

Transformer did NOT → eliminate hallucinations
solve
```

| Problem | Solved By | Status |
|---|---|---|
| Context within sentence | Transformer Attention | ✅ Solved |
| Word relationship understanding | Embeddings + Attention | ✅ Solved |
| Hallucination | RAG, RLHF, Grounding | ⚠️ Partially solved |

**Hallucination = right understanding of question, wrong answer from memory**

---

## Context Window

Fixed size "tray" — everything must fit inside.

| Model | Context Window |
|---|---|
| Early GPT | 4,000 tokens |
| GPT-4 | 128,000 tokens |
| Claude | 200,000 tokens |
| Gemini 1.5 | 1,000,000 tokens |

### What happens during generation of 50 pages:
```
Token 1 generated → added to context
Token 2 predicted using context + token 1
Token 3 predicted using everything before it
... 25,000 times for 50 pages

Speed: ~50-100 tokens/second on modern systems
50 pages ≈ 5-6 minutes to generate
```

### Context overflow:
If input + output exceeds limit → oldest content dropped → model loses early context — that's why long conversations sometimes feel like Claude "forgot" something.

---

## Why Wrong Context is Near Zero (but never exactly zero)

5 layers working together to prevent wrong context:

| Mechanism | How it helps |
|---|---|
| Attention | Reads all words together, not in isolation |
| Training data | Correct context seen millions of times |
| Conversation history | Anchors model firmly in correct domain |
| Temperature | Low = stick to high probability tokens |
| System prompt | Invisible guardrails from Anthropic |

**Hallucination still possible** — correct question understanding, wrong answer from training gaps.
