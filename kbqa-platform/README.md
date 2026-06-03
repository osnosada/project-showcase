# Knowledge Base-Driven Personalized Intelligent Q&A Platform

A **RAG (Retrieval-Augmented Generation)** based web application that allows users to upload domain-specific documents and ask questions grounded in the uploaded content. The system combines vector semantic search with LLM-powered answer generation, knowledge graph visualization, and multi-turn dialogue.

**Live Demo:** [https://kbqa-system.onrender.com](https://kbqa-system.onrender.com)

> Note: The free-tier Render service may take ~30 seconds to wake up on first access.

---

## System Architecture

```
User Upload (.txt/.docx/.pdf)
        │
        ▼
  Document Processing ──→ Text Extraction & Chunking (300-char sliding window)
        │
        ▼
  Embedding Generation ──→ ZhipuAI Embedding-3 (1024-dim vectors)
        │
        ▼
  Vector Index Cache ──→ Pickle-based cache with cosine similarity search
        │
        ▼
┌───────────────────────────────────────────────┐
│              Flask REST API Backend            │
│  ┌─────────────┐  ┌─────────────┐  ┌───────┐ │
│  │  JWT Auth    │  │ Multi-turn  │  │ Active │ │
│  │  + RBAC      │  │ Dialogue    │  │Retrieve│ │
│  └─────────────┘  └─────────────┘  └───────┘ │
│  ┌─────────────────────────────────────────┐   │
│  │      Knowledge Graph (Dual Strategy)    │   │
│  │  Structure-based │ AI-based (GLM-4)     │   │
│  └─────────────────────────────────────────┘   │
└───────────────────────────────────────────────┘
        │                           │
        ▼                           ▼
  ZhipuAI GLM-4              ECharts Force-directed
  (Answer Generation)        (Graph Visualization)
```

---

## Key Features

| Feature | Description |
|---------|-------------|
| **Vector Knowledge Base** | Semantic search using ZhipuAI Embedding-3 with cosine similarity |
| **Multi-format Upload** | Support .txt, .docx, .pdf with GBK/UTF-8 encoding auto-detection |
| **Multi-turn Dialogue** | Per-user session history with context-aware follow-up questions |
| **Active Retrieval** | Keyword-triggered raw document retrieval without LLM generation |
| **Knowledge Graph** | Dual extraction strategies (structure-based & AI-driven) with ECharts visualization |
| **JWT Authentication** | Role-based access control (user/admin) with token-based auth |
| **Thread Safety** | RLock-protected knowledge base for concurrent access |
| **CI/CD Pipeline** | GitHub Actions with automated testing across Python 3.9/3.10/3.11 |
| **Cloud Deployment** | Deployed on Render with Gunicorn |

---

## Tech Stack

| Category | Technology |
|----------|-----------|
| **Backend** | Python Flask, Flask-CORS, Flask-JWT-Extended |
| **AI/LLM** | ZhipuAI GLM-4 (answer generation), Embedding-3 (vector embeddings) |
| **Search** | scikit-learn cosine similarity, pickle-based vector cache |
| **Frontend** | HTML/CSS/JavaScript, ECharts (graph visualization) |
| **Database** | SQLite (user management) |
| **Testing** | pytest, pytest-cov (6 test suites: unit, bug-discovery, regression, integration) |
| **CI/CD** | GitHub Actions |
| **Deployment** | Render, Gunicorn |

---

## My Contributions

As the **core architect**, I designed and implemented the entire project foundation:

- **Backend Architecture:** Flask REST API with all 14 endpoints, JWT authentication, role-based access control
- **VectorKnowledgeBase:** Document chunking, embedding generation, cosine similarity search, pickle-based caching
- **KnowledgeGraph:** Dual extraction strategies (structure-based heading parsing & AI-driven entity/relation extraction)
- **SimpleKnowledgeBase:** Keyword-based fallback search with GBK/UTF-8 encoding auto-detection
- **Multi-turn Dialogue:** Per-user session history management with context-aware responses
- **Active Retrieval Mode:** Keyword-triggered raw document retrieval
- **Testing Infrastructure:** 6 test suites (unit, bug-discovery, regression, integration), discovered and fixed 12 real bugs
- **CI/CD Pipeline:** GitHub Actions with multi-version Python testing
- **Cloud Deployment:** Render deployment with Gunicorn, lazy-loading for production
- **Documentation:** Complete README.md and final report

---

## Project Structure

```
├── app.py                  # Flask backend API (routes, auth, upload, Q&A)
├── vector_rag.py           # Core: VectorKnowledgeBase + KnowledgeGraph
├── basic_rag.py            # Fallback: SimpleKnowledgeBase (keyword search)
├── static/                 # Frontend HTML/CSS/JS pages
│   ├── index.html          # Chat interface
│   ├── login.html          # Login/registration page
│   ├── graph.html          # Knowledge graph visualization
│   └── admin.html          # Admin user management
├── data/                   # Sample documents
├── tests/                  # Test suite (6 files)
├── .github/workflows/      # CI/CD pipeline
├── requirements.txt        # Dependencies
├── Procfile                # Deployment config
└── render.yaml             # Render deployment config
```

---

## Team

| Member | Role |
|--------|------|
| **Li Yuanping** | Core architecture and base functionality |
| Cheng Yazheng | Feature development, bug fixes, testing |
| Chen Zhishen | Bug fixes, UI refinement, E2E testing |
| Cao Zhewei | Assistance and E2E testing |

---

*This project was developed for BSAI301 coursework at Macau University of Science and Technology.*
