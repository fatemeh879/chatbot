# 📦 Installation Guide

Complete step-by-step guide to set up and run the RAG Chatbot.

---

## Prerequisites

### Required Software

1. **Python 3.8 or higher**
   - Download from [python.org](https://www.python.org/downloads/)
   - Verify installation: `python --version`

2. **Ollama**
   - Download from [ollama.ai/download](https://ollama.ai/download)
   - Follow installation instructions for your OS

3. **Git** (optional, for cloning)
   - Download from [git-scm.com](https://git-scm.com/downloads)

---

## Step 1: Install Ollama

### Windows
1. Download the installer from [ollama.ai/download](https://ollama.ai/download)
2. Run the installer
3. Verify: Open Command Prompt and run `ollama --version`

### Linux/Mac
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

Verify installation:
```bash
ollama --version
```

---

## Step 2: Download Required Models

After installing Ollama, download the required models:

```bash
# Download chat model (llama3.2 - approximately 2GB)
ollama pull llama3.2

# Download embeddings model (mxbai-embed-large - approximately 670MB)
ollama pull mxbai-embed-large
```

**Note**: Model downloads may take several minutes depending on your internet connection.

Verify models are installed:
```bash
ollama list
```

You should see:
```
NAME                        SIZE      MODIFIED
llama3.2:latest            2.0 GB    ...
mxbai-embed-large:latest    669 MB    ...
```

---

## Step 3: Clone or Download Repository

### Option A: Clone with Git
```bash
git clone https://github.com/fatemeh879/chatbot.git
cd chatbot
```

### Option B: Download ZIP
1. Go to [github.com/fatemeh879/chatbot](https://github.com/fatemeh879/chatbot)
2. Click "Code" → "Download ZIP"
3. Extract the ZIP file
4. Open terminal in the extracted folder

---

## Step 4: Create Virtual Environment

### Windows
```bash
python -m venv venv
venv\Scripts\activate
```

### Linux/Mac
```bash
python3 -m venv venv
source venv/bin/activate
```

**Note**: Your terminal prompt should now show `(venv)` indicating the virtual environment is active.

---

## Step 5: Install Python Dependencies

```bash
pip install -r requirements.txt
```

This will install:
- FastAPI
- LangChain
- ChromaDB
- Ollama integrations
- And other required packages

**Note**: Installation may take a few minutes.

---

## Step 6: Configure Environment

Create a `.env` file in the project root:

**Windows:**
```bash
copy .env.example .env
```

**Linux/Mac:**
```bash
cp .env.example .env
```

Edit `.env` with your preferred settings:

```env
# Model Settings
EMBEDDINGS_MODEL_NAME=mxbai-embed-large
CHAT_MODEL_NAME=llama3.2
CHAT_TEMPERATURE=0.3

# Vector Store
CHROMA_DB_PATH=./chroma_db
COLLECTION_NAME=knowledge_base

# Data Source (change to your content)
URL_PATH=https://example.com/your-content

# Logging
LOG_PATH=./logs/app_run.log
```

---

## Step 7: Ingest Data

Before using the chatbot, you need to ingest some data:

```bash
python ingest_cli.py
```

This will:
1. Extract text from the URL specified in `.env`
2. Chunk the text into smaller pieces
3. Generate embeddings
4. Store in ChromaDB

**Note**: First ingestion may take a few minutes.

---

## Step 8: Start the Application

### Terminal 1: Start Ollama (if not running)
```bash
ollama serve
```

### Terminal 2: Start the Chatbot
```bash
# Make sure virtual environment is activated
python main.py
```

You should see:
```
INFO:     Started server process
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000
```

---

## Step 9: Access the Chatbot

Open your web browser and navigate to:

```
http://localhost:8000
```

You should see the chat interface!

---

## Verification Checklist

- [ ] Python 3.8+ installed
- [ ] Ollama installed and running
- [ ] Models downloaded (llama3.2, mxbai-embed-large)
- [ ] Repository cloned/downloaded
- [ ] Virtual environment created and activated
- [ ] Dependencies installed
- [ ] `.env` file configured
- [ ] Data ingested
- [ ] Ollama server running
- [ ] Application started
- [ ] Browser can access `http://localhost:8000`

---

## Troubleshooting

### Issue: "Ollama not found"
**Solution**: 
- Make sure Ollama is installed
- Add Ollama to your PATH
- Restart terminal

### Issue: "Models not found"
**Solution**:
```bash
ollama pull llama3.2
ollama pull mxbai-embed-large
```

### Issue: "Port 8000 already in use"
**Solution**: 
- Change port in `main.py`
- Or stop the process using port 8000

### Issue: "No module named 'xxx'"
**Solution**:
```bash
pip install -r requirements.txt
```

### Issue: "ChromaDB errors"
**Solution**:
- Delete `chroma_db` folder
- Re-run ingestion

---

## Next Steps

1. **Customize your knowledge base**: Ingest your own documents
2. **Adjust settings**: Modify `.env` for your needs
3. **Test queries**: Try different questions
4. **Explore features**: Check out all the capabilities

---

## Getting Help

If you encounter issues:
1. Check the troubleshooting section above
2. Review logs in `logs/app_run.log`
3. Verify all prerequisites are installed
4. Check GitHub issues (if available)

---

*Happy chatting! 🚀*

