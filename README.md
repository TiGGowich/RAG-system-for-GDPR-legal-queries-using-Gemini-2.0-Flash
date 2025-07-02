# GDPR Legal Query Assistant: Retrieval-Augmented Generation (RAG) System

This project presents a Retrieval-Augmented Generation (RAG) system designed to answer complex legal queries within the context of the General Data Protection Regulation (GDPR). It integrates semantic chunking, hybrid retrieval (dense + sparse), and cross-encoder reranking to deliver grounded, traceable responses using Gemini 2.0 Flash as the Large Language Model (LLM).

🧑‍🎓 **This repository was developed as part of a university assignment for the MSc in Business Analytics at Warwick Business School.**

---

## 📌 Table of Contents

- [Project Overview](#-Project-Overview)
- [Problem Statement](#problem-statement)
- [Dataset](#dataset)
- [System Architecture](#system-architecture)
- [Key Design Decisions](#key-design-decisions)
- [Evaluation Methodology](#evaluation-methodology)
- [Results](#results)
- [Limitations & Future Work](#limitations--future-work)
- [Technologies Used](#technologies-used)
- [How to Run](#how-to-run)
- [Project Report](#project-report)
- [Contact](#contact)

---

## 🧠 Project Overview

While LLMs are powerful tools for natural language understanding and generation, they often struggle with providing accurate, auditable answers in domains requiring factual precision - like law. This project builds a RAG system for answering GDPR-related queries with grounded references, ensuring traceability and reducing hallucination.

---

## ❓ Problem Statement

How can we build a system that reliably answers GDPR legal queries using LLMs - while maintaining factual accuracy, grounding responses in documentation, and avoiding hallucinations?

---

## 📚 Dataset

The corpus combines three key GDPR sources:

- **UK GDPR Legislative Text** - Official regulatory wording
- **ICO Guidance** - Interpretations by the UK Information Commissioner’s Office
- **CNIL Handbook** - Operational guidance from France’s data protection authority

This multi-perspective corpus (legal, interpretative, operational) helps the system answer diverse question types effectively.

---

## 🏗️ System Architecture

[User Query] -> [Semantic Chunking] -> [Hybrid Retrieval: BM25 + Dense Embeddings] -> [Cross-Encoder Reranking] -> [LLM Generation (Gemini Flash 2.0)] -> [Grounded Legal Answer]

## ⚙️ Key Design Decisions

- **Semantic Chunking**: NLTK-based, maintains sentence integrity and token balance (~800 tokens)
- **Dense Embedding**: BAAI/bge-base-en, stored in ChromaDB vector store
- **Hybrid Retrieval**: Combines BM25 (keyword) and vector similarity for robust retrieval
- **Cross-Encoder Reranking**: BAAI/bge-reranker-large for contextual prioritization
- **LLM Prompting**: Gemini Flash 2.0 instructed to answer *only* using retrieved documents

---

## 📈 Evaluation Methodology

- 12 custom legal queries at 3 difficulty levels (easy, medium, hard)
- Graded by:
  - Relevance of retrieved context
  - Faithfulness of the answer to that context
  - Completeness of the response
- 0-5 score per criterion

---

## 🏆 Results

The Final Model outperformed all baselines, achieving a 56% improvement over the simplest configuration by combining semantic chunking, hybrid retrieval, BGE embeddings, and reranking.

Performance improved steadily across variants and remained strong even on harder queries. While relevance was consistently high, gains in faithfulness and completeness only became significant in the final setup.

One key failure case (Q2) revealed a core RAG limitation: the inability to answer questions when essential context is missing from the source corpus.

---

## 🚧 Limitations & Future Work

- Small corpus (~465 pages); not scalable without optimization
- Single-query mode only; no API or batch inference
- Struggled on abstract or philosophical queries (e.g., "purpose of GDPR")
- Future improvements:
  - Add confidence thresholds
  - Metadata-aware retrieval
  - Incorporate fallback to general-purpose knowledge base

---

## 🛠️ Technologies Used

- `Python Jupyter Notebooks / Colab`
- `ChromaDB`
- `BM25 (rank_bm25)`
- `BAAI/bge-base-en`, `bge-reranker-large`
- `Gemini Flash 2.0` via API
- `NLTK`
- `Langchain`, `Langchain-community`
- `pydf`

---

## 🚀 How to Run

Instructions on how to use and run the full code from the .ipynb are embedded within the Colab notebook. The only requirement for running the code is a Gemini API key which can be obtained for free within seconds.

---

## 📎 Project Report

Download the full PDF report [here](./RAG_assignment.pdf) for methodology, detailed examples, and references.

---

## 📫 Contact

Feel free to reach out on [LinkedIn](https://www.linkedin.com/in/benjamin-sachse-consultant) if you’d like to discuss this project or collaborate on similar work.
