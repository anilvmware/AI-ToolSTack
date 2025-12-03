# 🚀 AI-Powered Web Application Starter

A modern, production-grade starter template for building **AI-powered web applications** using **Next.js**, **FastAPI/Node**, **Supabase**, and **LLM integrations (OpenAI, Claude, Llama)**.

This template focuses on **rapid development**, clean architecture, scalable APIs, and end-to-end AI features such as RAG, embeddings, and agent workflows.

---

## ✨ Features

- ⚡ **Next.js 15 frontend** with ShadCN UI
- 🟦 **Supabase Auth + Postgres**
- 📦 **REST API (FastAPI or Node.js)** for backend logic
- 🤖 **AI Integration** with OpenAI, Anthropic, and Llama models
- 📚 **RAG Pipeline** (Embeddings, Vector Search, Context Builder)
- ☁️ **Edge functions** for low-latency processing (Vercel/Cloudflare)
- 🗂️ **Opinionated folder structure** for scale
- 🧪 **AI-generated test scaffolding**
- 🔐 **Environment variable management**
- 🚀 **One-click deployment** to Vercel & Supabase

---

## 🏗️ Architecture

```mermaid
flowchart TD

    subgraph Client["Frontend (Next.js)"]
        UI["React UI<br/>ShadCN Components"]
        AuthClient["Auth Client (Clerk / Supabase Auth)"]
        APIClient["API Calls / React Query"]
    end

    subgraph Edge["Edge Layer (Vercel / Cloudflare Workers)"]
        EdgeRouter["Edge Router"]
        EdgeFunctions["Edge Functions<br/>Middleware / Pre-processing"]
    end

    subgraph Backend["Backend API (FastAPI / Node.js)"]
        APIRouter["REST / GraphQL Routes"]
        BusinessLogic["Service Layer / Use Cases"]
        RAG["RAG Pipeline<br/>Embedding, Retrieval, Re-ranking"]
    end

    subgraph DB["Storage Layer"]
        SQLDB["Supabase Postgres"]
        VectorDB["Vector Store (Supabase Vector / Pinecone)"]
        FileStore["Object Storage<br/>(Supabase Storage / S3)"]
    end

    subgraph AI["AI Providers"]
        OpenAI["OpenAI GPT-5 / Embeddings"]
        Anthropic["Claude"]
        Groq["Groq Llama 3.2"]
    end

    UI --> APIClient --> EdgeRouter --> EdgeFunctions --> APIRouter
    APIRouter --> BusinessLogic
    BusinessLogic --> SQLDB
    BusinessLogic --> FileStore
    BusinessLogic --> VectorDB
    BusinessLogic --> RAG --> VectorDB

    RAG --> OpenAI
    RAG --> Anthropic
    RAG --> Groq
