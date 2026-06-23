# Nemo AI Companion

## Business Problem

General-purpose search engines return a list of links; they don't synthesise an answer or adapt to what the user already knows. A conversational AI companion can answer technical and general queries in context, use tools to fetch fresh information, and maintain a coherent conversation across multiple turns — reducing the back-and-forth of traditional search.

## Solution Overview

TechTales AI (codenamed Nemo) is a conversational assistant prototype built with LangChain. It answers technical and general queries by combining LLM reasoning with live web search and calculator tools. The agent decides which tool to call based on the question type, fetches fresh results when needed, and synthesises a grounded answer rather than relying solely on model knowledge.

## Architecture

```
User Query
    ↓
LangChain Agent (ReAct loop)
├── Web Search Tool (Tavily / DuckDuckGo)
├── Calculator Tool
└── LLM Reasoning (Mistral-7B / GPT)
    ↓
Synthesised Answer
```

1. **Agent Loop** — LangChain's `initialize_agent` with `ZERO_SHOT_REACT_DESCRIPTION` decides at each step whether to call a tool or produce a final answer.
2. **Search Tool** — Tavily or DuckDuckGo fetch live results for factual or time-sensitive queries, providing the LLM with grounded context.
3. **Calculator Tool** — handles arithmetic and unit conversion queries precisely, avoiding LLM hallucination on numerical tasks.
4. **Prompt Design** — a custom system prompt stored in a `.txt` file shapes the agent's persona and response style, making it easy to iterate without touching code.

## Technologies Used

- Python
- LangChain (agent orchestration and tool use)
- Mistral-7B (Hugging Face Inference API)
- Tavily Search API
- DuckDuckGo Search API
- python-dotenv

## AI Concepts Demonstrated

- Agentic AI (ReAct agent loop with tool selection)
- Tool Use (web search, calculator)
- Multi-turn Conversations (context maintained across exchanges)
- Retrieval-Augmented Generation (live search grounding)

## Key Learnings

- The ReAct pattern (Reason → Act → Observe → Repeat) is intuitive to debug because each step is logged as a distinct thought — you can see exactly why the agent chose a tool.
- Grounding answers with search results significantly reduces hallucination on factual queries.
- Modular prompt files (not hardcoded strings) make persona iteration fast without touching logic.
- LangChain's `load_tools()` abstracts tool setup well for prototyping, though production systems benefit from custom tool implementations for better error handling.

## Screenshots

_Screenshots to be added._

## Future Enhancements

- Persistent conversation memory using a vector store (FAISS or Chroma) for recall across sessions
- Domain specialisation — load a custom knowledge base for a specific topic area
- Streaming responses for lower perceived latency
- Switch to LangGraph for finer control over agent state and multi-step planning
