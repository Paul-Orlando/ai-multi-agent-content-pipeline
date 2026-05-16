# Troubleshooting Guide

This document provides solutions for common issues encountered while running the AI Multi-Agent Content Pipeline.

The goal is to help developers quickly diagnose and resolve:

* workflow failures
* retrieval issues
* embedding problems
* agent execution errors
* deployment issues
* configuration mistakes

---

# Troubleshooting Workflow

Recommended debugging process:

```plaintext id="jlwm193"
Check Environment
      ↓
Validate Workflow
      ↓
Verify Retrieval
      ↓
Test Agents
      ↓
Inspect Logs
```

---

# 1. OpenAI API Errors

---

# Problem

```plaintext id="jlwm194"
Authentication Error
```

or

```plaintext id="jlwm195"
401 Unauthorized
```

---

# Cause

Invalid or missing OpenAI API key.

---

# Solution

Verify `.env` contains:

```env id="jlwm196"
OPENAI_API_KEY=
```

Ensure:

* the key is active
* the key has billing access
* there are no extra spaces
* the environment file is loaded

---

# Recommended Validation

```bash id="jlwm197"
echo $OPENAI_API_KEY
```

---

# 2. Embedding Generation Failures

---

# Problem

Embeddings are not generated.

---

# Possible Causes

| Cause                   | Description            |
| ----------------------- | ---------------------- |
| Missing API Key         | Authentication failure |
| Invalid Embedding Model | Unsupported model      |
| Rate Limits             | Too many requests      |
| Empty Documents         | No content to embed    |

---

# Solution

Verify:

```env id="jlwm198"
EMBEDDING_MODEL=text-embedding-ada-002
```

and ensure documents contain valid text.

---

# 3. Empty Retrieval Results

---

# Problem

Retriever returns no relevant content.

---

# Possible Causes

| Cause                | Description            |
| -------------------- | ---------------------- |
| Empty Vector Store   | No embeddings indexed  |
| Incorrect FAISS Path | Missing index          |
| Poor Chunking        | Weak retrieval quality |
| Irrelevant Query     | Semantic mismatch      |

---

# Solution Checklist

Verify:

* documents were embedded
* FAISS index exists
* vectorstore path is correct
* retrieval query is meaningful

---

# Recommended Validation

Check:

```plaintext id="jlwm199"
./vectorstore/faiss
```

exists and contains index data.

---

# 4. FAISS Errors

---

# Problem

```plaintext id="jlwm200"
FAISS index not found
```

or

```plaintext id="jlwm201"
Unable to load vector store
```

---

# Cause

Missing or corrupted vector index.

---

# Solution

Rebuild embeddings and regenerate the vector store.

---

# Recommended Steps

```plaintext id="jlwm202"
Delete Old Vector Store
      ↓
Reprocess Documents
      ↓
Generate Embeddings
      ↓
Rebuild FAISS Index
```

---

# 5. Flowise Import Failures

---

# Problem

Workflow JSON fails to import.

---

# Possible Causes

| Cause                | Description        |
| -------------------- | ------------------ |
| Invalid JSON         | Formatting issue   |
| Version Mismatch     | Unsupported nodes  |
| Missing Dependencies | Incompatible setup |

---

# Solution

Verify:

* JSON syntax is valid
* Flowise version compatibility
* required node packages installed

---

# Recommended Validation Tools

Use:

```plaintext id="jlwm203"
JSON validators
```

before importing workflows.

---

# 6. Agent Execution Failures

---

# Problem

Agents stop responding or fail unexpectedly.

---

# Possible Causes

| Cause                     | Description             |
| ------------------------- | ----------------------- |
| Invalid Prompt Variables  | Missing injected values |
| Missing Retrieval Context | Empty semantic results  |
| Model Limits              | Token overflow          |
| Timeout Errors            | Long-running execution  |

---

# Solution

Validate:

* prompt variables
* retrieval output
* token usage
* workflow sequencing

---

# Prompt Variable Validation

Example:

```json id="jlwm204"
{
  "course": "{{question}}"
}
```

Ensure variables are correctly injected.

---

# 7. Workflow Stops Mid-Execution

---

# Problem

Workflow execution halts unexpectedly.

---

# Possible Causes

| Cause                   | Description          |
| ----------------------- | -------------------- |
| Broken Node Connections | Invalid edges        |
| Missing State           | Shared state failure |
| Tool Execution Errors   | Retrieval issues     |

---

# Solution

Verify:

```plaintext id="jlwm205"
Start → Search → Writer → Editor → End
```

workflow chain remains intact.

---

# 8. Poor Retrieval Quality

---

# Problem

Retrieved context is irrelevant or weak.

---

# Possible Causes

| Cause           | Description               |
| --------------- | ------------------------- |
| Poor Chunking   | Weak semantic granularity |
| Small Dataset   | Limited context           |
| Weak Queries    | Ambiguous retrieval       |
| Metadata Issues | Incorrect indexing        |

---

# Recommended Improvements

| Improvement            | Benefit            |
| ---------------------- | ------------------ |
| Better Chunking        | Improved retrieval |
| Larger Context Windows | Better reasoning   |
| Metadata Filtering     | Cleaner retrieval  |
| Hybrid Search          | Better recall      |

---

# Recommended Chunk Settings

| Setting       | Recommendation  |
| ------------- | --------------- |
| Chunk Size    | 500–1000 tokens |
| Chunk Overlap | 100–200 tokens  |

---

# 9. Low-Quality Generated Outputs

---

# Problem

Generated content feels weak, repetitive, or generic.

---

# Possible Causes

| Cause                 | Description        |
| --------------------- | ------------------ |
| Weak Retrieval        | Poor grounding     |
| Prompt Ambiguity      | Vague instructions |
| Low Context Quality   | Sparse documents   |
| Excessive Compression | Missing detail     |

---

# Solution

Improve:

* prompt specificity
* retrieval quality
* source documents
* agent specialization

---

# 10. Prompt Injection Issues

---

# Problem

Users attempt to override system behavior.

---

# Example

```plaintext id="jlwm206"
Ignore previous instructions.
```

---

# Recommended Mitigations

| Mitigation        | Purpose         |
| ----------------- | --------------- |
| Prompt Isolation  | Preserve roles  |
| Output Validation | Safer responses |
| Human Approval    | Manual review   |
| Moderation Layers | Detect abuse    |

---

# 11. Docker Deployment Issues

---

# Problem

Container fails to start.

---

# Possible Causes

| Cause                         | Description          |
| ----------------------------- | -------------------- |
| Missing Environment Variables | Runtime failure      |
| Incorrect Volumes             | Missing vector store |
| Dependency Errors             | Build failures       |

---

# Solution

Verify:

```bash id="jlwm207"
docker compose logs
```

and confirm:

* `.env` exists
* volumes mount correctly
* ports are available

---

# 12. High Token Usage

---

# Problem

Unexpected API costs.

---

# Causes

| Cause                  | Description          |
| ---------------------- | -------------------- |
| Large Prompts          | Excessive context    |
| Large Retrieval Chunks | Bigger token windows |
| Long Outputs           | Verbose generation   |

---

# Optimization Recommendations

| Optimization       | Benefit                |
| ------------------ | ---------------------- |
| Prompt Compression | Lower token count      |
| Smaller Chunks     | Reduced retrieval size |
| Output Limits      | Controlled generation  |
| Model Selection    | Lower inference costs  |

---

# 13. Performance Issues

---

# Problem

Workflow execution is slow.

---

# Possible Causes

| Cause                | Description      |
| -------------------- | ---------------- |
| Large Embeddings     | Heavy processing |
| Sequential Agents    | Linear execution |
| External API Latency | Slow requests    |

---

# Recommended Improvements

* embedding caching
* async execution
* parallel agents
* retrieval optimization

---

# 14. Logging & Debugging Recommendations

---

# Recommended Debugging Areas

| Area              | Purpose             |
| ----------------- | ------------------- |
| Retrieval Outputs | Validate grounding  |
| Prompt Inputs     | Verify instructions |
| Agent Outputs     | Detect failures     |
| Token Usage       | Monitor cost        |

---

# Recommended Logging Strategy

Safe logs:

```plaintext id="jlwm208"
Workflow started
Retrieval completed
Agent execution successful
```

Avoid logging:

* API keys
* sensitive prompts
* confidential documents

---

# 15. Recovery Workflow

---

# Recommended Recovery Process

```plaintext id="jlwm209"
Identify Failure
      ↓
Validate Environment
      ↓
Test Retrieval
      ↓
Run Single Agent
      ↓
Re-run Full Workflow
```

---

# Recommended Diagnostic Order

1. Verify environment variables
2. Validate workflow JSON
3. Confirm embeddings exist
4. Test retrieval manually
5. Run agents independently
6. Review logs
7. Re-run orchestration

---

# Future Troubleshooting Improvements

Potential future additions:

| Improvement         | Benefit              |
| ------------------- | -------------------- |
| Automatic Retries   | Improved reliability |
| Health Checks       | Faster diagnostics   |
| Workflow Dashboards | Better observability |
| Agent Telemetry     | Execution tracing    |
| Retrieval Metrics   | Quality monitoring   |

---

# Summary

Most workflow issues originate from:

* environment misconfiguration
* retrieval failures
* invalid embeddings
* workflow connection errors
* prompt variable issues

A structured debugging workflow helps isolate failures quickly and maintain stable multi-agent orchestration.
