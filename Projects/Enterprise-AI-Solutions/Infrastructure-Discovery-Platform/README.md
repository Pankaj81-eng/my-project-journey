# VMware Migration Assistant

## Business Problem

A major UK financial institution had thousands of infrastructure components — servers, services, databases, APIs — spread across on-premise and cloud environments with no reliable, up-to-date map of how they connected. Manual discovery was slow, error-prone, and produced static documentation that became stale within weeks. Teams had no way to answer questions like "what depends on this service?" or "what will break if we retire this host?"

## Solution Overview

An AI-powered infrastructure discovery platform that automatically ingests configuration data, builds a live Knowledge Graph of all components and their relationships, and exposes a natural language query interface backed by GraphRAG. Engineers can ask questions in plain English and receive context-aware answers drawn from the graph rather than flat documents.

## Architecture

```
Data Ingestion Layer
    ↓
Neo4j Knowledge Graph  ←→  Vector Embedding Store
    ↓
GraphRAG Retrieval Engine
    ↓
FastAPI Backend
    ↓
React Frontend (Query UI + Graph Visualisation)
```

1. **Ingestion** — configuration exports, CMDB data, and API responses are parsed and loaded into Neo4j as typed nodes (Server, Service, Database, API, Network) with labelled relationships.
2. **Knowledge Graph** — Cypher schemas model dependency chains. Relationships like `DEPENDS_ON`, `HOSTS`, `CALLS`, and `CONNECTS_TO` make impact analysis traversable.
3. **GraphRAG** — queries first retrieve the relevant graph subgraph, then pass it alongside vector-matched documents to an LLM for grounded, explainable answers.
4. **API** — FastAPI exposes endpoints for natural language queries, graph traversal, and impact analysis.
5. **UI** — React frontend with an interactive graph visualiser and a chat-style query panel.

## Technologies Used

- Neo4j (graph database)
- Cypher (query language)
- LangChain (GraphRAG orchestration)
- FastAPI (backend API)
- React + Vite (frontend)
- OpenAI (Azure deployment, LLM backbone)
- FAISS (vector similarity search)
- Python

## AI Concepts Demonstrated

- Knowledge Graph Design
- GraphRAG (graph-augmented retrieval)
- Cypher Query Generation from natural language
- Infrastructure Discovery and Dependency Analysis
- Retrieval-Augmented Generation (RAG)

## Key Learnings

- Graph schema design is the hardest part — getting the node types and relationship labels right determines whether the retrieval is useful.
- GraphRAG produces noticeably more accurate answers than flat RAG for relationship questions because the graph encodes structure that embeddings lose.
- Cypher generation via LLM requires careful prompt engineering and schema injection to stay within safe query patterns.
- Impact analysis (what breaks if X changes?) is a natural graph traversal — no ML needed, just well-designed relationships.

## Future Enhancements

- Real-time ingestion via event-driven connectors (Kafka, webhooks)
- Automated drift detection — alert when the live environment diverges from the graph
- Semantic search over Cypher query history to surface reusable patterns
- Export impact analysis reports to PDF for change management review
