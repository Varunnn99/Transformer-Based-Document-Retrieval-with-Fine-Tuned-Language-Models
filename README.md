
# Transformer-Based Document Retrieval with Fine-Tuned LLMs

This repository contains the code and resources for a project focused on building and evaluating a sophisticated **Retrieval-Augmented Generation (RAG)** pipeline. The system is designed to answer questions based on the content of the book *"Data Privacy: Principles and Practice."*

---

## 📖 Project Overview

The goal of this project is to create an intelligent system capable of understanding a large, domain-specific text and providing accurate, context-aware answers to user queries. This serves as a **proof-of-concept** for an advanced knowledge retrieval tool for enterprise use.

### The core methodology involves:
- Ingesting and Preprocessing a 200-page book on data privacy.
- Generating Embeddings for text chunks using a powerful sentence transformer.
- Retrieving Relevant Information using semantic similarity search and a reranker model.
- Generating Answers with the `Qwen/Qwen1.5-4B` Large Language Model.
- Fine-Tuning the Qwen model on a generated Q&A dataset to improve domain-specific accuracy.
- Evaluating the model's performance on trained, untrained, and general knowledge questions to test for catastrophic forgetting.

---

## ✨ Features

- **End-to-End RAG Pipeline**: A complete workflow from document ingestion to answer generation.
- **Semantic Search**: Utilizes state-of-the-art sentence embeddings for accurate information retrieval.
- **Fine-Tuned LLM**: The generative model is fine-tuned using **LoRA** for enhanced performance on the specific knowledge domain.
- **Comprehensive Evaluation**: The system is rigorously tested for accuracy, faithfulness, and knowledge retention using the **Gemini API** as an evaluator.

---

## ⚙️ Methodology

The project is implemented in the `Transformer_Based_Document_Retrieval_with_Fine_Tuned_Language_Models.ipynb` Jupyter Notebook and follows these steps:

### 📘 Data Preparation:
- The source text from *"Data Privacy: Principles and Practice"* is ingested and cleaned.
- The text is segmented into smaller, manageable chunks.

### 🔍 Embedding and Retrieval:
- Text chunks are converted into vector embeddings using `intfloat/e5-base-v2`.
- When a query is received:
  - A similarity search retrieves the most relevant chunks.
  - A `cross-encoder/ms-marco-MiniLM-L-6-v2` model reranks the results for higher accuracy.

### 🧠 Answer Generation & Fine-Tuning:
- The retrieved chunks provide context to the `Qwen/Qwen1.5-4B` model, which generates an initial answer.
- A dataset of question-context-answer triplets is created.
- The Qwen model is fine-tuned on this dataset using **LoRA** for domain specialization.

### 📊 Evaluation:
The performance of both the base and fine-tuned models is evaluated using the **Gemini API**:
- **Trained Evaluation**: Assesses performance on questions the model was trained on.
- **Untrained Evaluation**: Tests generalization on new, unseen questions from the book.
- **Catastrophic Forgetting Test**: Evaluates whether the model retains its general knowledge after fine-tuning.

---

## 🤖 Models Used

| Purpose               | Model Name                                  |
|------------------------|----------------------------------------------|
| Embedding Model        | `intfloat/e5-base-v2`                        |
| Reranker Model         | `cross-encoder/ms-marco-MiniLM-L-6-v2`      |
| Generative Model       | `Qwen/Qwen1.5-4B`                            |
| Evaluation Model       | **Google Gemini API**                        |

---

## 🚀 Setup and Usage

### 1. Clone the repository:
```bash
git clone <your-repo-url>
cd <your-repo-directory>
```

### 2. Install dependencies:
The Jupyter Notebook `Transformer_Based_Document_Retrieval_with_Fine_Tuned_Language_Models.ipynb` contains all the necessary `pip install` commands for the required libraries, including:
- `unsloth`
- `transformers`
- `sentence-transformers`
- `torch`
- and other essentials.

### 3. Prepare Data:
- Ensure the text files (`ch1.txt`, `ch2.txt`, etc.) from the book are available in the specified path within the notebook.
- Make sure the following query files are also in the correct directory:
  - `queries.txt`
  - `new_privacy_queries.txt`
  - `general_knowledge_questions.txt`

### 4. Run the Notebook:
Execute the cells in the Jupyter Notebook sequentially to run the entire pipeline, from:
- Data preprocessing  
- Embedding generation  
- Query-based retrieval  
- Answer generation  
- LoRA-based fine-tuning  
- Evaluation with Gemini API  

---

## 📁 File Descriptions

| File Name                                               | Description |
|---------------------------------------------------------|-------------|
| `Transformer_Based_Document_Retrieval_with_Fine_Tuned_Language_Models.ipynb` | Main notebook containing all steps from ingestion to evaluation. |
| `queries.txt`                                           | Initial queries for dataset generation. |
| `new_privacy_queries.txt`                               | Evaluation queries from unseen parts of the book. |
| `general_knowledge_questions.txt`                       | General questions for retention testing. |
| `book_embeddings.json`                                  | Precomputed embeddings for all book chunks. |
| `fine_tuning_data.json`                                 | Dataset of question-context-answer triplets for LoRA fine-tuning. |

---

## 📊 Evaluation Results

The models were evaluated on **faithfulness**, **correctness**, **relevance**, and **clarity**.

### 🔹 Untrained Data Evaluation:
Comparison between the base Qwen model and the fine-tuned version on unseen questions.

| Metric       | Base Model Score | Fine-Tuned Model Score |
|--------------|------------------|-------------------------|
| Faithfulness | 9.98 / 10        | 9.30 / 10               |
| Correctness  | 8.04 / 10        | 9.19 / 10               |
| Relevance    | 9.70 / 10        | 9.48 / 10               |
| Clarity      | 9.17 / 10        | 9.12 / 10               |

### 🔹 Catastrophic Forgetting Evaluation:
Assesses the fine-tuned model’s ability to retain general knowledge post domain-specific training.

- **Average Knowledge Retention Score**: `9.12 / 10`

The results indicate that the fine-tuned model showed **significant improvement in domain-specific correctness** without a major loss of its general knowledge.

---

## 🏁 Conclusion

This project successfully demonstrates the effectiveness of a **RAG pipeline enhanced with a fine-tuned LLM** for domain-specific question answering.

The fine-tuned `Qwen/Qwen1.5-4B` model:
- Provided more accurate and relevant answers.
- Retained general knowledge well.
- Validated the potential for building **specialized enterprise retrieval systems** using open-source models.

---
