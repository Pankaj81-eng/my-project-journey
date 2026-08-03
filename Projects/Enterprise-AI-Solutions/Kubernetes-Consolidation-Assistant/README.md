# Kubernetes Consolidation Assistant

## Business Problem

An enterprise infrastructure environment had hundreds of Kubernetes workloads deployed across multiple clusters — many legacy, some redundant, others undocumented. The consolidation and modernisation programme needed to understand what was running, which workloads could be merged or retired, and how to safely migrate Helm charts to updated configurations. Doing this manually at scale was impractical.

## Solution Overview

A multi-agent AI system built with LangGraph that automates the discovery, analysis, and planning phases of a Kubernetes consolidation programme. A Discovery Agent maps running workloads and their relationships into a Neo4j graph. A Planning Agent reasons over the graph to produce a prioritised consolidation plan. A Helm Transformer Agent rewrites and validates Helm charts for the target state. GitHub Integration allows plans and transformed charts to be submitted as pull requests for human review.

## Architecture

```
Discovery Agent  →  Neo4j Workload Graph
                          ↓
                   Planning Agent
                   (LangGraph state machine)
                          ↓
                 Helm Transformer Agent
                          ↓
                   GitHub PR Integration
```

1. **Discovery Agent** — connects to Kubernetes clusters via the API server, extracts workload metadata (Deployments, Services, ConfigMaps, resource limits), and loads a graph of workloads, dependencies, and namespace relationships into Neo4j.
2. **Planning Agent** — traverses the graph using Cypher queries, scores workloads for consolidation risk and opportunity, and produces an ordered migration plan with justifications.
3. **Helm Transformer Agent** — takes the plan output and rewrites Helm chart values and templates for the target cluster configuration, validating against schema.
4. **GitHub Integration** — submits transformed charts and migration plans as pull requests, enabling human-in-the-loop review before any change is applied.

## Technologies Used

- LangGraph (multi-agent orchestration)
- Neo4j (workload relationship graph)
- Cypher (graph queries and traversal)
- Kubernetes API (workload discovery)
- Helm (chart transformation)
- GitHub API (pull request integration)
- FastAPI (internal agent communication)
- Python

## AI Concepts Demonstrated

- Agentic AI (multi-agent system with distinct roles)
- Planning Agent (prioritised, reasoned consolidation plan)
- Knowledge Graph (workload dependency modelling)
- LangGraph state machine (multi-step agent orchestration)
- Infrastructure Modernisation
- Human-in-the-loop review via GitHub PRs

## Key Learnings

- Breaking the problem into three distinct agents (discover, plan, transform) made each agent testable in isolation and easier to debug.
- LangGraph's state machine model is well suited to multi-step processes where earlier steps must complete before later ones begin.
- Graph traversal for dependency analysis is far more reliable than heuristics — Cypher shortest-path queries naturally surface migration risk.
- Human-in-the-loop via GitHub PRs was essential for enterprise adoption — no automated system should apply infrastructure changes without a review gate.

## Future Enhancements

- Automated regression testing of transformed Helm charts in a preview namespace before PR submission
- Cost analysis layer — estimate cloud spend before and after consolidation
- Integration with enterprise CMDB to cross-reference discovered workloads against official asset records
- Drift monitoring — alert when deployed state diverges from the approved plan
