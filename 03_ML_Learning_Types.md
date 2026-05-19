# Machine Learning — Learning Types & Techniques

## Overview

```
Machine Learning Training
├── Supervised Learning
├── Unsupervised Learning
├── Semi-Supervised Learning
├── Self-Supervised Learning
└── Reinforcement Learning
```

---

## 1. Supervised Learning

**Labelled data — you know the output**

### Regression — predict a number
- **Linear** → straight line relationship
  - Example: House size → predict price
- **Polynomial** → curved relationship
  - Example: Car speed vs fuel consumption

### Classification — predict a category
- **Binary** → 2 outcomes only
  - Example: Email → Spam or Not Spam, Loan → Approve or Reject
- **Multi-Class** → 3+ outcomes
  - Example: Photo → Cat, Dog, or Bird?

---

## 2. Unsupervised Learning

**No labels — machine finds patterns itself**

### Clustering — group similar things
- **K-Means** → divide data into K groups
  - Example: Hospital groups patients by symptoms automatically
- **Hierarchical** → nested groupings
  - Example: Grouping news articles by topic

### Dimensionality Reduction — simplify data
- **PCA** (Principal Component Analysis) → compress features
  - Example: Patient has 500 test results → PCA reduces to 10 key indicators
- **Autoencoders** → neural network compression
  - Example: Compressing medical images

### Association Rule Learning — find relationships
- Example: "People who buy bread also buy butter" — recommendation engines

### Anomaly Detection — find outliers
- Example: Fraud detection, server failure prediction
- **Most commonly Unsupervised** — no labelled anomaly data needed
- Can also be Supervised (if historical labelled anomalies exist)
- Or Semi-Supervised (mostly normal + few labelled anomalies)

### Generative Models — create new data
- Example: GANs generate fake images

---

## 3. Semi-Supervised Learning

**Mix — small labelled + large unlabelled data**

- Example: Google Photos — you label 10 photos of a person, it finds all others
- Practical when labelling is expensive but raw data is cheap

---

## 4. Self-Supervised Learning

**No human labels — model creates its own labels from data**

- **This is how LLMs are trained**
- GPT trained by hiding a word and asking model to predict it
- Label is generated from data itself — no human labelling needed at scale
- Example: "The cat sat on the ___" → model predicts "mat"

---

## 5. Reinforcement Learning

**No labels — learn by trial, error, reward and penalty**

```
STATE   → current situation AI is in
ACTION  → what AI decides to do
REWARD  → positive feedback for good action
PENALTY → negative feedback for bad action
```

### Techniques:
- **Q-Learning** → learn best action per situation
- **Deep Q-Network (DQN)** → Q-Learning using Deep Learning
- **Policy Gradient** → directly optimise action strategy
- **Actor-Critic** → combines above two approaches

**Used in:** game playing AI, robotics, self-driving cars, AlphaGo

---

## Foundation Model Training — Which Types Used?

```
Self-Supervised Learning (primary)
→ Model creates own labels from data
→ "Predict the next word"
→ No human labelling needed at scale
→ Trained on trillions of words

Reinforcement Learning from Human Feedback (RLHF)
→ Humans rate model responses
→ Good response → reward
→ Bad response → penalty
→ How ChatGPT, Claude were refined

Supervised Learning (fine tuning phase)
→ Small curated labelled dataset
→ Align model behaviour after pre-training
```

---

## Anomaly Detection — Which ML Type?

| Approach | When Used |
|---|---|
| Unsupervised | No labelled data — most common |
| Supervised | Have historical labelled anomalies |
| Semi-Supervised | Mostly normal data + few labelled anomalies |

**In Elasticsearch:** ML anomaly detection uses unsupervised learning — learns baseline behaviour automatically, no labelling required.

---

## Larger ≠ Better — Model Size Decision

| Factor | Small Domain Model (13B) | Large General Model (175B) |
|---|---|---|
| Cost | Much lower | Very high |
| Latency | 3x faster | Slower |
| Accuracy (domain) | 0.57 | 0.59 |
| GPU hours | 1/10th | Baseline |

**Key insight:** 0.02 accuracy difference for 10x cost — not worth it for domain specific tasks.

### Decision Framework:
```
Domain specific task → Small domain-tuned model ✅
General reasoning   → Larger general model ✅
Real-time response  → Smaller model ✅
Budget constrained  → Smaller model ✅
```

---

## 7 Steps to Choose and Use an LLM

| Step | What | Key Decision |
|---|---|---|
| 1 | Use Case | What problem are you solving? |
| 2 | Model Size | Small (11B) vs Large (70B)? |
| 3 | Pre-Train | Use existing — costs $4.6M+ from scratch |
| 4 | Inferencing | Token = 3/4 word, master prompt engineering |
| 5 | Tuning | Fine Tune (all params) vs PEFT (tiny fraction) |
| 6 | Hosting | API (pay/token) vs Self-host (pay/hour) |
| 7 | Deployment | Cloud vs On-premise GPU |

### Tuning Options:
```
Fine Tune → retrains ALL parameters
            needs 100,000+ data points
            expensive, days to complete

PEFT      → retrains tiny fraction (100s-1000s params)
            much cheaper and faster
            LoRA is most popular PEFT technique
```
