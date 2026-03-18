# Agentic-Support 🎧🤖

An **Autonomous Customer Support Agent** designed to handle Tier-1 support tickets end-to-end. This intelligent system reads incoming tickets, queries internal documentation, drafts resolutions, and takes necessary actions via API integrations (e.g., refunds, password resets) before confidently closing the ticket. High-risk or complex queries are intelligently escalated to human agents.

---

## 🚀 How It Works

1. **Ingestion:** Incoming tickets are captured via webhooks or API integrations.
2. **Contextualization:** The ticket content is embedded and semantically matched against a centralized knowledge base using Pinecone.
3. **Drafting (RAG):** The agent drafts a resolution utilizing Retrieval-Augmented Generation.
4. **Action & Tool Use:** If a tool action is needed (e.g., executing a refund via Stripe, unlocking an account), the agent calls the relevant API.
5. **Confidence Gating:** Every action is assessed with a confidence score. Low-confidence cases or actions exceeding specific risk thresholds are immediately escalated to a human agent.

## 🛠 Tech Stack

- **LLM/AI:** Claude API
- **Ticketing / CRM Integrations:** Zendesk API
- **Knowledge Base:** Confluence API / Notion API, Pinecone (Vector Store)
- **Execution / Action:** Stripe API
- **Backend:** Python, FastAPI

## 🧠 Key Agentic Patterns

- **RAG (Retrieval-Augmented Generation):** Grounding responses in verifiable internal documentation.
- **Tool Use with Gating:** Safely interacting with external systems.
- **Human-in-the-Loop Escalation:** Seamlessly transferring context to human agents when confidence is low.
- **Confidence Scoring:** Evaluating certainty before taking automated actions.

## 📁 Project Structure

```text
.
├── agents/
│   ├── ticket_reader.py
│   ├── resolver.py
│   ├── tool_executor.py       # Stripe, Zendesk, API Integrations
│   └── human_escaler.py
├── tools/
│   ├── zendesk_api.py
│   ├── confluence_api.py      
│   ├── stripe_api.py
│   └── vector_store/
│       └── pinecone_client.py
├── workflows/
│   ├── support_workflow.py    # Standard autonomous resolution flow
│   └── escalation_workflow.py # Hand-off flow to human support
├── app/
│   ├── api/v1/
│   │   ├── tickets_webhook.py
│   │   └── live_chat.py
│   └── core/                  # App initialization, settings, models
├── data/
│   ├── sample_tickets/        # Mock tickets for testing
│   └── knowledge_base/        # Internal documentation / markdown
├── outputs/runs/              # Execution logs and agent traces
├── tests/                     # Unit and integration test suites
└── config/                    # Environment configs (dev, staging, prod)
```

## ✨ Stretch Goals

- **Past Incident Memory for Pattern Recognition:** Identifying recurring system issues based on aggregated analysis of incoming ticket trends.
- **Sentiment-Aware Tone Shifting:** Dynamically adjusting the LLM's communication tone based on the user's emotional state (frustration, urgency).
- **SLA-Aware Prioritization:** Processing tickets optimally based on customer tier, urgency, and SLA deadlines.
- **Cost/Blast Radius Estimation:** Calculating the potential risk and financial impact before undertaking automated actions (e.g., limiting maximum autonomous refund amounts).
