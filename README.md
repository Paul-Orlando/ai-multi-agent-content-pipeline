# AI Multi-Agent Content Pipeline
### Flowise — Sequential Multi-Agent System

A production-ready multi-agent pipeline built in Flowise that automatically
researches course content and generates publication-ready marketing copy
using three specialized sequential agents.

---

## System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    INPUT LAYER                          │
│                                                         │
│              📄 DOCX File (course content)              │
└─────────────────────────┬───────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                  KNOWLEDGE LAYER                        │
│                                                         │
│       🔢 OpenAI Embeddings (text-embedding-ada-002)     │
│                          │                              │
│                          ▼                              │
│            🗄️  FAISS Vector Store (local)               │
└─────────────────────────┬───────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│              AGENT 1 — Search Agent                     │
│                                                         │
│  → Retrieves course info from FAISS vector store        │
│  → Expands on each topic                                │
│  → Identifies target audience                           │
│                                                         │
│  Output: Detailed course summary + target audience      │
└─────────────────────────┬───────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│              AGENT 2 — Writer Agent                     │
│                                                         │
│  → Receives Search Agent output                         │
│  → Writes a structured 4-block marketing tweet          │
│  → Includes clear call to action                        │
│  → Proofreads for grammatical errors                    │
│                                                         │
│  Output: Draft tweet in markdown format                 │
└─────────────────────────┬───────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│              AGENT 3 — Editor Agent                     │
│                                                         │
│  → Edits for grammar and conciseness                    │
│  → Removes hashtags, emojis, and noisy details          │
│  → Finalizes structure and readability                  │
│                                                         │
│  Output: Publication-ready tweet in markdown            │
└─────────────────────────┬───────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                   FINAL OUTPUT                          │
│                                                         │
│         ✅ Tweet — Markdown, Ready to Publish           │
└─────────────────────────────────────────────────────────┘
```

---

## Agent Roles

| Agent | Role | Responsibility |
|---|---|---|
| Search Agent | Researcher | Retrieves and expands course topics, identifies target audience |
| Writer Agent | Marketing Manager | Writes structured 4-block tweet with call to action |
| Editor Agent | Editor | Refines grammar, removes noise, finalizes for publication |

---

## Key Features

- Three specialized sequential agents — each with a single responsibility
- RAG-powered research — grounded in actual document content
- FAISS vector store for fast local similarity search
- Structured agent prompts with tasks and expected outputs
- Full conversation history shared across all agents
- Publication-ready markdown output
- Configurable for any course or product document

---

## Tech Stack

- **Flowise** — visual multi-agent builder
- **OpenAI API** — gpt-4o-mini + text-embedding-ada-002
- **FAISS** — Meta vector store (local)
- **LangChain** — Sequential Agents framework
- **Docx File Loader** — document ingestion

---

## Agent Configuration

| Setting | Value |
|---|---|
| Model | gpt-4o-mini |
| Temperature | 0.9 |
| Embeddings | text-embedding-ada-002 |
| Vector Store | FAISS (local) |
| Document Type | DOCX |
| Conversation History | All messages (shared across agents) |
| Output Format | Markdown tweet |

---

## Setup & Import

1. Install and run Flowise:
```bash
npm install -g flowise
npx flowise start
```

2. Open Flowise at `http://localhost:3000`

3. Import the agent:
   - Click **Chatflows** → **Add New**
   - Click **Import**
   - Upload `multi_agent_content_pipeline.json`

4. Add your OpenAI API key in Flowise credentials

5. Update the FAISS base path in the Faiss node
   to your local machine path

6. Upload your DOCX course document in the
   Docx File Loader node

7. Click **Save** and **Deploy**

8. Enter a course name to start the pipeline

---

## Example Output

**Input:** Course name entered in chat

**Search Agent** retrieves and expands course topics,
identifies target audience from embedded document.

**Writer Agent** produces a structured 4-block draft:

```
Unlock the future of AI with our Advanced Prompt
Engineering course.

Master chain-of-thought, few-shot, and zero-shot
prompting techniques used by top AI engineers.

Designed for developers and technical professionals
ready to level up their LLM applications.

Enroll now and start building smarter AI systems today.
```

**Editor Agent** refines grammar, removes noise,
and confirms publication readiness.

---

## Customization

**Change the document source**
Replace the DOCX file with any course, product,
or content document.

**Adjust tweet style**
Modify the Writer Agent system prompt to change
tone, length, or format of the output.

**Add more agents**
Extend the pipeline — add a LinkedIn Post agent,
a Social Media Scheduler agent, or a Translation agent
after the Editor.

**Scale the vector store**
Swap FAISS for Pinecone or Chroma for larger
document collections or cloud deployment.

---

## Changelog

See [changelog.md](changelog.md) for full version history.

---

## Author

Paul Orlando
Creative Technologist | AI Agent Developer | Data Analytics
🌐 [paulforlando.com](https://www.paulforlando.com)
💼 [LinkedIn](https://www.linkedin.com/in/paul-orlando-7841b5154)
🐙 [GitHub](https://github.com/Paul-Orlando)
