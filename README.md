# Notes QA Agent (LangChain + LangSmith) 🧠📓

A lightweight Markdown notes reader you can run in a Jupyter notebook. It ingests notes from a local ./notes folder, builds a vector index (FAISS), and lets you ask questions with source-cited answers. Tracing and observability are powered by LangSmith.

---

# ✨ Features

Drop-in notes folder: put .md, .txt, .pdf, or .docx files in ./notes

RAG pipeline: chunk → embed → retrieve → answer with citations

Local vector store: FAISS (fast, serverless)

LangSmith tracing: see prompts, retrieved context, token usage, latencies

Notebook-first: designed for Jupyter; minimal dependencies

Extensible: swap models, tune chunking, add UI later (Gradio/Streamlit)

---

# Architecture

            ┌─────────────────────┐
            │   Notes (./notes)   │  ← .md, .txt, .pdf, .docx
            └─────────┬───────────┘
                      │ Load & Split (RecursiveCharacterTextSplitter)
                      ▼
                ┌─────────────┐
                │   Chunks    │
                └─────┬───────┘
                      │ Embed (OpenAIEmbeddings)
                      ▼
                ┌─────────────┐
                │   FAISS     │  ← persistent local vector index (optional)
                └─────┬───────┘
                      │ Retrieve top-k
                      ▼
               ┌────────────────┐
               │   RAG Prompt   │  ← formatted context + question
               └──────┬─────────┘
                      │ LLM (ChatOpenAI)
                      ▼
             ┌────────────────────┐
             │ Answer + Citations │
             └────────────────────┘

Observability: LangSmith (tracing, tags, metadata)


```bash
.
├─ notes/                # place your notes here (you create this)
├─ .env                  # environment variables (see below)
├─ notebook.ipynb        # optional: your Jupyter workflow
├─ README.md             # this file
└─ (optional) artifacts/ # saved FAISS index (if you persist)

```
