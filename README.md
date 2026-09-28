# Knowledge Base Retrieval System (RAG)

A full Retrieval-Augmented Generation pipeline — chunk documents, embed them, store them in a vector DB, retrieve the most relevant pieces, and generate a grounded answer.

## Problem Statement

Enterprises have huge volumes of internal documentation that's hard to search with plain keywords. RAG fixes this — it retrieves the most relevant chunks first, then feeds them to an LLM so the answer is actually grounded in real documents instead of the model guessing. This project builds a complete RAG pipeline end to end using free tools.

## Dataset

[Wikipedia (Simple English)](https://huggingface.co/datasets/wikimedia/wikipedia) — 3,000 articles sampled from 241,787 available, used as a free stand-in for internal enterprise documents. Same chunk/embed/retrieve pipeline applies directly to real company wikis, policies, or runbooks.

## What It Builds

- A document chunking pipeline (overlapping 300-word chunks)
- A ChromaDB vector store indexing every chunk's embedding (MPNet)
- A hybrid retrieval function combining dense (embedding) search with BM25 keyword search
- A working RAG answer-generation function grounded in retrieved context, powered by Groq's free API

## Results (from an actual run)

| Metric | Value |
|---|---|
| Corpus size | 3,000 documents → 4,040 chunks |
| Retrieval precision@5 (small sample) | 0.20 |
| Sample query | *"What is the capital of France?"* → **"Paris."** (correct, grounded in retrieved context) |

**Honest note on the precision number:** 0.20 is based on just 2 test queries and a strict "exact title match" scoring rule — several retrieved chunks were topically relevant but from articles with a different exact title, which the strict test doesn't credit. The retrieval and generation pipeline itself works correctly end to end; a larger, better-designed eval set would likely show a stronger number, and expanding it is a natural next step for this project.

## Tech Stack

Python · ChromaDB · Sentence-Transformers · Groq API (free tier) · Google Colab

## How to Run

1. Open the notebook in Google Colab
2. Run all cells top to bottom
3. Enter a free [Groq API key](https://console.groq.com/keys) when prompted

## Repo Structure

```
rag-knowledge-base/
├── Knowledge_Base_Retrieval_System.ipynb
└── README.md
```

## Disclaimer

Built as a learning/portfolio project using Wikipedia as a stand-in corpus. Retrieval precision numbers here are from a small demo query set, not a rigorous benchmark.

---
By Akshat Kesharwani
