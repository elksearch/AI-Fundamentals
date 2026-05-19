# MCP, gRPC & API — Protocols Explained

## REST API (Application Programming Interface)

Standard communication between client and server.

```
Client → HTTP Request (GET/POST/PUT/DELETE) → Server
       ← Response ←

Example:
GET  /books/123  → fetch book details
POST /loans      → create new loan
```

- Text based (JSON)
- Human readable
- HTTP/1.1
- You must know endpoints in advance

---

## MCP — Model Context Protocol

**Purpose built for AI Agents.**

Anthropic released MCP as open standard — same way HTTP became standard for web.

### What MCP Server Exposes:
```
MCP Server
├── Tools           → actions AI can perform
│                     (convert file, send email, query DB)
├── Resources       → data AI can read
│                     (files, databases, documents)
└── Prompt Templates → pre-built prompts for common tasks
```

### USB-C Analogy:
```
Before USB-C → different cable for every device
After USB-C  → one cable, works everywhere

Before MCP   → different custom integration for every tool
After MCP    → one protocol, AI connects to anything
```

### MCP Architecture:
```
Host (Claude, ChatGPT)
      ↓
MCP Client
      ↓ JSON-RPC 2.0
MCP Server
      ↓    ↓    ↓
     DB  Code  Files/Email
```

### MCP Communication Format (JSON-RPC 2.0 — Text Based):
```json
{
  "method": "get_weather",
  "params": {"city": "Boston"}
}
```

Human readable, easy to debug.

### Dynamic Self Discovery — Key Feature:
```
REST API → Developer must hardcode:
"I know endpoint /convert exists"

MCP → AI Agent asks MCP Server:
"What tools do you have?"
Server: "I have convert, compress,
         merge, extract tools"
AI picks right one dynamically
No hardcoding needed
```

---

## gRPC — Google Remote Procedure Call

High performance communication for **service to service** communication in distributed systems.

```
Client → HTTP/2 + Protocol Buffers (Binary) → Server

Binary format — NOT human readable
Extremely fast, tiny payload
```

### HTTP/1.1 vs HTTP/2:
```
HTTP/1.1 (REST/MCP):
Request 1 ──────────→ wait → response
Request 2 ──────────────────────→ wait → response
Sequential — one at a time

HTTP/2 (gRPC):
Request 1 ──→
Request 2 ──→  All simultaneously
Request 3 ──→
All responses come back in parallel
Much faster for internal service calls
```

### gRPC Features:
- Protocol Buffers (binary, not readable)
- Bidirectional Streaming
- Code Generation
- HTTP/2 multiplexing

---

## MCP vs API vs gRPC Comparison

| Factor | REST API | MCP | gRPC |
|---|---|---|---|
| Built for | General apps | AI Agents specifically | Microservices |
| Protocol | REST/HTTP | JSON-RPC 2.0 | Protocol Buffers |
| Transport | HTTP/1.1 | HTTP/1.1 or SSE | HTTP/2 |
| Data format | JSON (text) | JSON (text) | Binary |
| Human readable | ✅ Yes | ✅ Yes | ❌ No |
| Speed | Moderate | Moderate | Very fast |
| Tool discovery | ❌ Static | ✅ Dynamic runtime | ❌ Static |
| AI adapter needed | ✅ Yes | ❌ No | ✅ Yes |
| Streaming | Limited | Limited | ✅ Bidirectional |
| Use case | Any app | AI agent→tools | Service→service |

---

## How MCP and gRPC Work Together

They are NOT competing — they are **layers in the same system.**

### Real Example — Flight Booking AI Agent:

```
You → "Book me cheapest flight Mumbai to Dubai"
         ↓ HTTPS/REST (HTTP/1.1, JSON)
Claude (Anthropic Server)
         ↓ MCP Protocol (JSON-RPC 2.0, text)
MCP Server (Middle Layer)
         ↓ gRPC (HTTP/2, Binary)
Flight Search Microservice
         ↓ gRPC
Price Microservice
         ↓ gRPC
Seat Availability Microservice
         ↓ gRPC
Booking Microservice
         ↓ gRPC
Payment Microservice
         ↓ gRPC
Email Microservice
         ↑ response travels back up
Claude → "Your flight is booked!"
```

Each protocol doing what it does best:
- **HTTPS/REST** → You talking to Claude (simple, readable)
- **MCP** → Claude talking to external tools (AI purpose built, dynamic)
- **gRPC** → Internal services talking to each other (fast, binary)

---

## When Claude Uses MCP vs Answers Directly

```
You send request
        ↓
LLM analyses: "Can I answer from training alone?"
        ↓
YES → Answer directly (No MCP)
NO  → Invoke MCP tool
```

### Decision Table:

| Request | MCP? | Why |
|---|---|---|
| "Rephrase this text" | ❌ No | Pure language task |
| "Summarise document" | ❌ No | LLM reads directly |
| "Translate to French" | ❌ No | Built into LLM |
| "Convert Word to PDF" | ✅ Yes | Needs file tool |
| "Send email to John" | ✅ Yes | Needs Gmail access |
| "What is today's weather?" | ✅ Yes | Needs real time data |
| "Search my Google Drive" | ✅ Yes | Needs external access |
| "What is machine learning?" | ❌ No | Already in training |

### Simple Rule:
```
LLM has it internally → Direct response
                        No MCP, no external call

LLM needs something   → MCP invoked
from outside world       Tool discovered
                         Task executed
```

---

## Complete Flow — Claude Answering Your Question

```
Step 1 — Input Capture (~0-50ms)
Text captured → HTTP POST to Anthropic

Step 2 — Network Transit (~50-200ms)
HTTPS to Anthropic's load balancer

Step 3 — Auth & Rate Limiting (~10-30ms)
Session validated, routed to backend

Step 4 — Context Assembly (~20-50ms)
System prompt + conversation history + new question
All packed into one context window

Step 5 — Tokenization (~5-10ms)
Text → token IDs (numbers)

Step 6 — LLM Processing (~1-10 seconds)
Embedding → Attention layers → Feed forward → Output
Predicts one token at a time

Step 7 — Detokenization (~5ms)
Token IDs → readable text

Step 8 — Streaming
Tokens streamed back as generated

Step 9 — Rendering (~10-30ms)
Browser renders markdown, displays answer

Total: ~2-12 seconds end to end
```
