# Transformer-Based Document Retrieval with Fine-Tuned LLMs

This repository contains the code and resources for building and evaluating a sophisticated **Retrieval-Augmented Generation (RAG)** pipeline. The system answers questions based on the book *"Data Privacy: Principles and Practice."*

---

## 📖 Project Overview

The goal of this project is to create an intelligent system that can:
- Understand a large domain-specific text.
- Provide accurate, context-aware answers to user queries.

This serves as a **proof-of-concept** for an advanced enterprise-grade knowledge retrieval system.

### Core Methodology:
- Ingest and preprocess a 200-page book on data privacy.
- Generate embeddings for text chunks using a sentence transformer.
- Retrieve relevant information via semantic search and a reranker.
- Generate answers using a fine-tuned Qwen Large Language Model.
- Evaluate for both domain accuracy and general knowledge retention.

---

## ✨ Features

- **End-to-End RAG Pipeline**: From ingestion to answer generation.
- **Semantic Search**: Uses state-of-the-art sentence embeddings.
- **Fine-Tuned LLM**: Qwen model fine-tuned with LoRA for domain specialization.
- **Comprehensive Evaluation**: Tested using Gemini API for accuracy, relevance, and retention.

---

## ⚙️ Methodology

Implemented in `Transformer_Based_Document_Retrieval_with_Fine_Tuned_Language_Models.ipynb`, the pipeline follows these steps:

### 1. **Data Preparation**
- Ingest and clean text from *Data Privacy: Principles and Practice*.
- Segment the book into manageable chunks.

### 2. **Embedding & Retrieval**
- Convert chunks into embeddings using `intfloat/e5-base-v2`.
- On receiving a query:
  - Retrieve top matches using semantic similarity.
  - Rerank using `cross-encoder/ms-marco-MiniLM-L-6-v2`.

### 3. **Answer Generation & Fine-Tuning**
- Feed relevant chunks as context to `Qwen/Qwen1.5-4B` to generate initial answers.
- Generate a fine-tuning dataset with question-context-answer triplets.
- Fine-tune the Qwen model using LoRA for domain accuracy.

### 4. **Evaluation**
- **Trained Evaluation**: On known questions.
- **Untrained Evaluation**: On unseen queries from the same domain.
- **Catastrophic Forgetting Test**: On general knowledge questions to check knowledge retention.

---

## 🤖 Models Used

| Purpose             | Model Name                                      |
|---------------------|--------------------------------------------------|
| **Embedding**        | `intfloat/e5-base-v2`                           |
| **Reranker**         | `cross-encoder/ms-marco-MiniLM-L-6-v2`         |
| **Generative**       | `Qwen/Qwen1.5-4B`                               |
| **Evaluator**        | Google Gemini API                              |

---

## 🚀 Setup and Usage

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd <your-repo-directory>
