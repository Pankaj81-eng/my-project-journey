# Smart Clinical Assistant

## Business Problem

Clinical teams spend significant time searching for information — drug interactions, clinical guidelines, patient history summaries — across multiple disconnected systems. This friction slows decision-making, increases cognitive load, and can contribute to clinical errors. A trusted AI assistant that retrieves and synthesises clinical knowledge on demand can reduce this burden without replacing clinical judgement.

## Solution Overview

An AI-powered clinical decision support assistant that answers clinical queries by combining a Knowledge Graph of medical entities (conditions, treatments, drugs, guidelines) with vector-based retrieval over clinical documents. Clinicians can ask questions in natural language and receive grounded, explainable answers with source citations. The system is designed with a strict human-in-the-loop model — it surfaces information and recommendations, never makes autonomous clinical decisions.

## Architecture

```
Clinical Query (natural language)
    ↓
GraphRAG Retrieval Engine
├── Neo4j Medical Knowledge Graph
│   (Conditions → Treatments → Drugs → Guidelines)
└── Vector Store (clinical document embeddings)
    ↓
LLM Synthesis (with source citations)
    ↓
Explainable Answer + Source References
    ↓
Clinician Review and Decision
```

1. **Medical Knowledge Graph** — Neo4j models clinical entities (conditions, symptoms, treatments, drug interactions, clinical guidelines) as typed nodes with labelled relationships (`TREATS`, `CONTRAINDICATED_WITH`, `FOLLOWS_GUIDELINE`).
2. **Document Store** — clinical guideline documents and protocols are chunked and embedded into a vector store for semantic retrieval.
3. **GraphRAG** — queries retrieve both the relevant graph subgraph and semantically similar document chunks, providing the LLM with structured and unstructured context.
4. **Explainable Output** — every answer includes source citations (guideline name, document section) so clinicians can verify the information independently.
5. **Human-in-the-Loop** — the assistant is positioned as a decision support tool. No clinical action is taken without explicit clinician review and approval.

## Technologies Used

- Neo4j (medical knowledge graph)
- Cypher (graph querying)
- LangChain (GraphRAG orchestration)
- FAISS (vector similarity search)
- OpenAI (Azure deployment, LLM backbone)
- FastAPI (backend API)
- Streamlit (clinical UI prototype)
- Python

## AI Concepts Demonstrated

- Knowledge Graphs (medical entity and relationship modelling)
- GraphRAG (graph-augmented clinical retrieval)
- RAG (Retrieval-Augmented Generation)
- Explainable AI (source citations for every answer)
- Human-in-the-Loop decision support

## Key Learnings

- In healthcare, explainability is not optional — clinicians need to know where an answer came from before they can trust it. Citation-backed answers were far better received than black-box responses.
- Graph schema design for clinical data is complex: drug interactions, contraindications, and guideline hierarchies require careful relationship modelling to avoid misleading traversals.
- GraphRAG outperforms flat RAG for relationship queries ("what are the contraindications for X in patients with Y?") because the graph encodes those relationships explicitly.
- Human-in-the-loop framing is the right positioning for clinical AI — "decision support" rather than "autonomous assistant" reduces resistance and increases safe adoption.

## Screenshots

_Screenshots to be added._

## Future Enhancements

- Integration with EHR systems for patient-specific context (with appropriate access controls)
- Real-time guideline updates from authoritative clinical sources
- Audit trail — every query and response logged for clinical governance review
- Multi-modal input — accept lab reports, imaging notes, and discharge summaries for richer context
