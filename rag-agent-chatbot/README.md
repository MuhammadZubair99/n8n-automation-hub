# RAG Agent Chatbot (n8n Workflow)

This workflow implements a **Retrieval-Augmented Generation (RAG) chatbot** using n8n.  
It has **two phases**:

1. **Data Ingestion** – Downloads files, converts them into embeddings, and stores them in a vector database.
2. **Chat Agent** – Uses the vector store to answer user questions intelligently.

---

## 📌 Workflow Screenshot
_Add your screenshot below (replace this line with the image)._

![Workflow Screenshot](./workflow.png)

---

## 🧠 Overview of the Workflow

### 🔹 Phase 1 — Build Vector Store (Ingestion Pipeline)
This phase prepares your knowledge base.

Nodes involved:
- **Google Drive Trigger** – Detects new or updated documents.
- **Download File** – Fetches the document from Drive.
- **Pinecone Vector Store (Upsert)** – Saves your processed text & embeddings.
- **Embedding (Google Gemini / OpenAI)** – Converts document text into embeddings.
- **Various text loaders** – Split or process text for vectorization.

**Purpose:**  
To index files (PDF, docs, text, etc.) and store them in Pinecone for semantic search.

---

### 🔹 Phase 2 — Chat Agent (RAG Retrieval + LLM Response)
This phase handles user chat queries.

Nodes involved:
- **When Chat Message Received** – Chat trigger.
- **Pinecone Vector Search** – Retrieves top related chunks.
- **LLM Agent (Google Gemini / OpenAI)** – Generates the final answer.
- **Simplex Memory (optional)** – Stores conversation history.
- **Embeddings for Query** – Converts user question to embedding for semantic search.

**Purpose:**  
To answer user questions using stored knowledge + LLM reasoning.

---

## 🚀 How It Works

### Step 1 — Store Data
When a file is uploaded (Google Drive trigger):
1. File is downloaded.
2. Document text is extracted & chunked.
3. Text chunks are converted to embeddings.
4. Embeddings are stored in Pinecone.

### Step 2 — Answer Queries
1. User sends a chat message.
2. Message is embedded.
3. Related knowledge is retrieved from Pinecone.
4. LLM (Agent) uses context + memory to produce a final answer.

---

## 🧩 Requirements

### Accounts Needed
- **Google Drive**
- **Pinecone**
- **LLM provider (Gemini, OpenAI, etc.)**

### n8n Credentials
- Google Drive Credential  
- Pinecone API Credential  
- LLM Credential  
- Embeddings Credential (Gemini, OpenAI, etc.)

---

## 📁 Files Included

- `workflow.json` – Exported n8n workflow.
- `workflow.png` – Screenshot of the workflow.

---

## ▶️ Setup Guide

1. Import `workflow.json` into n8n.
2. Configure all required credentials:
   - Google Drive
   - Pinecone
   - LLM (Gemini / OpenAI)
3. Update Pinecone:
   - Index name  
   - Namespace  
4. Test the ingestion pipeline with one sample file.
5. Open the n8n chat window and ask questions.

---

## 🛠 Troubleshooting

- **Vector search returns empty**  
  → Check embeddings provider, index name, and namespace.

- **File not processed**  
  → Verify Google Drive trigger permissions.

- **LLM does not answer correctly**  
  → Increase the number of retrieved chunks (e.g., topK = 5–10).

- **Memory not preserved**  
  → Ensure `Simplex Memory` node is connected properly.

---

## 📄 License
Free to use and modify.

\
