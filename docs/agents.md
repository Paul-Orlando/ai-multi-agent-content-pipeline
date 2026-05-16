# Agents Documentation

The AI Multi-Agent Content Pipeline uses specialized sequential agents to transform source materials into polished marketing content.

Each agent has a narrowly scoped responsibility to improve modularity, maintainability, and output quality.

---

# Agent Pipeline Overview

```plaintext id="3vk8c1"
Search Agent
    ↓
Writer Agent
    ↓
Editor Agent
```

Each agent consumes the output of the previous agent.

---

# Why Multi-Agent Architecture

Instead of relying on a single prompt, the system divides work into specialized stages.

This approach improves:

* reasoning quality
* output consistency
* prompt control
* debugging
* scalability
* maintainability

---

# Agent Design Philosophy

Each agent follows:

| Principle             | Purpose                      |
| --------------------- | ---------------------------- |
| Specialization        | One responsibility per agent |
| Sequential Processing | Structured refinement        |
| Prompt Isolation      | Reduced prompt conflicts     |
| Modular Outputs       | Easier orchestration         |
| Context Grounding     | Better factual consistency   |

---

# 1. Search Agent

---

# Purpose

The Search Agent is responsible for researching and analyzing course content retrieved from the vector database.

It acts as the system’s knowledge extraction and reasoning layer.

---

# Responsibilities

The Search Agent:

* retrieves relevant course information
* identifies major topics
* expands on subject areas
* analyzes learning objectives
* identifies audience fit
* structures research insights

---

# System Prompt

```plaintext id="o13hgt"
You are a search agent that will look for all the possible information related to the course {course}.

### TASKS ###
1. Gather all the information including topics about the course.
2. Expand on each topic.
3. Help to figure out a specific target audience based on the course content.

### EXPECTED OUTPUT ###
The detailed information related to the course and the suggested target audience.
```

---

# Inputs

| Input                | Source                |
| -------------------- | --------------------- |
| User Query           | Workflow input        |
| Retrieved Documents  | Retriever Tool        |
| Conversation History | Shared workflow state |

---

# Tools Used

| Tool           | Purpose                     |
| -------------- | --------------------------- |
| Retriever Tool | Semantic document retrieval |

---

# Output

The Search Agent produces:

* expanded course summaries
* topic breakdowns
* audience recommendations
* structured research insights

---

# Architectural Role

```plaintext id="e2bw1v"
Reasoning Layer
```

---

# Design Pattern

Implements:

# Retrieval-Augmented Reasoning

The agent reasons over retrieved documents rather than relying entirely on model memory.

---

# Example Output

```markdown id="9j7j3m"
Course Topics:
- AI Product Strategy
- Prompt Engineering
- AI Workflow Automation

Target Audience:
- Product Managers
- Technical Marketers
- AI Consultants
```

---

# 2. Writer Agent

---

# Purpose

The Writer Agent transforms structured research into engaging marketing content.

It serves as the content generation layer.

---

# Responsibilities

The Writer Agent:

* creates promotional copy
* structures social content
* generates engagement hooks
* adds CTAs
* improves readability
* maintains marketing tone

---

# System Prompt

```plaintext id="h5o6lw"
You are a technical marketing manager whose goal is to write marketing copies.

### TASKS ###
1. Use the detailed course content to write a tweet that announces the course.
2. Ensure that the tweet is 4 blocks, easy to read, and shows excitement.
3. Include a clear call to action to enroll in the course.
4. Proofread for grammatical errors.

### EXPECTED OUTPUT ###
A well-written tweet in markdown format, ready to be published.
```

---

# Inputs

| Input                    | Source       |
| ------------------------ | ------------ |
| Research Insights        | Search Agent |
| Topic Expansions         | Search Agent |
| Audience Recommendations | Search Agent |

---

# Output

The Writer Agent produces:

* promotional tweets
* announcements
* marketing copy
* CTA-driven content

---

# Architectural Role

```plaintext id="8q4uk0"
Generation Layer
```

---

# Design Goals

The Writer Agent is optimized for:

* engagement
* clarity
* readability
* excitement
* concise messaging

---

# Example Output

```markdown id="b0o8hf"
Master AI Product Strategy with our latest course.

Learn real-world frameworks, prompt engineering, and workflow automation techniques used by modern AI teams.

Designed for product leaders, marketers, and builders ready to level up.

Enroll today and start building AI-driven products with confidence.
```

---

# 3. Editor Agent

---

# Purpose

The Editor Agent refines generated content to ensure publication readiness.

It acts as the system’s quality assurance layer.

---

# Responsibilities

The Editor Agent:

* fixes grammar
* shortens verbose text
* removes unnecessary details
* improves clarity
* improves conciseness
* standardizes tone

---

# System Prompt

```plaintext id="7jlwmr"
You are an editor whose goal is to edit a given tweet to ensure it is grammatically correct and concise.

### EXPECTED OUTPUT ###
The output is a tweet in markdown format that is ready for publication. Avoid hashtags, emojis, and noisy details.
```

---

# Inputs

| Input           | Source       |
| --------------- | ------------ |
| Marketing Draft | Writer Agent |

---

# Output

The Editor Agent produces:

* publication-ready content
* polished messaging
* concise copy
* refined social posts

---

# Architectural Role

```plaintext id="8q0tf8"
Refinement Layer
```

---

# Design Goals

The Editor Agent is optimized for:

* clarity
* brevity
* readability
* professionalism
* consistency

---

# Example Output

```markdown id="3gmjlwm"
Learn AI Product Strategy with practical frameworks, prompt engineering techniques, and workflow automation skills designed for modern product teams.

Enroll today and start building AI-driven products with confidence.
```

---

# Agent Dependencies

The system uses strict sequential dependencies.

---

# Dependency Chain

```plaintext id="nztf9u"
Search Agent
    ↓
Writer Agent
    ↓
Editor Agent
```

---

# Dependency Rules

| Agent        | Depends On     |
| ------------ | -------------- |
| Search Agent | Retriever Tool |
| Writer Agent | Search Agent   |
| Editor Agent | Writer Agent   |

---

# Shared Workflow Context

Agents can access:

* conversation history
* prior outputs
* workflow state
* retrieved documents

---

# Prompt Engineering Strategy

The pipeline uses prompt specialization to improve reliability.

---

# Benefits

| Benefit                | Explanation           |
| ---------------------- | --------------------- |
| Reduced Hallucinations | Retrieval grounding   |
| Better Outputs         | Specialized prompts   |
| Easier Debugging       | Modular stages        |
| Reusability            | Independent agents    |
| Scalability            | Add new agents easily |

---

# Sequential Refinement Pattern

The pipeline implements:

```plaintext id="r05cye"
Research
    ↓
Generate
    ↓
Refine
```

This multi-pass architecture improves final content quality significantly compared to single-prompt generation.

---

# Future Agent Enhancements

Potential future agents:

| Agent             | Purpose                     |
| ----------------- | --------------------------- |
| SEO Agent         | Optimize search visibility  |
| Compliance Agent  | Brand/legal validation      |
| LinkedIn Agent    | Long-form social generation |
| Analytics Agent   | Engagement optimization     |
| Translation Agent | Multi-language support      |
| Approval Agent    | Human-in-the-loop review    |

---

# Summary

The multi-agent architecture separates responsibilities across:

* research
* content generation
* editorial refinement

to create a scalable, maintainable, and high-quality AI content generation workflow.
