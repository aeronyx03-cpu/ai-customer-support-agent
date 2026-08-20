<div align="center">

<h1>Aeronyx AI Customer Support Agent</h1>

[![n8n](https://img.shields.io/badge/Automation-n8n-EA4B71.svg?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io/)
[![WhatsApp](https://img.shields.io/badge/Support-WhatsApp-25D366.svg?style=for-the-badge&logo=whatsapp&logoColor=white)](https://www.whatsapp.com/)
[![OpenAI](https://img.shields.io/badge/AI-OpenAI-412991.svg?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com/)
[![Qdrant](https://img.shields.io/badge/RAG-Qdrant-DC244C.svg?style=for-the-badge)](https://qdrant.tech/)
[![Google Drive](https://img.shields.io/badge/Knowledge-Google%20Drive-4285F4.svg?style=for-the-badge&logo=googledrive&logoColor=white)](https://drive.google.com/)

[Overview](#overview) · [Architecture](#workflow-architecture) · [Setup](#quick-start) · [Configuration](#configuration) · [Security](#security) · [Roadmap](#roadmap)

</div>

<p align="center">
  <em>AI-powered WhatsApp customer support with RAG, memory, and business knowledge retrieval.</em>
</p>

---

## What You Get

- **AI-powered customer support.** Automatically answer customer questions through WhatsApp.
- **RAG knowledge retrieval.** Retrieve relevant business information before generating responses.
- **Google Drive knowledge base.** Use business documents stored in Google Drive as support knowledge.
- **Vector search with Qdrant.** Store and retrieve document embeddings for contextual answers.
- **Conversation memory.** Maintain recent customer conversation context.
- **WhatsApp integration.** Receive and send customer messages directly through WhatsApp.
- **AI Agent architecture.** Allow the AI agent to combine customer messages with retrieved business knowledge.
- **Automated document processing.** Download and process knowledge documents for vector storage.
- **Webhook support.** Handle WhatsApp verification and incoming message events.
- **Expandable support platform.** Designed to evolve into a complete AI customer-service system.

---

## Overview

The **Aeronyx AI Customer Support Agent** is an intelligent customer-support automation built with n8n.

It connects WhatsApp conversations with an AI Agent and a Retrieval-Augmented Generation (RAG) knowledge system.

Instead of answering only from the AI model's general knowledge, the system can retrieve relevant information from your business documents and use that context to generate more useful responses.

```text
Customer
   │
   ▼
WhatsApp Message
   │
   ▼
Webhook
   │
   ▼
AI Support Agent
   │
   ├──────────────► Conversation Memory
   │
   └──────────────► RAG Knowledge Retrieval
                        │
                        ▼
                   Qdrant Vector DB
                        │
                        ▼
                  Business Documents
                        │
                        ▼
                  AI Response
                        │
                        ▼
                     WhatsApp
```

---

## Workflow Architecture

```text
                    ┌─────────────────────┐
                    │      Customer       │
                    │      WhatsApp       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │      Webhook        │
                    │ Incoming Message    │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Message Check     │
                    │  Process Messages   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │      AI Agent       │
                    └──────┬───────┬──────┘
                           │       │
                  ┌────────┘       └─────────┐
                  ▼                          ▼
        ┌──────────────────┐       ┌──────────────────┐
        │ Conversation     │       │ RAG Retrieval    │
        │ Memory           │       │                  │
        └──────────────────┘       └────────┬─────────┘
                                            │
                                            ▼
                                  ┌──────────────────┐
                                  │ Qdrant Vector DB │
                                  └────────┬─────────┘
                                           │
                                           ▼
                                  ┌──────────────────┐
                                  │ Business Context │
                                  └────────┬─────────┘
                                           │
                           ┌───────────────┘
                           ▼
                    ┌─────────────────────┐
                    │   OpenAI Model      │
                    │ Generate Response   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │ WhatsApp Response   │
                    └─────────────────────┘
```

---

## Knowledge Base Pipeline

The system can build its support knowledge base from documents stored in Google Drive.

```text
Google Drive
     │
     ▼
Download Documents
     │
     ▼
Data Loader
     │
     ▼
Token Splitter
     │
     ▼
OpenAI Embeddings
     │
     ▼
Qdrant Vector Store
     │
     ▼
Searchable Business Knowledge
```

This allows the AI support agent to retrieve relevant information when answering customer questions.

---

## Core Components

| Component | Purpose |
| --- | --- |
| **Webhook** | Receives incoming WhatsApp events |
| **AI Agent** | Controls AI-powered customer-support responses |
| **OpenAI Chat Model** | Generates natural-language responses |
| **RAG** | Retrieves relevant business information |
| **Qdrant Vector Store** | Stores and retrieves business knowledge embeddings |
| **Google Drive** | Provides business documents |
| **Embeddings OpenAI** | Converts document content into searchable vectors |
| **Token Splitter** | Splits large documents into smaller searchable chunks |
| **Window Buffer Memory** | Maintains conversation context |
| **WhatsApp Send** | Sends AI-generated replies to customers |

---

## Quick Start

### 1. Clone The Repository

```bash
git clone https://github.com/aeronyx03-cpu/ai-customer-support-agent.git
```

Enter the project:

```bash
cd ai-customer-support-agent
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

---

## Configuration

<details>

<summary><strong>WhatsApp Setup</strong></summary>

Configure your WhatsApp Business integration inside n8n.

The workflow uses webhook nodes to receive WhatsApp events and WhatsApp nodes to send responses.

You will need the appropriate WhatsApp Business / Meta credentials.

Configure:

```text
Webhook verification
WhatsApp credentials
Phone number configuration
Incoming message events
Outgoing message permissions
```

</details>

<details>

<summary><strong>OpenAI Setup</strong></summary>

Connect your OpenAI credentials through the n8n credential manager.

The workflow uses OpenAI for:

```text
Chat responses
Embeddings
RAG processing
```

Never store real API keys directly inside this repository.

</details>

<details>

<summary><strong>Qdrant Setup</strong></summary>

The workflow uses Qdrant as its vector database.

Qdrant stores searchable embeddings generated from your business documents.

Configure:

```text
Qdrant URL
Collection
Authentication
Vector-store credentials
```

The workflow contains nodes for creating and refreshing the collection.

</details>

<details>

<summary><strong>Google Drive Knowledge Base</strong></summary>

Connect Google Drive through the n8n credential manager.

Store the business documents that the AI should use as its knowledge source.

Examples:

```text
FAQ documents
Product information
Service documentation
Policies
Pricing information
Business procedures
Support documentation
```

The workflow downloads these documents and processes them for RAG retrieval.

</details>

<details>

<summary><strong>Conversation Memory</strong></summary>

The workflow contains window-buffer memory.

This allows the support agent to retain recent conversation context instead of treating every message independently.

Memory configuration can be adjusted according to the support use case.

</details>

---

## How RAG Works

RAG stands for **Retrieval-Augmented Generation**.

Instead of asking the AI model to answer directly:

```text
Customer Question
        ↓
      AI Model
        ↓
      Answer
```

the system retrieves relevant business information first:

```text
Customer Question
        │
        ▼
Search Business Knowledge
        │
        ▼
Retrieve Relevant Documents
        │
        ▼
Send Context + Question to AI
        │
        ▼
Generate Context-Aware Response
```

This architecture is especially useful for customer support because answers can be based on your own business information.

---

## Example Customer Flow

```text
Customer:
"What is your refund policy?"

        ↓

WhatsApp receives message

        ↓

AI Agent identifies request

        ↓

RAG searches Qdrant

        ↓

Relevant refund-policy document retrieved

        ↓

AI creates response using retrieved information

        ↓

Customer receives response on WhatsApp
```

---

## Testing

Before activating the workflow:

1. Configure WhatsApp credentials.
2. Configure OpenAI.
3. Connect Google Drive.
4. Configure Qdrant.
5. Load sample business documents.
6. Build the vector collection.
7. Send a test WhatsApp message.
8. Verify that relevant business information is retrieved.
9. Verify the generated AI response.
10. Confirm that the WhatsApp reply is delivered.

Expected flow:

```text
Customer Message
       │
       ▼
Webhook
       │
       ▼
AI Agent
       │
       ▼
RAG Search
       │
       ▼
Business Knowledge
       │
       ▼
AI Response
       │
       ▼
WhatsApp Reply
```

---

## Security

Never commit:

```text
OpenAI API Keys
WhatsApp Access Tokens
Meta Credentials
Qdrant API Keys
Google OAuth Tokens
Passwords
Webhook Secrets
Private Service Credentials
```

Use the **n8n credential manager** for sensitive information.

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
ai-customer-support-agent/
│
├── workflow.json
├── README.md
└── .gitignore
```

### `workflow.json`

Contains the complete n8n customer-support workflow.

### `README.md`

Contains project documentation, setup instructions, and system architecture.

### `.gitignore`

Helps prevent secrets and local configuration files from being accidentally committed.

---

## Current Capabilities

The current architecture supports:

```text
WhatsApp Customer Messages
        ↓
AI Agent
        ↓
Conversation Memory
        ↓
RAG Knowledge Retrieval
        ↓
OpenAI Response
        ↓
WhatsApp Reply
```

It also contains the infrastructure required to build and refresh the vector knowledge base.

---

## Roadmap

Future versions can include:

- **Human Support Escalation**
- **Automatic Ticket Creation**
- **Sentiment Analysis**
- **Urgency Detection**
- **Customer Identification**
- **CRM Integration**
- **Conversation Analytics**
- **Multilingual Support**
- **Voice Message Support**
- **Automatic Ticket Classification**
- **Email Support**
- **Telegram Support**
- **Website Chat Support**
- **Support Performance Dashboard**
- **Customer Satisfaction Tracking**
- **Multiple AI Provider Support**

---

## Future Architecture

```text
                 Customer
                    │
           ┌────────┼────────┐
           ▼        ▼        ▼
       WhatsApp   Website   Email
           │        │        │
           └────────┼────────┘
                    ▼
              AI Support Agent
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
      Memory       RAG       CRM Data
        │           │           │
        └───────────┼───────────┘
                    ▼
              AI Decision
                ↙       ↘
          Resolve       Escalate
             │              │
             ▼              ▼
        Customer       Human Agent
```

---

## Project Goal

The goal of the **Aeronyx AI Customer Support Agent** is to create a modular customer-support platform that combines:

**AI Agents + Business Knowledge + Conversation Memory + Messaging Automation**

The long-term system is designed to automate routine customer queries while allowing complex or sensitive conversations to be escalated to human support.

---

<div align="center">

### Aeronyx

**AI Automation · Intelligent Workflows · Software Solutions**

</div>
