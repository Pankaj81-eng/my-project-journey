# LangChain Azure Agent

## Business Problem

Before building multi-agent systems for enterprise clients, it's worth having a minimal, correct reference for the fundamentals: an LLM that can call tools rather than just generate text. Most tutorials either oversimplify this or bury it in framework boilerplate.

## Solution Overview

A small command-line agent built on LangChain and Azure OpenAI, with two custom tools (a calculator and a greeting tool) registered via the `@tool` decorator and dispatched through `AgentType.OPENAI_FUNCTIONS`. The whole thing is under 60 lines - deliberately minimal, so the tool-calling mechanics are visible rather than hidden behind abstraction.

## Architecture

```
User input (CLI)
    ↓
LangChain AgentExecutor (OPENAI_FUNCTIONS)
    ↓
Azure OpenAI (function-calling capable deployment)
    ↓
Tool dispatch: calculator | say_hello
    ↓
Response
```

## Technologies Used

- LangChain
- Azure OpenAI (function calling)
- Python, python-dotenv

## AI Concepts Demonstrated

- Tool/function calling with structured inputs
- Agent-tool dispatch loops
- Azure OpenAI deployment configuration

## Key Learnings

- Registering a tool with `@tool` isn't enough - it also has to be passed into the `tools` list handed to `initialize_agent`, or the agent never sees it. An easy mistake that silently drops functionality rather than erroring.
- `AgentType.OPENAI_FUNCTIONS` needs a deployment that actually supports function calling (`gpt-4`, `gpt-4o`, or compatible) - it fails unhelpfully otherwise.

## Code

Public repo: [github.com/Pankaj81-eng/langchain-azure-agent](https://github.com/Pankaj81-eng/langchain-azure-agent)

## Future Enhancements

- Add tools with external side effects (API calls, file I/O) to demonstrate error handling in the dispatch loop
- Swap `initialize_agent` for LangGraph, matching the orchestration pattern used in the enterprise agentic platforms
