# AI Test Case Generator

## Business Problem

Writing comprehensive test cases manually is time-consuming and inconsistent. QA engineers spend hours translating feature descriptions into structured test scenarios, often missing edge cases. An AI system that generates test cases from natural language prompts can reduce this effort significantly while improving coverage consistency.

## Solution Overview

A smart application that generates structured test cases from natural language prompts using Mistral-7B via Hugging Face. Users describe a feature or workflow in plain English; the system retrieves relevant context via Tavily search (RAG), enriches the prompt, and generates a structured set of test cases exported to Excel. A Gradio web interface makes it accessible without any coding knowledge.

## Architecture

```
User Prompt (natural language)
    ↓
Tavily Search (RAG — retrieve relevant context)
    ↓
Enriched Prompt
    ↓
Mistral-7B (Hugging Face Inference API)
    ↓
Structured Test Cases
    ↓
Excel Export (.xlsx)
```

1. **RAG Retrieval** — Tavily fetches relevant web results for the feature being tested, providing the LLM with current, grounded context beyond its training data.
2. **Prompt Enrichment** — the raw user prompt is combined with retrieved context to produce a richer, more specific generation prompt.
3. **LLM Generation** — Mistral-7B-Instruct interprets the enriched prompt and outputs test cases in a structured format (title, steps, expected result, pass/fail criteria).
4. **Export** — Pandas and XlsxWriter format the output into a neatly structured `.xlsx` file ready for use in a test management tool.
5. **UI** — Gradio provides a simple web interface for entering prompts and downloading output.

## Technologies Used

- Python
- Mistral-7B-Instruct (Hugging Face Inference API)
- Tavily Search API (RAG retrieval)
- Gradio (web UI)
- Pandas + XlsxWriter (Excel export)
- python-dotenv

## AI Concepts Demonstrated

- Retrieval-Augmented Generation (RAG)
- LLM-driven structured output generation
- Prompt engineering for QA-specific tasks
- Multi-step workflow: retrieve → enrich → generate → export

## Key Learnings

- RAG meaningfully improves test case quality — context-enriched prompts produce more specific, realistic scenarios than prompts without retrieval.
- Prompt engineering for structured output requires explicit format instructions and examples; the LLM needs to know exactly what schema to produce.
- Gradio is excellent for rapid QA tool prototyping — a usable UI in under 20 lines.
- The generate → export pipeline is easy to extend: swap the LLM, add new export formats, or plug in a different retrieval source without touching the rest.

## Screenshots

_Screenshots to be added._

## Future Enhancements

- PDF and image input support for generating test cases from design mockups
- Integration with test management tools (Jira Xray, TestRail) for direct import
- Feedback loop — allow QA engineers to rate generated test cases to improve prompts over time
- Support for BDD-format output (Given/When/Then) alongside standard test case format
