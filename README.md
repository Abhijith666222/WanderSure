<div align="center">

# ✈️ WanderSure

### **Conversational travel insurance that actually gets you.**

*No forms. No fine print hunting. Just talk.*

[![MSIG](https://img.shields.io/badge/MSIG-Conversational%20Insurance-0066B3?style=flat-square)](https://github.com/Abhijith666222/WanderSure)
[![Groq AI](https://img.shields.io/badge/Powered%20by-Groq%20AI-000?style=flat-square)](https://groq.com)
[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Next.js](https://img.shields.io/badge/Frontend-Next.js%2014-000?style=flat-square&logo=next.js)](https://nextjs.org)

</div>

---

## 🎯 What is WanderSure?

**WanderSure** turns travel insurance from a chore into a conversation. Upload a booking, ask in plain language, get answers with real policy citations, compare plans side by side, and buy without leaving the chat. We built all five innovation blocks from the Ancileo × MSIG challenge and then went further: sentiment-aware replies, multi-language support, document-based quoting, risk scoring from claims data, and Stripe payments wired into the flow.

---

## 🚀 Why it's cool

| Before | With WanderSure |
|--------|------------------|
| 10–30 min of forms | Chat and upload; quote in minutes |
| Guessing which plan fits | Compare policies on any criteria with citations |
| Dense PDFs and jargon | Plain-language answers + exact policy references |
| Pay and hope | Risk assessment + coverage suggestions, then pay in-chat |

We deliver a **zero-form experience**: extract trip details from PDFs and images, validate and fill gaps with questions, recommend coverage using historical claims patterns, and complete purchase via Stripe with status updates in the same conversation.

---

## 🧩 What we built (all 5 blocks)

### 🧠 Block 1: Policy intelligence

- **PDF extraction** from all policy PDFs (PyPDF2 + pdfplumber).
- **Dynamic normalization** with Groq LLM into the taxonomy structure.
- **Semantic handling** of terms like "medical expenses" vs "healthcare costs".
- **Side-by-side comparison** of any policies on chosen criteria.
- **Citations** so every explanation points to exact policy text.

**Policies:** TravelEasy, Scootsurance, TravelEasy Pre-Ex · **Model:** Groq `llama-3.3-70b-versatile` (JSON mode).

---

### 💬 Block 2: Conversational magic

- **Natural-language Q&A** with a consistent, travel-savvy tone.
- **Sentiment detection** (confused, frustrated, anxious, excited) and **adaptive tone**.
- **Multi-language**: auto-detect language and respond in kind.
- **Conversation memory** for preferences and trip context.
- **Personality**: friendly, clear, with light emoji use.

**Implementation:** `conversation_handler.py` · Memory is in-memory (extendable to Redis).

---

### 📄 Block 3: Document intelligence

- **Multi-format**: PDFs, images, emails, plain text.
- **Structured extraction**: dates, destinations, travelers, costs.
- **Validation**: flags missing data and asks follow-ups.
- **Quote generation** from trip data with **activity-based** and **age-based** pricing.

**Stack:** pdfplumber (primary), PyPDF2 fallback, Groq for structured JSON extraction.

---

### 💳 Block 4: Seamless commerce

- **Stripe** checkout sessions created from the chat.
- **DynamoDB** for payment records and status.
- **Status polling** so the bot can report payment state in real time.
- **Webhooks**: Stripe events update DynamoDB via the Payments stack.
- **Error handling** for failures and edge cases.

**Setup:** Uses the repo `Payments/` Docker stack (DynamoDB Local, webhook service, payment pages).

---

### 🎯 Block 5: Predictive intelligence

- **Risk assessment** from destination, activities, age, duration, and season.
- **Historical-style analysis** (synthetic claims data; extendable to real DB).
- **Coverage recommendations** (e.g. medical limits) based on trip and risk.
- **Activity risk scoring** and **seasonal patterns** in the model.

**Implementation:** `predictive_intelligence.py` · Multi-factor risk scoring + Groq for natural-language recommendations.

---

## 🎨 Frontend

- **Chat UI**: gradients, smooth animations, real-time messaging.
- **Markdown** in bot responses and **quick-action** sample questions.
- **Mobile-friendly** layout.

**Stack:** Next.js 14 (App Router), TypeScript, Tailwind CSS.

---

## 📡 API overview

Base URL: `http://localhost:8001/api/`

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/ask` | POST | Ask questions about insurance |
| `/extract` | POST | Extract trip info from documents |
| `/quote` | POST | Generate personalized quotes |
| `/compare` | POST | Compare policies |
| `/risk` | POST | Get risk assessment |
| `/payment/create` | POST | Create payment session |
| `/payment/status/{id}` | GET | Check payment status |

---

## 🔧 Configuration

| Variable | Required | Description |
|----------|----------|-------------|
| `GROQ_API_KEY` | Yes | All AI features |
| `STRIPE_SECRET_KEY` | No | Payment processing |
| `STRIPE_WEBHOOK_SECRET` | No | Webhook validation |
| `DDB_ENDPOINT` | No | Default: `http://localhost:8000` |
| `AWS_REGION` | No | Default: `ap-southeast-1` |

---

## 🧪 Quick test

```bash
python test_system.py
```

Covers policy extraction, conversation handling, document extraction, risk assessment, and payment handler (when keys are set).

---

## 📁 Repo layout

```
WanderSure/
├── wandersure_server.py      # MCP server (main entry)
├── run_server.py             # FastAPI server
├── policy_intelligence.py    # Block 1
├── conversation_handler.py  # Block 2
├── document_intelligence.py  # Block 3
├── payment_handler.py        # Block 4
├── predictive_intelligence.py # Block 5
├── test_system.py            # Test suite
├── frontend/                 # Next.js UI
├── Payments/                 # Payment services (Docker)
├── Taxonomy/                 # Policy taxonomy
├── Policy_Wordings/          # Source policy PDFs
└── problem_statement.md      # Original challenge brief
```

---

## ✅ Innovation checklist (what we hit)

- Unique approach to understanding insurance documents
- Normalization beyond fixed taxonomies
- Comparison with citations
- Distinct personality and natural conversation flow
- Novel extraction and validation
- Seamless payment flow and error handling
- Risk and recommendation from claims-style data
- Predictive modeling and clear value for the user

**WanderSure is a full implementation of the five blocks with real UX and technical enhancements.**

For the original challenge text and judging criteria, see **`problem_statement.md`**.
