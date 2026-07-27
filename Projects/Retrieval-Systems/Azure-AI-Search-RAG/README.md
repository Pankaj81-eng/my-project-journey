# Azure AI Search - Document Q&A

## Business Problem

Documents scattered across a team's storage are only useful if they can be found. Manually searching PDFs, Word docs and text files for a keyword or topic doesn't scale past a handful of files - enterprises need retrieval that indexes and searches at the storage layer, not the application layer.

## Solution Overview

A Streamlit app that uploads documents to Azure Blob Storage, indexes them with Azure AI Search, and returns full-text matches with highlighted snippets across the whole document set. An Azure OpenAI-backed summarisation function (`action.py`) provides a concise summary of any matched content.

## Architecture

```
Streamlit UI
    |
    |-- upload --> Azure Blob Storage --> Azure AI Search indexer
    |                                            |
    |-- query  ------------------------------>  index --> highlighted results
    |
    `-- summarise --> Azure OpenAI
```

## Technologies Used

- Streamlit
- Azure Blob Storage
- Azure AI Search (full-text search with highlighting)
- Azure OpenAI (summarisation)

## AI Concepts Demonstrated

- Enterprise document retrieval (pre-GraphRAG foundation)
- Full-text search with relevance highlighting
- Retrieval-then-summarise pattern

## Key Learnings

- Configuration should never live in application code - the original version had Azure keys and a connection string hardcoded directly in `app.py`. Moving everything to environment variables was a deliberate fix before this went public, not an afterthought.
- Disabling TLS verification to work around a certificate issue (as the original did) trades a real security control for convenience - the fix is to point at the correct CA bundle (`certifi`), not skip verification.
- Full-text search with highlighting gets you further than expected before you need embeddings - this is the natural predecessor to the GraphRAG work in the enterprise platforms.

## Code

Public repo: [github.com/Pankaj81-eng/azure-ai-search-rag](https://github.com/Pankaj81-eng/azure-ai-search-rag)

## Future Enhancements

- Add vector or hybrid search alongside the existing full-text ranking
- Automate the indexer run after upload, rather than requiring a manual trigger in the Azure Portal
