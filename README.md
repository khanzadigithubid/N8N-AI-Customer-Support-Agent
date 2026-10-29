# 🤖 N8N AI Customer Support Agent

An intelligent, multilingual customer support automation workflow built with **n8n** and **OpenAI GPT-4o-mini**. It handles customer queries automatically and escalates to a human agent when needed.

---

## ✨ Features

- 🌐 **Multilingual** — replies in English, Urdu, or Roman Urdu (matches the customer's language)
- 🧠 **AI-Powered** — uses OpenAI GPT-4o-mini for smart, context-aware responses
- 💬 **Conversation Memory** — remembers the last 10 messages per session
- 🔀 **Human Handoff** — automatically detects angry customers, refund requests, or unknown queries and escalates to a human
- ⚡ **Webhook-based** — easy to connect with WhatsApp, Telegram, or any frontend
- 🛡️ **Safe by design** — never asks for passwords, card numbers, or OTPs

---

## 🖼️ Workflow Diagram

![AI Customer Support Agent Workflow](./workflow-diagram.svg)

---

## 🗂️ Workflow Overview

```
Customer Message (Webhook)
        ↓
  AI Support Agent  ←──  OpenAI GPT-4o-mini
        ↑                 Conversation Memory
        ↓
  Check Handoff
        ↓
   Send Reply (JSON)
```

| Node | Description |
|------|-------------|
| **Customer Message (Webhook)** | Receives POST requests with customer messages |
| **AI Support Agent** | LangChain agent with custom system prompt |
| **OpenAI Chat Model** | GPT-4o-mini at temperature 0.3 |
| **Conversation Memory** | Window buffer — last 10 messages per session |
| **Check Handoff** | Detects `[HANDOFF]` tag in AI response |
| **Send Reply** | Returns JSON with `reply` and `needsHuman` fields |

---

## 🚀 Setup Guide

### 1. Import the Workflow
1. Open your n8n instance
2. Click **Import** → upload `Ai customer support agent .json`

### 2. Add OpenAI Credentials
1. Open the **OpenAI Chat Model** node
2. Add your OpenAI API key under credentials

### 3. Customize Company Info
Edit the **System Message** inside the **AI Support Agent** node with your own:
- Working hours
- Delivery & return policy
- Payment methods
- Support email & phone number

### 4. Activate the Workflow
Click **Activate** in the top-right corner of n8n.

---

## 🧪 Test It

Send a POST request to your webhook URL:

```bash
curl -X POST <YOUR_WEBHOOK_URL> \
  -H "Content-Type: application/json" \
  -d '{"sessionId": "user123", "message": "How long does delivery take?"}'
```

### Sample Response

```json
{
  "reply": "Delivery usually takes 3 to 5 working days. Orders above 2000 PKR get free delivery!",
  "needsHuman": false
}
```

### Human Handoff Response

```json
{
  "reply": "I understand your concern. Let me connect you with our support team right away.",
  "needsHuman": true
}
```

---

## 📋 API Reference

### Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `sessionId` | string | ✅ | Unique ID per user/conversation |
| `message` | string | ✅ | Customer's message |

### Response Body

| Field | Type | Description |
|-------|------|-------------|
| `reply` | string | AI-generated response |
| `needsHuman` | boolean | `true` if escalation is needed |

---

## 🔧 Customization Ideas

- 🔌 Replace the Webhook trigger with a **WhatsApp** or **Telegram** node
- 🗄️ Swap the memory buffer with **Redis** or **Postgres** for persistent memory
- 📧 Add an email/Slack notification node when `needsHuman` is `true`
- 📊 Log all conversations to Google Sheets or a database

---

## 🛠️ Tech Stack

- [n8n](https://n8n.io/) — Workflow automation
- [OpenAI GPT-4o-mini](https://platform.openai.com/) — Language model
- [LangChain nodes for n8n](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/) — AI agent framework

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

> Built with ❤️ using n8n + OpenAI
