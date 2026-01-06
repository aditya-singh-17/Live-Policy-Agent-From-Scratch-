
# Live Policy Intelligence Agent

**Retrieval-Augmented Generation with Live Data Refresh**

## Overview
This project implements a **live, self-updating policy intelligence agent** that connects directly to authoritative public-health websites, detects content changes, refreshes its internal knowledge base, and answers user queries using retrieval-augmented generation (RAG).

Unlike static document-based systems, the agent ensures responses are always grounded in the **latest available policy information**.

---

## Problem Statement

Public health and government guidelines change frequently. Most applications rely on static documents or manual refresh cycles, leading to outdated or inconsistent information being served to hospitals, students, and the general public.


## Solution

We designed a deterministic agent pipeline that:

1. Fetches guideline content from a live authoritative source
2. Computes a content hash to detect changes
3. Refreshes embeddings only when changes occur
4. Retrieves relevant guideline sections for a query
5. Generates grounded responses using an LLM

This approach minimizes unnecessary recomputation while guaranteeing freshness and correctness.



## System Architecture

The agent follows an **Observe → Decide → Act → Respond** loop:

* **Observe**

  * Fetch live guideline content
  * Compute content hash for change detection

* **Decide**

  * Determine response mode based on detected changes and user query

* **Act**

  * Refresh knowledge base if content has changed
  * Retrieve relevant chunks using RAG

* **Respond**

  * Generate and format the final answer

All helper functions are orchestrated inside a single canonical agent function to maintain clarity and traceability.

---

## Key Design Decisions

* Hash-based change detection for efficient updates
* Rule-based decision logic (not LLM-driven)
* Retrieval only when required
* Single authoritative source to avoid conflicting policies

---

## Scope and Safety

This prototype intentionally focuses on WHO public-health guidelines to ensure accuracy, safety, and trust.
The architecture is **source-agnostic** and can be extended to other official policy sources.

The system does not provide medical diagnosis or treatment advice.

---

## Tech Stack

* Python
* Google Colab
* Retrieval-Augmented Generation (RAG)
* Large Language Model (LLM) API
* hashlib for content change detection

---

## Running the Demo

Open the notebook and run all cells sequentially.

To query the agent:

```python
ask_agent("What are the current isolation and quarantine guidelines?")
```

The agent will:

* Fetch the latest guideline content
* Detect updates automatically
* Retrieve relevant sections
* Generate a grounded response

---

## Future Extensions

* Support for multiple official sources (e.g., national health authorities)
* Region-specific policy comparisons
* Multilingual support
* Lightweight UI for non-technical users

---

## License

This project is intended for educational and research purposes.


