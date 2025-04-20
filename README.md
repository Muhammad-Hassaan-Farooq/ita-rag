# 🔍 RAG Project: Sherlock Holmes QA

This project implements a **Retrieval-Augmented Generation (RAG)** pipeline to answer natural language questions based on a custom document collection. It demonstrates how external knowledge can be integrated with a large language model to enhance its ability to answer factual questions.

---

## 📌 Project Overview

**Goal:**  
Answer questions about Sherlock Holmes stories using retrieved context from documents.

**Example Question:**  
> _"Who is Sherlock Holmes?"_

---

## 🧠 Model Details

- **Language Model:** `google/flan-t5-xxl`
  - **Size:** 3 billion parameters
  - **Type:** Instruction-tuned encoder-decoder LLM
  - **Use:** Generates answers based on the question + retrieved context.

---

## 📚 Retrieval Pipeline

### 1. **Document Preprocessing**
Documents were first loaded and cleaned for semantic chunking.

### 2. **Chunking Strategy**

```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,
    chunk_overlap=100
)
texts = text_splitter.split_documents(documents)
```

- **Chunk Size:** 500 characters  
- **Overlap:** 100 characters  
- **Why?** This balance ensures each chunk maintains enough context while allowing for continuity across splits.

### 3. **Retriever**
A vector-based retriever was used to index and fetch relevant document chunks based on semantic similarity to the question.

---

## 🧪 Workflow

1. **User Input:** A natural language question is provided.
2. **Retriever:** The top-k most relevant chunks are retrieved from the document index.
3. **LLM Generation:** The model (`flan-t5-xxl`) uses the retrieved context and question to generate a response.

---

## 💬 Example Run

**Question:**  
`"Who is Sherlock Holmes?"`

**Retrieved Context:**  
> [Relevant passages about Sherlock Holmes from the dataset]

**Generated Answer:**  
> _"Sherlock Holmes is a fictional detective known for his logical reasoning and keen observation skills. He often works with Dr. John Watson and resides at 221B Baker Street."_

---

## 🛠️ Technologies Used

- Python
- Hugging Face Transformers
- LangChain / custom retrieval logic
- FAISS / similar vector search backend
- Google `flan-t5-xxl` LLM

---

## 🚀 Future Improvements

- Integrate multi-hop retrieval
- Fine-tune or prompt-tune the LLM for domain-specific tasks
- Add UI or API endpoints for interactive querying
