# AI Multi-Agent Content Pipeline
### Flowise — Sequential Multi-Agent System

A production-ready multi-agent pipeline built in Flowise
that automatically researches course content and generates
publication-ready marketing copy using three specialized
sequential agents.

---

## System Architecture


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
- Full conversation history across all agents
- Publication-ready markdown output
- Configurable for any course or product document

---

## Tech Stack

- Flowise (visual multi-agent builder)
- OpenAI API (gpt-4o-mini + text-embedding-ada-002)
- FAISS (Meta vector store — local)
- LangChain Sequential Agents
- Docx File Loader

---

## Agent Configuration

| Setting | Value |
|---|---|
| Model | gpt-4o-mini |
| Temperature | 0.9 |
| Embeddings | text-embedding-ada-002 |
| Vector Store | FAISS (local) |
| Document Type | DOCX |
| Output Format | Markdown tweet |

---

## Setup & Import

2. Open Flowise at http://localhost:3000

3. Import the agent:
   - Click **Chatflows** → **Add New**
   - Click **Import**
   - Upload `multi_agent_content_pipeline.json`

4. Add your OpenAI API key in Flowise credentials

5. Update the FAISS path to your local machine
   in the Faiss node

6. Upload your DOCX course document in the
   Docx File Loader node

7. Click **Save** and **Deploy**

8. Enter a course name to start the pipeline

---

## Example Output

**Input:** Course name entered in chat

**Search Agent output:**
Detailed course topics, expanded descriptions,
and suggested target audience

**Writer Agent output:**
Draft 4-block marketing tweet with call to action

**Editor Agent output (final):**

---

## Customization

**Change the document source:**
Replace the DOCX file with any course, product,
or content document.

**Adjust tweet style:**
Modify the Writer Agent system prompt to change
tone, length, or format of the output.

**Add more agents:**
Extend the pipeline with additional agents —
for example a Social Media Scheduler agent or
a LinkedIn Post agent after the Editor.

**Scale the vector store:**
Swap FAISS for Pinecone or Chroma for larger
document collections.

---

## Author

Paul Orlando
Creative Technologist | AI Agent Developer | Data Analytics
🌐 paulforlando.com
💼 linkedin.com/in/paul-orlando-7841b5154
🐙 github.com/Paul-Orlando
