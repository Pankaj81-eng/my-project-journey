# Document Summarizer

## Business Problem

Long reports, meeting notes and research papers take time to read in full just to extract the key points. A tool that generates a concise, accurate summary on demand saves that time and makes document review and knowledge-sharing faster across a team.

## Solution Overview

A Streamlit app that accepts `.txt`, `.pdf` and `.docx` uploads, extracts the text, and uses Azure OpenAI to generate a concise summary. Credentials are managed via `.env` rather than hardcoded, and the interface is simple enough for non-technical users to upload a document and get a summary with no setup.

## Architecture

```
Document upload (.txt / .pdf / .docx)
    |
Text extraction (PyPDF2 / python-docx)
    |
Azure OpenAI  --  summarisation
    |
Streamlit UI  --  display summary
```

## Technologies Used

- Python
- Streamlit
- Azure OpenAI
- PyPDF2, python-docx
- python-dotenv

## AI Concepts Demonstrated

- LLM-based summarisation over arbitrary uploaded documents
- Multi-format text extraction as a pre-processing step before an LLM call
- Environment-based credential management for API access

## Key Learnings

- Summarisation quality is only as good as the text extraction feeding it - getting clean text out of PDFs and Word documents took more care than the summarisation call itself.
- Managing API credentials via `.env` from the start, rather than retrofitting it later, kept the project safe to iterate on without worrying about accidental exposure.

## Code

Private repo (`Document-Summarizer`) - a personal productivity tool, kept private.

## Future Enhancements

- Support longer documents via chunked summarisation with a final merge pass
- Add adjustable summary length/detail as a user-facing option
