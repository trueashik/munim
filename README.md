# Munim.AI - The Bharat Biz-Agent 🇮🇳
> **Neurathon 2026 Submission | Problem Statement 2: The Bharat Biz-Agent**

![Munim AI Banner](assets/app_screenshot.png)

**Munim.AI** is an autonomous, voice-first AI agent that empowers Indian SMBs to manage invoices, track ledgers ('Khata'), and handle business operations entirely through **WhatsApp** and **Telegram**. 

Bridging the digital divide, Munim turns unstructured voice notes (Hinglish) into structured financial data without requiring the user to type or learn complex software.

---

## 🏗️ Architecture & Workflow



The system follows a decoupled Microservices architecture:
1.  **Interface:** Telegram Bot API (Voice & Text Input).
2.  **Orchestrator:** **n8n** (hosted on AWS) manages the logic flow.
3.  **Intelligence:** **Google Gemini 3 Pro** extracts entities (Customer, Amount, Item) from unstructured audio.
4.  **Database:** **Supabase (PostgreSQL)** stores distinct user profiles and ledgers with Row Level Security (RLS).
5.  **Document Engine:** **Gotenberg** (Self-hosted) generates PDF invoices on the fly.
6.  **Voice Engine:** **Whisper** (Self-hosted) analyzes voice with accuracy.

---

## 🚀 Deployment Strategy (Why AWS?)

**Note to Judges:**
To ensure a fully functional "Voice-First" experience with <500ms latency, the backend logic (**n8n**) is hosted live on **AWS EC2**.

* **Reason:** Telegram Bots require secure, public-facing **Webhooks (HTTPS)** to receive real-time updates. Hosting the backend locally (localhost) during evaluation would break the webhook integration.
* **Code Transparency:** While the runtime is cloud-hosted, the **full source code** (workflow logic) is exported and included in this repository under `backend-logic/munim_workflow.json` for your review.

---

## 🛠️ How to Run Locally (Frontend Interface)

[cite_start]We have containerized the Landing Page interface using Docker to fulfill the submission requirements[cite: 5].

### Prerequisites
* Docker Desktop installed.

### Steps
1.  Clone the repository:
    ```bash
    git clone [https://github.com/trueashik/Munim.git](https://github.com/trueashik/Munim.git)
    cd frontend
    ```

2.  Build the Docker Image:
    ```bash
    docker build -t munim-interface .
    ```

3.  Run the Container:
    ```bash
    docker run -p 7860:7860 munim-interface
    ```

4.  **Access the App:** Open `http://localhost:7860`.
    * Clicking "Start Munim" will redirect you to the live, AWS-hosted Telegram Bot.

---

## 💡 Key Features (Problem Statement Fit)

### 1. 🗣️ Voice-First Interaction
* [cite_start]**Constraint Met:** "Primary input method should be Voice"[cite: 114].
* **Implementation:** Users can say *"Rahul ka 500 ka bill banao"* (Hinglish). The bot processes this audio natively.

### 2. 🇮🇳 India-First Engineering
* [cite_start]**Constraint Met:** "Multilingual & Code-Mixed Support"[cite: 100].
* **Implementation:** Handles complex Hinglish queries and understands local context like 'Udhaar' (Credit).

### 3. 📄 Autonomous Action (Agentic AI)
* [cite_start]**Constraint Met:** "Autonomous Task Execution"[cite: 119].
* **Implementation:** The agent doesn't just chat; it performs **DB Writes** (Supabase) and **File Generation** (PDFs) autonomously.

### 4. 🔒 Trust & Safety
* [cite_start]**Constraint Met:** "Human-in-the-Loop Safety"[cite: 108].
* **Implementation:** Critical actions (like sending an invoice to a customer) generate a "Draft" first. The user must click a button to confirm the WhatsApp Deep Link before it is sent.

---

## 🛡️ Privacy & Security
* **Data Storage:** All user data is stored in Supabase.
* **RLS Policies:** Row Level Security is enabled, ensuring users can only query their own ledger data.
* **Encryption:** Data is encrypted at rest and in transit (TLS 1.3).

---

## 📦 Tech Stack
* **Backend:** n8n (AWS EC2)
* **Database:** Supabase
* **AI Model:** Gemini 3 Pro
* **PDF Engine:** Gotenberg
* **Frontend:** HTML5 / Tailwind CSS
* **Containerization:** Docker

---

**Built with ❤️ for Neurathon 2026**
