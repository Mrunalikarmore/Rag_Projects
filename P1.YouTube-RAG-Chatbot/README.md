# Project 01: YouTube RAG Chatbot

A beginner-friendly **Retrieval-Augmented Generation (RAG)** application that answers questions about YouTube videos using their available transcripts.
This project demonstrates how to combine transcript extraction, text chunking, embeddings, vector search, and an LLM to build a question-answering system using LangChain.

## 🎯 Project Objective

The goal is to enable users to ask questions about a YouTube video and receive answers grounded in the relevant transcript content, rather than relying only on the LLM's general knowledge.

## 🏗️ Architecture

1. **Transcript Extraction:** Fetch available captions using `youtube-transcript-api`.
2. **Text Chunking:** Split the transcript into smaller, overlapping chunks using `RecursiveCharacterTextSplitter`.
3. **Embeddings:** Convert text chunks into numerical vectors using Hugging Face Sentence Transformers.
4. **Vector Storage:** Index the embeddings using FAISS.
5. **Retrieval:** Retrieve relevant transcript chunks for a user's question.
6. **Prompt Construction:** Combine the retrieved context and question using a LangChain prompt template.
7. **LLM Generation:** Generate an answer using a chat model accessed through Groq.
8. **Output Parsing:** Use `StrOutputParser` to return the final response as plain text.

## 🛠️ Tech Stack

- **Language:** Python
- **Development Environment:** Google Colab
- **Orchestration:** LangChain
- **Transcript Extraction:** YouTube Transcript API
- **Text Embeddings:** Hugging Face Sentence Transformers (`all-MiniLM-L6-v2`)
- **Vector Store:** FAISS
- **LLM Provider:** Groq API
- **Output Parsing:** LangChain `StrOutputParser`

## 🔄 RAG Pipeline

`YouTube Transcript → Text Chunks → Embeddings → FAISS → Retriever → Prompt Template → LLM → Answer`

## ✨ Key Features

- Extracts available English captions from a YouTube video.
- Splits lengthy transcripts into manageable text chunks.
- Retrieves relevant context using vector similarity search.
- Uses retrieved transcript content to guide LLM responses.
- Supports multiple questions about the same indexed video.
- Demonstrates LangChain runnables and the LangChain Expression Language (LCEL).

## 📂 Project Files

```text
01-youtube-rag-chatbot/
├── README.md
├── youtube_rag_chatbot.ipynb
└── screenshots&requirements
```

## ⚙️ Installation and Setup

### 1. Install dependencies

```bash
pip install youtube-transcript-api langchain-community langchain-groq langchain-huggingface langchain-core langchain-text-splitters sentence-transformers faiss-cpu
```

### 2. Configure the API key

Create a Groq API key and store it securely in Google Colab Secrets using the name `GROQ_API_KEY`.

Never upload API keys or other secrets to GitHub.

### 3. Open the notebook

Open `youtube_rag_chatbot.ipynb` in Google Colab and execute the cells in order.

### 4. Select a YouTube video

Provide a video ID with accessible captions in a supported language. The current implementation requests English captions.

### 5. Ask questions

Run the RAG chain with a question:

```python
answer = main_chain.invoke(
    "Can you summarize the main points of the video?"
)
print(answer)
```

## 🧠 Key Concepts Learned

- Retrieval-Augmented Generation (RAG)
- Text chunking and overlap
- Semantic embeddings
- Vector similarity search
- FAISS and retrievers
- Prompt templates
- LangChain runnables and LCEL
- `RunnableParallel`
- `RunnablePassthrough`
- `RunnableLambda`
- `StrOutputParser`
- Connecting an LLM through an API

## ⚠️ Limitations

- Requires accessible captions or transcripts.
- Currently requests English captions only.
- Answer quality depends on transcript quality and the relevance of retrieved chunks.
- LLM responses may still contain inaccuracies.
- The vector index is created in the current notebook runtime and is not automatically persisted between sessions.

## 🔮 Future Improvements

- Add memory to remember the privious chat.
- Evaluate retrieval quality and answer accuracy.
- Add robust error handling for unavailable transcripts and API errors.

## 📚 Learning Outcome

This project helped me understand how the individual components of a RAG system work together, from extracting source information and retrieving relevant context to generating a grounded response using an LLM.
It serves as my first foundational project in my journey towards building more advanced Generative AI and RAG applications.
