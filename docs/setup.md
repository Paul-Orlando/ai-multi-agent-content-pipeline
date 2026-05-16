# Setup Guide

This guide explains how to install, configure, and run the AI Multi-Agent Content Pipeline locally.

---

# Prerequisites

Before starting, ensure the following tools are installed:

| Tool              | Recommended Version |
| ----------------- | ------------------- |
| Node.js           | 18+                 |
| npm               | Latest              |
| Docker (optional) | Latest              |
| OpenAI API Key    | Required            |

---

# Clone Repository

```bash id="jlwm103"
git clone <repository-url>

cd ai-multi-agent-content-pipeline
```

---

# Install Dependencies

```bash id="jlwm104"
npm install
```

---

# Environment Configuration

Create a local `.env` file:

```bash id="jlwm105"
cp .env.example .env
```

---

# Required Environment Variables

Example configuration:

```env id="jlwm106"
OPENAI_API_KEY=

MODEL_NAME=gpt-4o-mini

EMBEDDING_MODEL=text-embedding-ada-002

FAISS_DB_PATH=./vectorstore/faiss

FLOWISE_PORT=3000
```

---

# Environment Variable Descriptions

| Variable        | Purpose                    |
| --------------- | -------------------------- |
| OPENAI_API_KEY  | OpenAI authentication      |
| MODEL_NAME      | Primary chat model         |
| EMBEDDING_MODEL | Embedding generation model |
| FAISS_DB_PATH   | Local vector database path |
| FLOWISE_PORT    | Application server port    |

---

# Folder Initialization

Create required local directories:

```bash id="jlwm107"
mkdir -p vectorstore/faiss

mkdir -p outputs

mkdir -p logs
```

---

# Running the Application

## Development Mode

```bash id="jlwm108"
npm start
```

---

## Docker Mode

```bash id="jlwm109"
docker compose up
```

---

# Workflow Import

Import the workflow JSON into Flowise.

---

# Workflow File

```plaintext id="jlwm110"
multi_agent_content_pipeline.json
```

---

# Import Steps

1. Open Flowise
2. Navigate to Chatflows
3. Click Import
4. Select:

```plaintext id="jlwm111"
multi_agent_content_pipeline.json
```

5. Save workflow
6. Configure credentials
7. Start execution

---

# OpenAI Credential Setup

Inside Flowise:

1. Open Credentials
2. Create OpenAI Credential
3. Add API key
4. Save credential
5. Attach credential to:

   * ChatOpenAI node
   * OpenAI Embeddings node

---

# Document Preparation

Supported document format:

```plaintext id="jlwm112"
.docx
```

---

# Recommended Document Types

* course materials
* training guides
* learning modules
* educational documentation

---

# Embedding Workflow

```plaintext id="jlwm113"
DOCX Files
    ↓
Embedding Generation
    ↓
FAISS Index Creation
```

---

# Running a Sample Query

Example input:

```plaintext id="jlwm114"
AI Product Management Course
```

---

# Expected Workflow Execution

```plaintext id="jlwm115"
Retrieve Context
    ↓
Search Agent Analysis
    ↓
Writer Agent Generation
    ↓
Editor Agent Refinement
```

---

# Output Example

```markdown id="jlwm116"
Master AI Product Strategy with practical frameworks, prompt engineering techniques, and workflow automation methods.

Enroll today and start building AI-driven products with confidence.
```

---

# Recommended Local Development Structure

```plaintext id="jlwm117"
vectorstore/
outputs/
logs/
docs/
prompts/
tests/
```

---

# Debugging Tips

---

# Common Issue — Missing OpenAI Key

## Error

```plaintext id="jlwm118"
Authentication Error
```

## Solution

Verify:

```env id="jlwm119"
OPENAI_API_KEY=
```

is configured correctly.

---

# Common Issue — Empty Retrieval Results

## Causes

* embeddings not generated
* vector store missing
* incorrect FAISS path
* empty documents

## Solution

Rebuild embeddings and verify:

```plaintext id="jlwm120"
./vectorstore/faiss
```

exists.

---

# Common Issue — Flowise Import Errors

## Solution

Verify:

* compatible Flowise version
* valid workflow JSON
* node dependencies installed

---

# Recommended Development Workflow

```plaintext id="jlwm121"
Update Documents
      ↓
Regenerate Embeddings
      ↓
Run Workflow
      ↓
Validate Outputs
      ↓
Refine Prompts
```

---

# Performance Recommendations

Recommended optimizations:

| Optimization           | Benefit               |
| ---------------------- | --------------------- |
| Chunk Documents        | Better retrieval      |
| Cache Embeddings       | Faster startup        |
| Persistent FAISS Index | Reduced recomputation |
| Batch Embedding Calls  | Lower API overhead    |

---

# Security Recommendations

Never commit:

* `.env`
* API keys
* generated credentials
* sensitive documents

Ensure `.gitignore` excludes all secrets.

---

# Recommended Production Improvements

Future production enhancements may include:

* managed vector databases
* distributed orchestration
* workflow monitoring
* agent analytics
* observability tooling
* secure secret management

---

# Verification Checklist

Before running the workflow:

* OpenAI API key configured
* dependencies installed
* workflow imported
* FAISS directory created
* documents uploaded
* embeddings generated

---

# Summary

The setup process consists of:

1. installing dependencies
2. configuring environment variables
3. importing the workflow
4. generating embeddings
5. executing the multi-agent pipeline

Once configured, the system can automatically transform source course materials into publication-ready marketing content.
