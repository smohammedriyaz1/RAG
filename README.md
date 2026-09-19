# 🚀 Retrieval-Augmented Generation (RAG)

A **Retrieval-Augmented Generation (RAG)** application that combines document retrieval, vector embeddings, ChromaDB, and Large Language Models to generate context-aware answers from user-provided documents.

## 📌 Project Overview

This project implements an end-to-end RAG pipeline:

```text
Documents
    ↓
Text Extraction
    ↓
Text Chunking
    ↓
Embeddings
    ↓
ChromaDB Vector Store
    ↓
Semantic Retrieval
    ↓
Relevant Context
    ↓
OpenAI / Groq LLM
    ↓
Generated Answer
```

The system retrieves relevant information from the stored documents and provides it as context to the LLM before generating an answer.

---

## ✨ Features

* 📄 Document processing
* ✂️ Text chunking with overlap
* 🔢 384-dimensional embeddings
* 🗄️ ChromaDB vector database
* 🔍 Semantic similarity search
* 📑 Top-K document retrieval
* 🤖 Retrieval-Augmented Generation
* 🧠 OpenAI LLM integration
* ⚡ Groq LLM integration
* 🔐 Secure API-key handling with Google Colab Secrets

---

## 🛠️ Tech Stack

| Technology            | Usage                   |
| --------------------- | ----------------------- |
| Python                | Core development        |
| Google Colab          | Development environment |
| Sentence Transformers | Embeddings              |
| all-MiniLM-L6-v2      | Embedding model         |
| ChromaDB              | Vector database         |
| LangChain             | LLM integration         |
| OpenAI                | LLM                     |
| Groq                  | LLM inference           |
| NumPy                 | Data processing         |
| Pandas                | Data processing         |

---

## 🧠 Embedding Model

The project uses:

```text
all-MiniLM-L6-v2
```

The model converts text into **384-dimensional vectors**.

Example:

```text
"What is RAG?"
       ↓
Embedding Model
       ↓
(1, 384)
```

These vectors are stored in ChromaDB and used for semantic similarity search.

---

## 🔎 Document Retrieval

For every user query:

1. The query is converted into an embedding.
2. ChromaDB searches for similar document vectors.
3. The most relevant documents are retrieved.
4. Retrieved content is passed to the LLM as context.
5. The LLM generates the final response.

Example:

```python
results = retriever.retrieve(query, top_k=3)
```

---

## 🤖 LLM Support

The project supports both **Groq** and **OpenAI**.

### Groq

```python
from langchain_groq import ChatGroq

llm = ChatGroq(
    model="openai/gpt-oss-20b",
    temperature=0,
    api_key=groq_api_key
)
```

### OpenAI

```python
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(
    model="gpt-4o-mini",
    temperature=0,
    api_key=openai_api_key
)
```

---

## 🔐 API Key Security

API keys are **not stored in this repository**.

For Google Colab, use Colab Secrets:

```python
from google.colab import userdata

groq_api_key = userdata.get("GROQ_API_KEY")
openai_api_key = userdata.get("OPENAI_API_KEY")
```

Never upload actual API keys to GitHub.

---

## 💻 RAG Generation

```python
def generate_output(query, retriever, llm, top_k=3):

    results = retriever.retrieve(query, top_k)

    context = "\n".join(
        [doc["document"] for doc in results]
    ) if results else ""

    if not context:
        return "No relevant context found."

    prompt = f"""
    Answer the question using only the provided context.

    If the answer is not present in the context,
    say "I don't know based on the provided context."

    Context:
    {context}

    Question:
    {query}

    Answer:
    """

    response = llm.invoke(prompt)

    return response.content
```

---

## ▶️ Example

### Query

```text
What is RAG?
```

### Pipeline

```text
Query
 ↓
Embedding
 ↓
ChromaDB
 ↓
Relevant Documents
 ↓
Context
 ↓
LLM
 ↓
Answer
```

### Example

```text
RAG stands for Retrieval-Augmented Generation.
It combines information retrieval with a language
model to generate answers using relevant external
information.
```

---

## 📁 Project Structure

```text
RAG/
│
├── RAG_Project.ipynb
├── README.md
├── requirements.txt
├── data/
└── vector_store/
```

---

## 📚 Key Concepts Demonstrated

* Retrieval-Augmented Generation
* LLMs
* Embeddings
* Vector databases
* ChromaDB
* Semantic search
* Document chunking
* Top-K retrieval
* Prompt engineering
* OpenAI API
* Groq API
* LangChain
* API-key security

---

## 🔮 Future Improvements

* Streamlit interface
* PDF/DOCX/TXT support
* Conversation memory
* Source citations
* Hybrid search
* Reranking
* RAG evaluation
* Cloud deployment

---

## 👨‍💻 Author

**Shaik Mohammed Riyaz**

AI/ML | Generative AI | RAG | LLMs | Full-Stack Development

GitHub: [smohammedriyaz1](https://github.com/smohammedriyaz1)

---

⭐ If you find this project useful, consider starring the repository.
