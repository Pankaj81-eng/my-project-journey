# Finance Insights App

## Business Problem

Bank statements are hard to make sense of at a glance - a list of transactions doesn't tell you where your money actually went. A lightweight tool that turns a raw statement into a visual breakdown by category makes that immediately obvious, without needing a full personal-finance platform.

## Solution Overview

A Streamlit app that parses CSV bank statements and visualises the spending breakdown by category using Plotly. Built for personal use rather than as a hosted product - it reads a statement, structures the transactions, and renders an interactive pie chart of where the money went.

## Architecture

```
CSV bank statement
    |
Pandas  --  parse + structure transactions
    |
Category grouping
    |
Plotly  --  interactive pie chart (Streamlit UI)
```

## Technologies Used

- Python
- Streamlit
- Plotly
- Pandas

## Key Learnings

- Plotly produces clean, interactive charts with very little code compared to hand-rolling chart rendering.
- Streamlit is an effective way to put a usable UI in front of non-technical users without building a separate frontend.
- CSV parsing needs to be defensive - real bank export formats vary more than expected, and exception handling around parsing mattered more than the visualisation logic.

## Code

Private repo (`FinanceApp`) - built for personal use over personal bank data, so it stays private rather than public.

## Future Enhancements

- Fuzzy-match transaction descriptions to categories automatically, rather than relying on manual categorisation
- Support statement formats beyond the current CSV layout
