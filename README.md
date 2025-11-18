# 🤖 RAG Chatbot - Domain-Specific AI Assistant

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.95+-green.svg)
![LangChain](https://img.shields.io/badge/LangChain-Latest-orange.svg)
![Ollama](https://img.shields.io/badge/Ollama-Local-purple.svg)
![ChromaDB](https://img.shields.io/badge/ChromaDB-Vector%20Store-teal.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

**A Production-Ready Retrieval-Augmented Generation (RAG) Chatbot**

*Built with Local LLMs • No API Keys Required • Fully Private & Secure*

[Features](#-features) • [Architecture](#-architecture) • [Demo](#-demo) • [Tech Stack](#-tech-stack) • [Installation](#-installation)

</div>

---

## 📖 Overview

This is a **domain-specific RAG (Retrieval-Augmented Generation) chatbot** that answers questions based solely on your own knowledge base. Unlike generic chatbots, this system:

- ✅ **Only answers from ingested documents** - No hallucinations from general knowledge
- ✅ **Runs entirely locally** - No cloud APIs, no data leaving your machine
- ✅ **Production-ready** - Built with FastAPI, proper error handling, and logging
- ✅ **Smart retrieval** - Uses semantic search with similarity thresholds
- ✅ **Conversation memory** - Maintains context across messages
- ✅ **Beautiful UI** - Modern, responsive chat interface

### 🎯 Use Cases

- **Document Q&A**: Answer questions about your documentation, manuals, or knowledge base
- **Domain-Specific Assistants**: Create specialized chatbots for specific topics
- **Private Knowledge Bases**: Keep sensitive information local and secure
- **Educational Tools**: Help students learn from course materials
- **Internal Company Assistants**: Answer questions about company policies, procedures, etc.

---

## ✨ Features

### Core Features

| Feature | Description |
|---------|-------------|
| 🔍 **Semantic Search** | Uses vector embeddings to find relevant context from your knowledge base |
| 🧠 **Local LLM** | Runs on your CPU using Ollama - no cloud dependencies |
| 💾 **Vector Store** | ChromaDB for efficient document storage and retrieval |
| 💬 **Conversation Memory** | Maintains context across multiple messages |
| 🎯 **Domain-Specific** | Only answers from your knowledge base - rejects unrelated questions |
| 📚 **Multiple Data Sources** | Ingest from URLs, text files, or multiple sources |
| 🌐 **Web Interface** | Beautiful, responsive chat UI built with Vue.js |
| 🔒 **Privacy-First** | Everything runs locally - your data never leaves your machine |

### Advanced Features

- **Smart Retrieval**: Similarity threshold filtering to ensure relevant context
- **Response Validation**: Detects potential hallucinations
- **Error Handling**: Robust error handling with fallback mechanisms
- **Logging**: Comprehensive logging for debugging and monitoring
- **CLI Tools**: Command-line interface for data ingestion
- **Chunk Inspection**: Tools to verify and debug your knowledge base

---

## 🏗️ Architecture

### System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    USER INTERFACE                            │
│              (Vue.js Chat Interface)                         │
└──────────────────────┬──────────────────────────────────────┘
                       │ HTTP/REST API
┌──────────────────────▼──────────────────────────────────────┐
│                   FASTAPI BACKEND                            │
│  • REST API Endpoints                                        │
│  • Request/Response Handling                                 │
│  • Error Handling                                            │
└──────────────────────┬──────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────┐
│                   RAG PIPELINE                               │
│  ┌──────────────┐      ┌──────────────┐                     │
│  │  Retrieval   │─────▶│  Generation  │                     │
│  │   Module     │      │    Module    │                     │
│  └──────────────┘      └──────────────┘                     │
└──────────────────────┬──────────────────────────────────────┘
                       │
        ┌──────────────┼──────────────┐
        │              │              │
┌───────▼──────┐ ┌─────▼──────┐ ┌────▼──────┐
│  ChromaDB    │ │   Ollama   │ │  Ollama   │
│ Vector Store │ │ Embeddings │ │ Chat LLM  │
│              │ │   Model    │ │  Model    │
└──────────────┘ └────────────┘ └───────────┘
```

### Data Flow

```
1. INGESTION (One-time setup)
   ┌─────────────┐
   │   Document  │
   └──────┬──────┘
          │
          ▼
   ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
   │   Chunking  │─────▶│ Embedding   │─────▶│  ChromaDB   │
   │             │      │  (Ollama)   │      │  Storage    │
   └─────────────┘      └─────────────┘      └─────────────┘

2. QUERY PROCESSING (Every question)
   ┌─────────────┐
   │ User Query  │
   └──────┬──────┘
          │
          ▼
   ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
   │ Embedding   │─────▶│  Similarity │─────▶│  Retrieve   │
   │  (Ollama)   │      │   Search    │      │  Context    │
   └─────────────┘      └─────────────┘      └──────┬───────┘
                                                    │
                                                    ▼
   ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
   │   Context   │─────▶│   LLM       │─────▶│  Response   │
   │  + Query   │      │ (Ollama)    │      │             │
   └─────────────┘      └─────────────┘      └─────────────┘
```

### Component Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        FRONTEND                              │
│  • Vue.js 3 (CDN)                                            │
│  • Modern Chat UI                                            │
│  • Responsive Design                                         │
└──────────────────────┬──────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────────┐
│                        BACKEND                               │
│  ┌──────────────────────────────────────────────────────┐  │
│  │  FastAPI Application                                  │  │
│  │  • /chat endpoint                                     │  │
│  │  • Static file serving                                │  │
│  │  • CORS middleware                                    │  │
│  └──────────────────┬───────────────────────────────────┘  │
│                     │                                       │
│  ┌──────────────────▼───────────────────────────────────┐  │
│  │  RAG Pipeline                                         │  │
│  │  • Query processing                                   │  │
│  │  • Document retrieval                                 │  │
│  │  • Response generation                                │  │
│  │  • Conversation memory                               │  │
│  └──────────────────┬───────────────────────────────────┘  │
└─────────────────────┼──────────────────────────────────────┘
                      │
        ┌─────────────┼─────────────┐
        │             │             │
┌───────▼──────┐ ┌───▼──────┐ ┌───▼──────┐
│  ChromaDB    │ │  Ollama  │ │  Ollama  │
│              │ │          │ │          │
│ • Vector     │ │ • mxbai- │ │ • llama3.│
│   Storage    │ │   embed- │ │   2      │
│ • Metadata   │ │   large  │ │          │
│ • Similarity │ │          │ │          │
│   Search     │ │          │ │          │
└──────────────┘ └──────────┘ └──────────┘
```

---

## 🛠️ Tech Stack

### Backend
- **FastAPI** - Modern, fast web framework for building APIs
- **LangChain** - Framework for LLM applications and RAG pipelines
- **ChromaDB** - Open-source vector database
- **Ollama** - Local LLM inference engine
- **Python 3.8+** - Programming language

### Frontend
- **Vue.js 3** - Progressive JavaScript framework
- **Modern CSS** - Custom styling with CSS variables
- **Responsive Design** - Works on desktop and mobile

### Models
- **llama3.2** - Chat/Generation model (2GB)
- **mxbai-embed-large** - Embeddings model (670MB)

### Tools
- **BeautifulSoup4** - Web scraping and HTML parsing
- **Requests** - HTTP library for fetching URLs
- **Uvicorn** - ASGI server for FastAPI

---

## 📦 Installation

### Prerequisites

1. **Python 3.8+** - [Download Python](https://www.python.org/downloads/)
2. **Ollama** - [Install Ollama](https://ollama.ai/download)

### Step 1: Install Ollama

**Windows:**
- Download from [ollama.ai/download](https://ollama.ai/download)
- Run the installer

**Linux/Mac:**
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

### Step 2: Download Required Models

```bash
# Download chat model (2GB)
ollama pull llama3.2

# Download embeddings model (670MB)
ollama pull mxbai-embed-large
```

### Step 3: Clone Repository

```bash
git clone https://github.com/fatemeh879/chatbot.git
cd chatbot
```

### Step 4: Install Dependencies

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Step 5: Configure Environment

Create a `.env` file:

```env
# Model Settings
EMBEDDINGS_MODEL_NAME=mxbai-embed-large
CHAT_MODEL_NAME=llama3.2
CHAT_TEMPERATURE=0.3

# Vector Store
CHROMA_DB_PATH=./chroma_db
COLLECTION_NAME=knowledge_base

# Data Source
URL_PATH=https://example.com/your-content

# Logging
LOG_PATH=./logs/app_run.log
```

### Step 6: Run the Application

```bash
# Start Ollama (if not running)
ollama serve

# In another terminal, start the application
python main.py
```

Visit `http://localhost:8000` in your browser.

---

## 🚀 Quick Start

1. **Ingest your data:**
   ```bash
   python ingest_cli.py
   ```

2. **Start the chatbot:**
   ```bash
   python main.py
   ```

3. **Open in browser:**
   ```
   http://localhost:8000
   ```

---

## 📸 Demo

### UI Screenshots

*[Add your UI screenshots here]*

### Demo Video

*[Add your demo video link here]*

---

## 🎯 Key Features Explained

### 1. Domain-Specific Answers

The chatbot is designed to **only answer questions based on your ingested knowledge base**. It will:
- ✅ Answer questions when context is found
- ❌ Reject questions outside the knowledge domain
- 📚 Inform users about available topics

### 2. Semantic Search

Uses **vector embeddings** to find semantically similar content, not just keyword matches. This means:
- Finds relevant context even if exact words don't match
- Understands synonyms and related concepts
- Filters by similarity threshold for quality

### 3. Local & Private

Everything runs on your machine:
- No cloud APIs
- No data transmission
- No API keys required
- Complete privacy

### 4. Production-Ready

Built with best practices:
- Error handling and logging
- Response validation
- Conversation memory
- Clean architecture

---

## 📊 Performance

- **Response Time**: ~2-5 seconds (depends on CPU)
- **Memory Usage**: ~4-6GB RAM (for models + system)
- **Storage**: ~3GB for models, varies for vector store
- **Concurrent Users**: Supports multiple users (limited by CPU)

---

## 🔒 Privacy & Security

- ✅ **100% Local**: No data leaves your machine
- ✅ **No API Keys**: No external service dependencies
- ✅ **Open Source Models**: Using open-source LLMs
- ✅ **Data Control**: You control all data and storage

---

## 📝 Project Structure

```
chatbot/
├── frontend/          # Vue.js chat interface
├── core/              # Core utilities and configuration
├── models/            # LLM model wrappers
├── rag/               # RAG pipeline implementation
├── vector_store/      # ChromaDB integration
├── data/              # Sample data files
├── logs/              # Application logs
└── main.py           # FastAPI application entry point
```

---

## 🤝 Contributing

This is a portfolio project. Feel free to:
- ⭐ Star the repository
- 🍴 Fork and customize
- 📝 Report issues
- 💡 Suggest improvements

---

## 📄 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgments

Built with amazing open-source tools:
- [LangChain](https://langchain.com/) - RAG framework
- [Ollama](https://ollama.ai/) - Local LLM inference
- [ChromaDB](https://www.trychroma.com/) - Vector database
- [FastAPI](https://fastapi.tiangolo.com/) - Web framework
- [Vue.js](https://vuejs.org/) - Frontend framework

---

## 📧 Contact

**Developer**: Fatemeh  
**GitHub**: [@fatemeh879](https://github.com/fatemeh879)  
**Repository**: [chatbot](https://github.com/fatemeh879/chatbot)

---

<div align="center">

**⭐ If you find this project interesting, please give it a star! ⭐**

Made with ❤️ using Python, FastAPI, and Local LLMs

</div>

