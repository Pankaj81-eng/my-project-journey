# AI Test Case Generator

🎥 [Watch the demo](https://www.youtube.com/watch?v=oSUILlU8x6s)

## Business Problem

Writing comprehensive test cases manually is time-consuming and inconsistent. QA engineers spend hours translating feature descriptions into structured test scenarios, often missing edge cases. An AI system that generates test cases from natural language prompts can reduce this effort significantly while improving coverage consistency.

## Solution Overview

A smart application that generates structured test cases from natural language prompts using Mistral-7B-Instruct via Hugging Face. Users describe a feature or workflow in plain English; the system retrieves context from **two** sources - a local FAISS knowledge base and live Tavily web search - combines both into an enriched prompt, and generates a structured set of test cases exported to Excel. A Gradio web interface makes it accessible without any coding knowledge.

## Architecture

```
User Prompt (natural language)
    |
    |-- Local knowledge base --> Sentence-Transformer embeddings --> FAISS vector search
    |-- Live web search       --> Tavily Search API
    |
Combined context (local RAG + live search)
    |
Enriched Prompt
    |
Mistral-7B-Instruct (Hugging Face Inference API)
    |
Structured Test Cases  -->  Excel Export (.xlsx)
```

1. **Dual Retrieval** - a local FAISS vector store (built from a curated knowledge base, embedded with `sentence-transformers/all-MiniLM-L6-v2`) provides grounded domain context, while Tavily search adds current, live web results. Combining both gives the LLM more relevant context than either source alone.
2. **Prompt Enrichment** - the raw user prompt is combined with both retrieved contexts to produce a richer, more specific generation prompt.
3. **LLM Generation** - Mistral-7B-Instruct interprets the enriched prompt and outputs test cases in a structured format (title, steps, expected result, pass/fail criteria).
4. **Export** - Pandas and XlsxWriter format the output into a neatly structured `.xlsx` file ready for use in a test management tool.
5. **UI** - Gradio provides a simple web interface for entering prompts and downloading output.

## Technologies Used

- Python
- Mistral-7B-Instruct (Hugging Face Inference API)
- LangChain (retrieval orchestration)
- FAISS (local vector store) + Sentence-Transformers (embeddings)
- Tavily Search API (live web retrieval)
- Gradio (web UI)
- Pandas + XlsxWriter (Excel export)
- python-dotenv

## AI Concepts Demonstrated

- Retrieval-Augmented Generation (RAG) - combining a static local knowledge base with live web search
- LLM-driven structured output generation
- Prompt engineering for QA-specific tasks
- Multi-source retrieval: local vector search + live search → enrich → generate → export

## Key Learnings

- Combining local FAISS retrieval with live Tavily search covers both cases a single source misses - domain-specific context that's stable over time, and current information a static knowledge base won't have.
- RAG meaningfully improves test case quality — context-enriched prompts produce more specific, realistic scenarios than prompts without retrieval.
- Prompt engineering for structured output requires explicit format instructions and examples; the LLM needs to know exactly what schema to produce.
- Gradio is excellent for rapid QA tool prototyping — a usable UI in under 20 lines.
- The generate → export pipeline is easy to extend: swap the LLM, add new export formats, or plug in a different retrieval source without touching the rest.

## Future Enhancements

- PDF and image input support for generating test cases from design mockups
- Integration with test management tools (Jira Xray, TestRail) for direct import
- Feedback loop — allow QA engineers to rate generated test cases to improve prompts over time
- Support for BDD-format output (Given/When/Then) alongside standard test case format
