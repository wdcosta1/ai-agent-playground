# AI Agent Playground

<img width="3717" height="1932" alt="image" src="https://github.com/user-attachments/assets/dadf9b0b-d7a5-44e6-b025-1c5be64938c1" />

A full-stack AI application built to explore modern agent architectures with **LangChain**, **LangGraph**, and **Retrieval-Augmented Generation (RAG)**.

The project demonstrates how conversational AI, document retrieval, persistent memory, and tool-calling agents can work together in a production-style application.

---

## Features

### Intelligent Chat Agent

* Chat with a local LLM running through Ollama
* Persistent conversations across page refreshes
* Tool-calling support powered by LangGraph

### Retrieval-Augmented Generation (RAG)

* Upload PDF, Markdown, and text documents
* Automatic document chunking and vector indexing
* Semantic search using FAISS and local embeddings
* Answers grounded in your own knowledge base

### Autonomous Tool Selection

The agent decides when to:

* Search uploaded documents
* Recall stored user information
* Answer directly from model knowledge

No manual mode switching required.

### Long-Term Memory

<img width="3707" height="1825" alt="image" src="https://github.com/user-attachments/assets/d39890c5-6fe9-48f2-b77b-91217ea814ef" />


* Stores facts about the user across sessions
* Persists memory to disk
* Demonstrates LangGraph's thread memory vs. persistent memory patterns

### Session Management

* Multiple chat sessions
* Export conversations to PDF or DOCX
* Session history persists between visits

---

## Architecture Overview

The application combines three major AI patterns:

### 1. LangChain Pipelines

Reusable prompt templates and LCEL chains power structured AI workflows and utility features such as code explanation.

### 2. Retrieval-Augmented Generation

Documents move through a complete ingestion pipeline:

Document Loading → Chunking → Embedding → FAISS Vector Store → Semantic Retrieval

The project demonstrates the distinction between:

* **Ingestion** — one-time indexing process
* **Retrieval** — runtime document search during conversations

### 3. LangGraph Agents

The application uses a stateful agent graph with two memory systems:

#### Thread Memory

Managed by `MemorySaver`

* Conversation-specific state
* Persists within a chat thread

#### Persistent Memory

Managed by `InMemoryStore`

* Stores user facts
* Shared across sessions
* Persisted to disk

The agent has access to two tools:

* `search_documents`
* `save_memory`

Conditional graph edges allow the model to repeatedly call tools until it can generate a final response.

---

## What I Learned

This project was built primarily as a learning exercise to understand how modern AI applications are structured beyond simple chat interfaces.

Key concepts explored:

* LangChain prompt composition and LCEL
* Tool calling and agent orchestration
* LangGraph state machines and memory systems
* Vector databases and semantic retrieval
* Embedding models and document indexing
* Full-stack AI application architecture
* Local-first AI development with Ollama
* React state management for AI applications

---

## Tech Stack

### Backend

* Python
* FastAPI
* LangChain
* LangGraph
* FAISS
* Ollama

### Frontend

* Next.js 16
* React 19
* TypeScript
* Zustand
* TanStack Query
* Tailwind CSS v4

---

## Project Structure

```text
backend/
├── agents/
├── chains/
├── graphs/
├── models/
└── services/

frontend/
├── app/
├── components/
├── hooks/
├── lib/
└── store/
```

The folder structure intentionally separates LangChain components from LangGraph components to make the responsibilities of each framework easier to understand.

---

## Getting Started

### Prerequisites

#### Python 3.10+

```bash
python --version
```

#### Node.js 20+

```bash
node --version
```

#### Ollama

Install Ollama and pull the required models:

```bash
# Chat model
ollama pull llama3.1:8b

# Embedding model
ollama pull nomic-embed-text
```

Optional smaller model:

```bash
ollama pull mistral
```

Then update the model configuration in:

```python
backend/models/llm.py
```

---

## Installation

### Backend

```bash
cd backend

python -m venv .venv

# Windows
.venv\Scripts\activate

# Mac/Linux
source .venv/bin/activate

pip install -r requirements.txt
```

Create:

```text
backend/.env
```

Example:

```env
ANTHROPIC_API_KEY=
```

Only required if switching from Ollama to Anthropic.

### Frontend

```bash
cd frontend
npm install
```

---

## Running the Application

### Backend

```bash
cd backend
uvicorn app:app --reload
```

Backend:

```text
http://localhost:8000
```

Swagger Docs:

```text
http://localhost:8000/docs
```

### Frontend

```bash
cd frontend
npm run dev
```

Frontend:

```text
http://localhost:3000/chat
```

### Ollama

```bash
ollama serve
```

On most systems Ollama starts automatically.

---

## First Use

1. Open `http://localhost:3000/chat`
2. Start a conversation with the assistant
3. Open the side panel and navigate to **Docs**
4. Upload documents and click **Re-index**
5. Ask questions about your uploaded content
6. Explore stored user facts in the **Memory** tab
7. View the agent architecture in the **About** tab

---

## Future Improvements

* Multiple vector store backends
* Streaming responses
* Multi-agent workflows
* Web search integration
* Human-in-the-loop approvals
* Authentication and user accounts
* Cloud deployment support

---

## Why This Project Exists

Most AI tutorials focus on isolated concepts such as prompting, RAG, or agents.

This project combines those concepts into a single application that demonstrates how modern AI systems can use:

* Tools
* Memory
* Retrieval
* State
* Agent orchestration

to create a more capable and realistic user experience.
