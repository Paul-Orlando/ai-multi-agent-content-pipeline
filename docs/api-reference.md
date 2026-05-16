# API & Workflow Reference

This document provides a technical reference for the AI Multi-Agent Content Pipeline workflow configuration, execution schema, node structure, and shared state management.

The goal is to provide developers with a clear understanding of:

* workflow configuration
* node interfaces
* shared state
* prompt variables
* retrieval contracts
* agent inputs and outputs

---

# Workflow File

Primary workflow configuration:

```plaintext id="jlwm155"
multi_agent_content_pipeline.json
```

---

# Workflow Structure

The workflow is composed of:

```plaintext id="jlwm156"
Nodes
    +
Edges
    +
Shared State
    +
Prompt Variables
```

---

# High-Level Workflow Graph

```plaintext id="jlwm157"
Start
  ↓
Search Agent
  ↓
Writer Agent
  ↓
Editor Agent
  ↓
End
```

---

# JSON Workflow Schema

The workflow JSON contains two primary sections:

| Section | Purpose             |
| ------- | ------------------- |
| nodes   | Workflow components |
| edges   | Node connections    |

---

# Node Schema

Each node follows a structure similar to:

```json id="jlwm158"
{
  "id": "node_id",
  "type": "customNode",
  "data": {},
  "position": {},
  "width": 300,
  "height": 400
}
```

---

# Core Workflow Nodes

| Node              | Purpose                        |
| ----------------- | ------------------------------ |
| Start Node        | Workflow initialization        |
| Search Agent      | Research & retrieval reasoning |
| Writer Agent      | Marketing content generation   |
| Editor Agent      | Editorial refinement           |
| Retriever Tool    | Semantic retrieval             |
| FAISS             | Vector search                  |
| OpenAI Embeddings | Embedding generation           |
| DOCX Loader       | Document ingestion             |
| End Node          | Final output                   |

---

# 1. Start Node Reference

---

# Purpose

Initializes workflow execution.

---

# Responsibilities

* loads chat model
* initializes state
* handles user input
* manages conversation context

---

# Example Configuration

```json id="jlwm159"
{
  "type": "Start",
  "model": "ChatOpenAI",
  "state": {}
}
```

---

# Inputs

| Input      | Type          |
| ---------- | ------------- |
| User Query | string        |
| Chat Model | BaseChatModel |
| State      | object        |

---

# Outputs

| Output           | Type   |
| ---------------- | ------ |
| Workflow Context | object |

---

# 2. Search Agent Reference

---

# Purpose

Research and reasoning layer.

---

# Responsibilities

* retrieval reasoning
* topic extraction
* audience analysis

---

# Prompt Variables

| Variable   | Type   |
| ---------- | ------ |
| `{course}` | string |

---

# Example Prompt Injection

```json id="jlwm160"
{
  "course": "{{question}}"
}
```

---

# Inputs

| Input             | Source         |
| ----------------- | -------------- |
| Retrieved Context | Retriever Tool |
| User Query        | Workflow input |
| Shared State      | Workflow state |

---

# Outputs

| Output            | Type          |
| ----------------- | ------------- |
| Research Insights | markdown/text |

---

# Example Output

```markdown id="jlwm161"
# Topics
- AI Strategy
- Prompt Engineering

# Audience
- Product Managers
- AI Teams
```

---

# 3. Writer Agent Reference

---

# Purpose

Marketing content generation.

---

# Responsibilities

* social copy generation
* CTA creation
* formatting optimization

---

# Inputs

| Input             | Source       |
| ----------------- | ------------ |
| Research Insights | Search Agent |

---

# Outputs

| Output          | Type          |
| --------------- | ------------- |
| Marketing Draft | markdown/text |

---

# Example Output

```markdown id="jlwm162"
Master AI Product Strategy with practical frameworks and workflow automation techniques.

Enroll today.
```

---

# 4. Editor Agent Reference

---

# Purpose

Final content refinement.

---

# Responsibilities

* grammar correction
* concise rewriting
* publication cleanup

---

# Inputs

| Input           | Source       |
| --------------- | ------------ |
| Marketing Draft | Writer Agent |

---

# Outputs

| Output        | Type          |
| ------------- | ------------- |
| Final Content | markdown/text |

---

# 5. Retriever Tool Reference

---

# Tool Name

```plaintext id="jlwm163"
search_course
```

---

# Purpose

Semantic retrieval interface.

---

# Responsibilities

* receive queries
* search vector store
* return relevant chunks

---

# Inputs

| Input | Type   |
| ----- | ------ |
| Query | string |

---

# Outputs

| Output              | Type  |
| ------------------- | ----- |
| Retrieved Documents | array |

---

# Example Retrieval Response

```json id="jlwm164"
[
  {
    "pageContent": "AI workflow automation concepts",
    "metadata": {}
  }
]
```

---

# 6. FAISS Vector Store Reference

---

# Purpose

Stores semantic embeddings.

---

# Responsibilities

* vector indexing
* similarity search
* retrieval operations

---

# Configuration Example

```json id="jlwm165"
{
  "basePath": "./vectorstore/faiss",
  "topK": 4
}
```

---

# Inputs

| Input      | Type     |
| ---------- | -------- |
| Embeddings | vector[] |

---

# Outputs

| Output             | Type       |
| ------------------ | ---------- |
| Similarity Matches | document[] |

---

# 7. OpenAI Embeddings Reference

---

# Purpose

Generate semantic embeddings.

---

# Model

```plaintext id="jlwm166"
text-embedding-ada-002
```

---

# Inputs

| Input | Type   |
| ----- | ------ |
| Text  | string |

---

# Outputs

| Output           | Type    |
| ---------------- | ------- |
| Embedding Vector | float[] |

---

# 8. DOCX Loader Reference

---

# Purpose

Extract source document text.

---

# Supported Formats

```plaintext id="jlwm167"
.docx
```

---

# Outputs

| Output           | Type  |
| ---------------- | ----- |
| Document Objects | array |

---

# Example Output

```json id="jlwm168"
{
  "pageContent": "course material",
  "metadata": {}
}
```

---

# 9. Shared State Reference

---

# Purpose

Allow nodes to share execution context.

---

# State Includes

| State Field   | Purpose              |
| ------------- | -------------------- |
| messages      | conversation history |
| outputs       | prior agent outputs  |
| retrievedDocs | retrieval context    |
| metadata      | workflow metadata    |

---

# Example State Object

```json id="jlwm169"
{
  "messages": [],
  "outputs": {},
  "retrievedDocs": []
}
```

---

# Conversation History Modes

| Mode          | Purpose             |
| ------------- | ------------------- |
| all_messages  | Full history        |
| last_message  | Previous message    |
| user_question | Current query       |
| empty         | Stateless execution |

---

# 10. Edge Reference

---

# Purpose

Define workflow execution order.

---

# Example Edge

```json id="jlwm170"
{
  "source": "Search Agent",
  "target": "Writer Agent"
}
```

---

# Execution Flow

```plaintext id="jlwm171"
Search Agent
    ↓
Writer Agent
    ↓
Editor Agent
```

---

# Prompt Variable Injection

Variables are dynamically injected into prompts.

---

# Example

```json id="jlwm172"
{
  "promptValues": {
    "course": "{{question}}"
  }
}
```

---

# Recommended Output Formats

Preferred output types:

| Format     | Use Case               |
| ---------- | ---------------------- |
| Markdown   | Human-readable outputs |
| JSON       | Structured automation  |
| Plain Text | Lightweight workflows  |

---

# Error Handling Recommendations

Recommended future improvements:

* schema validation
* output validation
* retry logic
* fallback prompts
* structured error responses

---

# Future API Enhancements

Potential future additions:

| Enhancement         | Purpose                    |
| ------------------- | -------------------------- |
| REST API            | External integrations      |
| Webhooks            | Event-driven workflows     |
| Streaming Responses | Real-time generation       |
| JSON Schemas        | Structured outputs         |
| Agent SDK           | Programmatic orchestration |

---

# Recommended Developer Workflow

```plaintext id="jlwm173"
Update Workflow
      ↓
Validate JSON
      ↓
Test Retrieval
      ↓
Run Agents
      ↓
Evaluate Outputs
```

---

# Summary

This reference documents:

* workflow structure
* node interfaces
* retrieval contracts
* state management
* prompt variables
* execution sequencing

to support maintainable, scalable, and extensible multi-agent orchestration development.
