# AI Test Data Generator

## Business Problem

Manual test data creation is repetitive, time-consuming, and often produces unrealistic data that fails to surface real bugs. QA teams need large volumes of structured, realistic test data quickly — matching specific field types, formats, and constraints — and being able to regenerate it on demand when test schemas change.

## Solution Overview

A Flask-based web application that lets users define custom field schemas (field name, data type, constraints) and generate realistic synthetic test data powered by Azure OpenAI. Field definitions are stored in SQLite for reuse across sessions. Generated data is exported as a formatted Excel file ready for use in automated or manual testing workflows.

## Architecture

```
Web UI (Flask + Jinja2)
    ↓
SQLite (field definition storage)
    ↓
Azure OpenAI (synthetic data generation)
    ↓
Pandas + XlsxWriter (Excel export)
```

1. **Schema Definition** — users define fields via the UI: name, data type, constraints (length, required/optional, format). Definitions are persisted in SQLite and reusable across sessions.
2. **AI Generation** — field definitions are serialised into a structured prompt sent to Azure OpenAI. The model generates human-like synthetic records matching the schema.
3. **Export** — Pandas formats the records and XlsxWriter produces a clean `.xlsx` file with appropriate column headers and types.
4. **Session Management** — stored definitions can be viewed, reused, or cleared; users don't need to redefine the schema each session.

## Technologies Used

- Python
- Flask (backend framework)
- Jinja2 (HTML templating)
- SQLite (field definition persistence)
- Azure OpenAI (synthetic data generation)
- Pandas + XlsxWriter (Excel export)
- python-dotenv (credential management)

## AI Concepts Demonstrated

- Retrieval-Augmented Generation (schema-driven prompt construction)
- Structured LLM output (schema-constrained generation)
- Prompt engineering for data generation tasks

## Key Learnings

- Schema injection into prompts (field names, types, constraints) is essential — without it the LLM generates plausible but wrong data.
- Separating field definition storage from generation logic makes the system reusable: define once, generate many times with different row counts.
- `.env`-based credential management is straightforward with `python-dotenv` and keeps API keys out of source code.
- Excel export with proper formatting (column widths, typed cells) makes the output immediately usable without manual cleanup.

## Future Enhancements

- CSV export alongside Excel
- Input validation for field constraints before sending to the LLM
- Login-based user accounts to save personal field templates
- Integration with test automation tools to auto-seed databases with generated data
- Support for relational data (foreign key relationships between datasets)
