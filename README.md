<div align="center">

<h1>Aeronyx AI Lead Qualification Agent</h1>

[![n8n](https://img.shields.io/badge/Automation-n8n-EA4B71.svg?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io/)
[![AI](https://img.shields.io/badge/AI-Lead%20Qualification-6C63FF.svg?style=for-the-badge)](#)
[![Google Sheets](https://img.shields.io/badge/Google-Sheets-34A853.svg?style=for-the-badge&logo=googlesheets&logoColor=white)](https://www.google.com/sheets/about/)
[![OpenAI](https://img.shields.io/badge/AI-OpenAI-412991.svg?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com/)

[Overview](#overview) · [How It Works](#how-it-works) · [Setup](#quick-start) · [Configuration](#configuration) · [Security](#security) · [Roadmap](#roadmap)

</div>

<p align="center">
  <em>AI-powered lead qualification automation built with n8n.</em>
</p>

---

## What You Get

- **Automatic lead monitoring.** Detect new leads directly from Google Sheets without manually checking for new entries.
- **AI-powered qualification.** Analyze incoming lead information using an AI model and predefined qualification criteria.
- **Structured AI results.** Convert AI responses into structured data that can be used by other automation nodes.
- **Automatic status updates.** Write qualification results directly back into Google Sheets.
- **Custom qualification logic.** Modify the AI instructions according to your business, industry, or sales requirements.
- **Error handling.** Stop and report workflow failures instead of silently losing lead-processing tasks.
- **Expandable architecture.** Designed as the foundation for a larger AI-powered lead generation and sales automation system.

---

## Overview

The **Aeronyx AI Lead Qualification Agent** automates the process of reviewing incoming leads.

Instead of manually examining every new prospect, the workflow detects a new lead, sends the available information to an AI model, generates a qualification result, processes the response, and updates the lead automatically.

```text
New Lead
    │
    ▼
Google Sheets
    │
    ▼
New Entry Detected
    │
    ▼
AI Lead Analysis
    │
    ▼
Lead Qualification
    │
    ▼
Structured Result
    │
    ▼
Google Sheets Updated
```

The current version focuses on **lead analysis and qualification**.

---

## How It Works

### 1. Lead Detection

The workflow monitors a configured Google Sheet.

When a new lead is added, the Google Sheets trigger automatically starts the workflow.

### 2. Lead Information Processing

Information associated with the new lead is collected and prepared for AI analysis.

The information available depends on the structure of your Google Sheet.

For example:

```text
Name
Company
Industry
Website
Requirements
Business Information
Contact Information
```

### 3. AI Lead Qualification

The lead information is passed to the AI qualification node.

The AI evaluates the prospect according to the qualification instructions configured inside the workflow.

Possible qualification factors include:

- Business relevance
- Industry
- Company characteristics
- Customer requirements
- Sales potential
- Lead quality
- Business fit

### 4. Structured Response

The AI response is processed and converted into structured data.

This allows the remaining automation nodes to reliably use the generated result.

### 5. Lead Status Update

The final qualification result is automatically written back to Google Sheets.

The spreadsheet can therefore function as a lightweight lead-management database.

---

## Workflow Architecture

```text
┌───────────────────────────────┐
│     Google Sheets Trigger     │
│        New Lead Added         │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│       Lead Information        │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│      AI Lead Qualification    │
│                               │
│     Analyze Lead Details      │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│       Extract AI Result       │
│      Structured Response      │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│             Merge             │
│       Workflow Information    │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│      Update Lead Status       │
│         Google Sheets         │
└───────────────────────────────┘
```

---

## Workflow Components

| Component | Purpose |
| --- | --- |
| **Check for new entries** | Monitors Google Sheets for new leads |
| **Qualify leads with GPT** | Performs AI-powered lead evaluation |
| **Extract JSON reply** | Converts the AI response into structured information |
| **Merge** | Combines workflow data |
| **Update lead status** | Writes the qualification result back to Google Sheets |
| **Error Handler** | Handles workflow failures |

---

## Quick Start

### 1. Clone The Repository

```bash
git clone https://github.com/aeronyx03-cpu/ai-lead-generation-agent.git
```

Enter the project:

```bash
cd ai-lead-generation-agent
```

---

### 2. Start n8n

If n8n is installed locally:

```bash
n8n
```

Open:

```text
http://localhost:5678
```

---

### 3. Import The Workflow

Inside n8n:

**Create Workflow → Import from File**

Select:

```text
workflow.json
```

The complete automation will appear inside the n8n workflow editor.

---

## Configuration

<details>

<summary><strong>Google Sheets Setup</strong></summary>

Connect your Google account through the n8n credential manager.

Configure the Google Sheets trigger to monitor the spreadsheet containing incoming leads.

The spreadsheet should contain the information required for qualification.

Example structure:

| Name | Company | Industry | Website | Requirement | Status |
| --- | --- | --- | --- | --- | --- |
| Example Lead | Example Inc. | Technology | example.com | Website Development | Pending |

The exact columns can be customized according to your requirements.

</details>

<details>

<summary><strong>AI Setup</strong></summary>

Configure your AI credentials through the n8n credential manager.

The current workflow contains an AI-powered lead qualification step.

Do not store API keys directly inside the workflow repository.

</details>

<details>

<summary><strong>Lead Qualification Logic</strong></summary>

Open:

```text
Qualify leads with GPT
```

inside the n8n workflow.

Modify the qualification instructions according to your requirements.

Example:

```text
Analyze the supplied lead.

Evaluate the lead based on:

- Business relevance
- Company characteristics
- Customer requirements
- Sales potential
- Overall business fit

Return the result in structured format.
```

Qualification criteria can be completely customized for different businesses.

</details>

---

## Testing

Before activating the workflow, perform a complete test.

### Add A Test Lead

Add a sample entry to your configured Google Sheet.

The expected execution should be:

```text
Test Lead Added
       │
       ▼
n8n Detects Entry
       │
       ▼
AI Receives Lead
       │
       ▼
AI Generates Qualification
       │
       ▼
Response Processed
       │
       ▼
Google Sheet Updated
```

Verify that:

- The correct lead is detected.
- The correct information reaches the AI.
- The AI returns the expected structure.
- The qualification result is parsed correctly.
- Google Sheets receives the updated result.
- Error handling works correctly.

Once testing is successful, activate the workflow.

---

## Security

Credentials should be managed through **n8n's credential management system**.

Never commit:

```text
API Keys
Passwords
OAuth Tokens
Database Credentials
Private Tokens
Service Account Secrets
```

The repository ignores common secret files:

```gitignore
.env
.env.local
credentials.json
*.secret
```

---

## Repository Structure

```text
ai-lead-generation-agent/
│
├── workflow.json
├── README.md
└── .gitignore
```

### `workflow.json`

Contains the complete n8n automation.

### `README.md`

Contains project documentation, architecture, setup instructions, and configuration information.

### `.gitignore`

Prevents common secret and environment files from being accidentally committed.

---

## Current Capabilities

The current system handles:

```text
Incoming Lead
      ↓
AI Analysis
      ↓
Qualification
      ↓
Structured Result
      ↓
Lead Status Update
```

Automatic lead discovery and outreach are not part of the current version.

---

## Roadmap

The system is designed to eventually become a complete AI-powered lead generation and sales automation platform.

Planned capabilities include:

- **Automatic Lead Discovery**
  - Find potential businesses and prospects automatically.

- **Business Data Enrichment**
  - Collect additional information about companies and prospects.

- **Website Analysis**
  - Analyze company websites before qualification.

- **AI Lead Scoring**
  - Assign numerical lead-quality scores.

- **Duplicate Detection**
  - Prevent the same prospect from entering the system multiple times.

- **Personalized Outreach**
  - Generate customized messages for each qualified lead.

- **Automated Email Outreach**
  - Automatically contact approved prospects.

- **Follow-Up Automation**
  - Send intelligent follow-ups based on responses and timing.

- **CRM Integration**
  - Synchronize qualified leads with CRM platforms.

- **Human Approval**
  - Allow manual approval before outreach.

- **Analytics**
  - Track qualification rates, outreach performance, and conversions.

---

## Future Architecture

```text
Lead Discovery
      │
      ▼
Data Enrichment
      │
      ▼
Website Analysis
      │
      ▼
AI Lead Scoring
      │
      ▼
Lead Qualification
      │
      ▼
Human Approval
      │
      ▼
Personalized Outreach
      │
      ▼
Automated Follow-Up
      │
      ▼
CRM
      │
      ▼
Conversion Analytics
```

---

## Project Goal

**Aeronyx AI Lead Qualification Agent** is designed as the first component of a modular AI-powered sales automation ecosystem.

The goal is to automate repetitive lead-processing tasks while maintaining configurable qualification logic and allowing the system to expand into:

**Lead Discovery → Qualification → Outreach → Follow-Up → Conversion**

---

<div align="center">

### Aeronyx

**AI Automation · Intelligent Workflows · Software Solutions**

</div>
