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


Post-Call Intelligence Phase (Clari)


Context Inputs:
- Final transcript
- Call audio reference
- Account & Opportunity metadata
- Historical interaction summaries

MCP Rules:
- Long-context models allowed
- Structured output enforcement
- Historical trend analysis enabled

- MCP Prompt Contracts
Call Summary Contract

```
{
  "summary": "string",
  "customer_intent": [
    "Support",
    "Renewal",
    "Upsell",
    "Escalation"
  ],
  "sentiment": "Positive | Neutral | Negative",
  "key_topics": ["string"],
  "next_steps": [
    {
      "action": "string",
      "owner": "Agent | System",
      "due_date": "ISO-8601"
    }
  ]
}
```


Salesforce Data Model
Core Objects

| Object      | Purpose                          |
| ----------- | -------------------------------- |
| VoiceCall   | Call audio, transcript, metadata |
| Case        | Support context                  |
| Task        | Follow-up actions                |
| Activity    | Timeline & engagement tracking   |
| Opportunity | Revenue insights (optional)      |


Field Mapping Example

| AI Output       | Salesforce Field                   |
| --------------- | ---------------------------------- |
| Call Summary    | `VoiceCall.Call_Summary__c`        |
| Customer Intent | `VoiceCall.Intent__c`              |
| Next Steps      | `Task.Subject`, `Task.Description` |
| Risk Signals    | `Opportunity.Risk_Score__c`        |


## 🔐 Security & Compliance

### Data Protection
- Audio stored in **Service Cloud Voice provider** or **Salesforce**
- Transcript access controlled via **Salesforce permission sets**
- **MCP enforces context-scoped data access**

### Compliance Controls
- GDPR & SOC 2 aligned
- PII masking enforced at the **MCP layer**
- Full AI audit trail including:
  - Prompt version
  - Model used
  - Execution timestamp
  - Output confidence score

---

## ⚙️ Implementation Strategy

### Phase 1 – Foundation
- Enable **Service Cloud Voice**
- Configure **Agentforce**
- Enable **VoiceCall** object
- Integrate **Clari** with Salesforce

### Phase 2 – MCP Enablement
- Define AI **prompt contracts**
- Configure **context boundaries**
- Implement **fallback and retry logic**
- Enable **observability and execution logs**

### Phase 3 – Intelligence Expansion
- Intent taxonomy tuning
- Sentiment and risk scoring
- Automated task creation
- Manager dashboards and insights

---

## 🚀 Deployment Guidelines

- **Agentforce** → latency-sensitive, real-time AI only
- **Clari** → heavy post-call analysis and intelligence
- Enforce **single ownership** of call summary fields
- Version all **MCP contracts** in Git

---

## 📈 Observability & Metrics

### Recommended KPIs
- AI suggestion acceptance rate
- Call summary accuracy score
- Follow-up completion rate
- Intent classification precision

---

## 🔄 Extensibility

- Plug in alternative **Conversation Intelligence** tools
- Extend MCP to **chat and email** channels
- Add **Einstein Copilot** for automated field updates

---

## 🧪 Testing Strategy

- Mock call transcripts for unit testing
- Contract testing for MCP outputs
- Agent UAT for AI suggestions
- AI drift monitoring using MCP logs

---

## 📚 References

- Salesforce Service Cloud Voice Documentation  
- Agentforce Architecture Guides  
- Clari Conversation Intelligence APIs  
- Model Context Protocol (MCP) Specification  

---

## 🏁 Conclusion

This solution delivers:
- Real-time agent productivity with **Agentforce**
- Deep post-call intelligence with **Clari**
- Scalable, governed AI using **MCP**

The architecture is **enterprise-ready, modular, and future-proof**.

```

---

If you want next, I can:
- Add **Mermaid diagrams** (`sequenceDiagram`, `flowchart`)
- Create **repo folder structure**
- Provide **Apex / Flow / MCP config samples**
- Add **CI/CD & environment strategy**

```
