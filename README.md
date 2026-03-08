# AI Meeting Prep Assistant for AEs

AI-powered meeting prep assistant that turns a prospect list into structured sales briefs — built with n8n, Tavily, and any LLM of your choice.

---

## What It Does

Upload an Excel file with your prospect list. The agent researches each company, generates a structured meeting prep brief, and returns an enriched Excel file ready to download — all in under a minute.

Each brief includes:
- Company snapshot
- Recent signals (news, funding, hires, product announcements)
- Buyer profile
- Most likely pain point
- Suggested opening line

---

## How It Works

```
v0 Frontend
    |
    | POST multipart/form-data (Excel file)
    v
n8n Webhook
    |
    v
Extract from File (Excel to JSON rows)
    |
    v
AI Agent  <---->  Tavily (Customer_Research tool)
    |
    v
Edit Fields (map prospect fields + brief)
    |
    v
Convert to File (JSON rows to Excel binary)
    |
    v
Respond to Webhook (returns Excel to frontend)
    |
    v
v0 Frontend — user downloads enriched Excel file
```

---

## Repo Contents

```
├── workflow/
│   └── AI_Meeting_Prep_Assistant.json   # n8n workflow — import directly
├── prompts/
│   ├── system_prompt.md                 # AI Agent system prompt
│   └── v0_frontend_prompt.md            # Prompt used to generate the v0 frontend
├── sample/
│   └── sample_prospects.xlsx            # Sample input file to test the workflow
└── README.md
```

---

## Prerequisites

- [n8n](https://n8n.io) account (cloud or self-hosted)
- [Tavily](https://tavily.com) API key
- OpenAI API key (or swap for Claude, Gemini, or Mistral)
- [v0](https://v0.dev) account to generate the frontend

---

## Setup

### 1. Import the n8n workflow

- In n8n, go to **Workflows** and click **Import**
- Upload `workflow/AI_Meeting_Prep_Assistant.json`
- Add your credentials:
  - OpenAI API key (or your LLM of choice)
  - Tavily API key

### 2. Get your webhook URL

- Activate the workflow
- Copy the webhook URL from the Webhook node — it will look like:
  `https://[your-instance].app.n8n.cloud/webhook/meeting-prep`

### 3. Generate the frontend in v0

- Go to [v0.dev](https://v0.dev)
- Paste the contents of `prompts/v0_frontend_prompt.md`
- Replace `[YOUR_WEBHOOK_URL]` with the URL from step 2
- Deploy or export the generated app

### 4. Prepare your input file

Your Excel file needs exactly three columns:

| prospect_name | prospect_title | company_name |
|---|---|---|
| Sarah Chen | VP of Sales | Notion |
| Marcus Williams | Head of Revenue | Figma |

Use `sample/sample_prospects.xlsx` as a reference.

---

## Prompts

### System Prompt

The system prompt lives inside the AI Agent node and defines how the agent reasons and formats its output. The full prompt is in `prompts/system_prompt.md`.

To swap the LLM, replace the OpenAI Chat Model sub-node with any model supported by n8n. The system prompt works with Claude, Gemini, and Mistral without changes.

### v0 Frontend Prompt

The complete prompt used to generate the v0 frontend is in `prompts/v0_frontend_prompt.md`. Use it as a starting point and adjust the design or loading copy to fit your context.

---

## Part of the Building with Agentic AI Series

This project is built as part of my 10-week LinkedIn series on building real agentic systems.

- Week 1: How to Pick the Right Problems for AI Agents
- Week 2: What Is an Agentic System, Actually?
- Week 3: Prompt Engineering
- Week 4: From Tools to Product — this project

Follow along on [LinkedIn](https://linkedin.com) and [Medium](https://medium.com/@sarasoleymani) for new articles every week.

---

## Questions or Issues

Open an issue or drop a comment on the article. Happy to help you get it running.
