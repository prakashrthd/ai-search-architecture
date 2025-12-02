# AI Search Architecture

> AI-enabled knowledge search platform built with **.NET 8 microservices**, **Azure**, and **modern AI (RAG / embeddings)**.  

---

## 🎯 Problem This Solves

Modern teams have documents, SOPs, and knowledge spread across systems.  
This project aims to provide an **AI-powered search service** where a user can:

- Ask questions in **natural language**
- Relevant context is retrieved from indexed documents
- An **AI model (Azure OpenAI / OpenAI)** generates an answer grounded in those documents

---

## 🧱 High-Level Architecture

```mermaid
flowchart LR
    User["User / Frontend (Web or Mobile)"] -->|HTTPS| APIGw["API Gateway (.NET 8)"]
    APIGw -->|JWT or B2C Token| AuthSvc["Auth Service"]
    APIGw --> ContentSvc["Content Service"]
    APIGw --> AISvc["AI Service"]

    ContentSvc --> DB["SQL / PostgreSQL"]
    AISvc --> VectorStore["Vector DB / Azure AI Search"]
    AISvc --> LLM["Azure OpenAI / OpenAI"]

    subgraph Observability
        Logs["Structured Logs"]
        Metrics["Metrics / Traces"]
    end

    APIGw --> Logs
    AISvc --> Logs
    ContentSvc --> Logs

