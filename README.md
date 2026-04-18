# 🤖 WhatsApp AI Admission Agent

An AI-powered WhatsApp chatbot built for coaching centres to automate student admissions — from lead capture to course queries to follow-up scheduling. Built entirely with no-code/low-code tools.

---

## 📸 Workflow Preview

> ![Workflow](./Screenshot%202026-04-18%20053507.png)

---

## ✨ What It Does

- **Lead Capture** — Automatically logs every new student inquiry (name, phone, course interest) into a Google Sheet
- **Course Query Handling** — Student asks about a course → agent fetches real-time fee, duration, and batch info from a Google Sheet and replies instantly
- **AI-Powered Replies** — GPT-4o-mini acts as a polite admissions counselor, keeping responses short, accurate, and human
- **Follow-Up Scheduling** — Flags students for follow-up based on conversation stage
- **Webhook Verification** — Handles Meta's webhook handshake automatically on first setup

---

## 🛠 Tech Stack

| Tool | Purpose |
|------|---------|
| **n8n** | Workflow automation & logic |
| **Meta WhatsApp Cloud API** | WhatsApp messaging interface |
| **OpenAI GPT-4o-mini** | AI response generation |
| **Google Sheets** | Student leads & course data storage |
| **Twilio (optional)** | WhatsApp sandbox for testing |

---

## 🔁 Workflow Architecture

```
Incoming WhatsApp Message
        ↓
  Webhook (n8n)
        ↓
Is Verification Request? (Meta handshake)
   ├── YES → Return hub.challenge
   └── NO  ↓
  Parse Phone + Message (JavaScript node)
        ↓
  Lookup Student in Google Sheets
        ↓
  Fetch Course Data from Google Sheets
        ↓
  Generate AI Response (GPT-4o-mini)
        ↓
  Send WhatsApp Reply (HTTP Request → Twilio/Meta API)
```

---

## 📂 Files

```
/
├── My_workflow_3_Fixed.json     # Main WhatsApp agent workflow
├── My_workflow_5.json           # Supporting/extended workflow
└── README.md
```

---

## 🚀 How to Run

### Prerequisites
- n8n instance (cloud or self-hosted)
- Meta Developer account with WhatsApp Cloud API access
- OpenAI API key
- Google Sheets with two sheets: `student leads` and `course data`

### Setup Steps

1. **Import the workflow** — In n8n, go to *Workflows → Import from file* and upload `My_workflow_3_Fixed.json`

2. **Set credentials** — Add your credentials in n8n for:
   - Google Sheets OAuth2
   - OpenAI API
   - HTTP Basic Auth (Twilio or Meta)

3. **Configure Google Sheets**
   - Sheet 1 (`student leads`): Columns — `Name`, `Phone`, `Course`
   - Sheet 2 (`course data`): Columns — `Course`, `Fee`, `Duration`, `Batch`

4. **Set your webhook URL** in Meta Developer Console → WhatsApp → Webhook
   - URL: `https://your-n8n-instance/webhook/whatsapp`
   - Verify Token: match what's in your workflow

5. **Activate the workflow** — Hit the toggle in n8n to publish. The webhook won't respond until the workflow is active.

---

## ⚠️ Common Issues

| Issue | Fix |
|-------|-----|
| Webhook verification failing | Make sure workflow is **published/activated**, not just saved |
| Node naming mismatch errors | Ensure node names in expressions exactly match the node titles |
| GPT not responding | Check OpenAI API key credentials and token limits |

---

## 👤 Built By

**Tegbir Singh**
BBA — Branding & Advertising, NMIMS Mumbai
[tegbir1060@gmail.com](mailto:tegbir1060@gmail.com) | +91 7347348454

---

## 📄 License

MIT — free to use and modify with attribution.
