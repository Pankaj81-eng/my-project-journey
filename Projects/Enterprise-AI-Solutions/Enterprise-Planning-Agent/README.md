# Enterprise Planning Agent

## Business Problem

Large enterprise modernisation initiatives involve coordinating dozens of workstreams, dependencies, and stakeholders. Programme managers spend significant time manually synthesising status reports, identifying blockers, and producing updated plans. This work is repetitive, slow, and prone to missing cross-workstream dependencies.

## Solution Overview

An agentic AI planning system that ingests programme data (workstream status, dependencies, risks, and timelines), reasons over it using a LangGraph multi-step planning loop, and produces updated programme plans, risk summaries, and recommended next actions. It operates as a planning co-pilot — not replacing human judgement but accelerating the synthesis and drafting work.

## Architecture

```
Data Ingestion (structured + unstructured inputs)
    ↓
Knowledge Graph (workstreams, dependencies, risks)
    ↓
LangGraph Planning Loop
├── Context Retrieval Agent (GraphRAG)
├── Risk Analysis Agent
├── Plan Generation Agent
└── Output Formatting Agent
    ↓
Structured Programme Plan + Recommendations
```

1. **Ingestion** — workstream data, status updates, and risk logs are ingested from structured sources (spreadsheets, project tools) and loaded into a graph.
2. **Knowledge Graph** — Neo4j models workstreams as nodes with `DEPENDS_ON`, `BLOCKS`, and `RISKS` relationships, making dependency chains traversable.
3. **LangGraph Loop** — a state machine orchestrates four agents in sequence: context retrieval, risk analysis, plan generation, and output formatting. Each agent specialises in one task and passes state forward.
4. **Output** — produces a structured programme plan document with prioritised actions, flagged risks, and dependency impact analysis.

## Technologies Used

- LangGraph (multi-step planning orchestration)
- Neo4j (dependency and risk graph)
- LangChain (LLM integration and RAG)
- OpenAI (Azure deployment)
- FastAPI (API layer)
- Python

## AI Concepts Demonstrated

- Agentic AI (multi-agent planning loop)
- Planning Agents (structured, multi-step reasoning)
- Knowledge Graphs (workstream dependency modelling)
- GraphRAG (graph-augmented context retrieval)
- Retrieval-Augmented Generation

## Key Learnings

- A planning agent works best when it has a structured representation of dependencies — flat text inputs produce vague plans; graph-backed inputs produce specific, prioritised actions.
- Separating retrieval, analysis, and generation into distinct agents with clear state contracts makes the system easier to debug and improve incrementally.
- LLM-generated plans need grounding — passing graph context alongside the prompt dramatically reduces hallucinated dependencies.
- Human-in-the-loop checkpoints matter: the agent drafts, the human approves. This framing was key to stakeholder trust.

## Screenshots

_Screenshots to be added._

## Future Enhancements

- Integration with project management tools (Jira, Monday.com) for live data ingestion
- Automated weekly plan refresh with change-diff highlighting
- Scenario modelling — "what if workstream X slips by two weeks?" analysis
- Voice briefing output — generate a spoken programme summary for leadership review
