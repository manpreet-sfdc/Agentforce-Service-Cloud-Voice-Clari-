# Agentforce + Service Cloud Voice + Clari  
## AI-Driven Call Intelligence with MCP Orchestration

---

## 📌 Overview

This repository documents a **reference architecture and implementation strategy** for integrating:

- **Salesforce Agentforce** with **Service Cloud Voice** for real-time call handling and in-call AI assistance
- **Clari** for post-call AI intelligence (call summary, transcript refinement, intent detection, and next-step generation)
- **Model Context Protocol (MCP)** as the orchestration and governance layer for AI interactions

The solution enables **real-time agent productivity** and **post-call intelligence**, while Salesforce remains the **system of record**.

---

## 🎯 Objectives

- Provide **live AI assistance** during customer voice calls
- Generate **high-quality call summaries, intents, and next steps**
- Use **MCP** to govern AI context, prompts, and model responsibilities
- Avoid AI overlap between Agentforce and Clari
- Ensure **enterprise security, compliance, and observability**

---

## 🧩 High-Level Architecture

| Layer | Technology | Responsibility |
|----|----|----|
| Voice & CTI | Service Cloud Voice | Call routing, recording, real-time transcription |
| Real-time AI | Agentforce | Live agent assist, knowledge surfacing |
| Post-call AI | Clari | Summary, intent, sentiment, next steps |
| AI Orchestration | MCP | Context control, prompt routing, governance |
| System of Record | Salesforce | VoiceCall, Case, Task, Activity |

---

## 🔁 End-to-End Call Flow

1. Customer initiates call → Service Cloud Voice
2. Agent answers call in Salesforce Console
3. Agentforce provides **real-time AI guidance**
4. Call ends → `VoiceCall` record created
5. Audio + transcript stored in Salesforce
6. Clari ingests call data
7. Clari AI generates:
   - Call summary
   - Customer intent
   - Sentiment
   - Next steps
8. Insights synced back to Salesforce
9. MCP logs and governs all AI interactions

---

## 🧠 Model Context Protocol (MCP)

### Why MCP?

MCP ensures:
- Clear separation of **real-time vs post-call AI**
- Controlled AI context sharing
- Prompt versioning and auditability
- Model-level governance and fallback handling

---

### MCP Context by Phase

#### Real-Time Call Phase (Agentforce)

```
Context Inputs:
- VoiceCall ID
- Rolling live transcript
- Case metadata
- Knowledge base references

MCP Rules:
- Low-latency models only
- No historical call context
- Stateless execution window

```
