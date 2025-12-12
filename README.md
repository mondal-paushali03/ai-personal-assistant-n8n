# 🌐 Personal Automation Assistant

*A modular workflow-based assistant for communication, scheduling, and task automation.*

This project implements a **personal automation system** built on **n8n** that centralizes routine tasks into one assistant.
It integrates **Telegram**, **Google Calendar**, **Gmail**, **VAPI phone calling**, **contact management**, and **knowledge retrieval** into a unified setup.

The system is structured into four independent workflows—each responsible for a specific function—and one master assistant that routes requests intelligently.
<img width="1633" height="755" alt="image" src="https://github.com/user-attachments/assets/3ea023b7-fdf8-4587-a8b4-53e197e0b736" />

---

## ⚙️ Overview

The Personal Assistant can:

* Process text and voice messages from Telegram
* Schedule events on Google Calendar
* Send and retrieve emails from Gmail
* Place automated phone calls via VAPI
* Look up verified contacts stored in Google Sheets
* Search internal knowledge using embeddings and Pinecone
* Maintain short-term conversation context

Instead of hardcoding actions, the system uses a **tool-based delegation approach**:
the main assistant identifies what the user wants and assigns the task to the correct workflow.

---

## 🧱 System Components

### 1. **Personal Assistant (Main Workflow)**

Handles incoming messages, understands intent, checks contacts, retrieves context, and decides which workflow should perform the requested action.

Responsible for:

* Accepting text & voice messages
* Transcribing audio
* Managing conversation state
* Routing tasks to tools (Calendar, Email, Phone, Knowledge Base)

### 2. **Calendar Agent**

Works with Google Calendar to:

* Create events
* Add attendees
* Retrieve events for specific dates
* Apply reasonable defaults (e.g., 60-minute duration)

### 3. **Email Agent**

Handles Gmail operations:

* Send structured emails
* Read emails filtered by sender
* Validate email addresses using the Contacts sheet
* Maintain consistent signatures
* Avoid sending messages to unknown recipients

### 4. **Phone Call Agent**

Uses VAPI to:

* Initiate calls with configurable instructions
* Wait for call completion
* Poll status in intervals
* Return a call summary

### 5. **Knowledge Base**

Stores internal documents as vector embeddings and retrieves relevant information using Pinecone.

### 6. **Contacts Database**

A Google Sheet used to verify phone numbers and email addresses before any call or email is executed.

---

## 🔌 Integration Flow

```
User Message (Telegram)
          ↓
 Personal Assistant
          ↓
  +-----------------------------+
  | Task Routing & Validation   |
  +-----------------------------+
    ↓         ↓         ↓
Calendar   Email     Phone
 Agent     Agent      Agent
    ↓         ↓         ↓
 Google     Gmail      VAPI
Calendar              Calling
```

---
## 💡 Example Interactions

### Scheduling

> “Add a meeting with John tomorrow at 4 PM.”

### Email

> “Send an update email to the design team.”

### Phone Call

> “Call the supplier and confirm the delivery date.”

### Voice Commands

Send a voice note → automatically transcribed → processed → executed.

---
## 🚀 Why This Project

This system was built to streamline routine personal and work-related tasks by centralizing them into one assistant.
Instead of switching between apps, the user interacts once, and the assistant handles the rest—whether it’s contacting someone, scheduling, retrieving information, or making a call.

It demonstrates practical automation, real API integrations, and modular workflow design.

---

## 🛠️ Technologies Used

* **n8n** (workflow orchestration)
* **Telegram Bot API**
* **Google Calendar API**
* **Gmail API**
* **Google Sheets API**
* **Pinecone Vector DB**
* **VAPI (AI calling infrastructure)**
* **OpenAI (transcription & embeddings)**

---

## 📎 Notes

You can import any workflow JSON into n8n directly.
Credentials for Gmail, Calendar, Telegram, VAPI, and Google Sheets must be configured separately.
