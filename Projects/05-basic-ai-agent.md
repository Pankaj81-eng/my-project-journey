# 05 - Basic AI Agent (Proof of Concept)

## 🧠 Summary
A simple and educational project that demonstrates how to create a LangChain-based AI agent using custom tools. This command-line assistant can respond to user queries and call functions like a calculator or greeting tool. Designed as a foundation to understand how AI agents operate with tools using the OpenAI (Azure) API.

---

## 🧪 Use Case

This project was primarily created to:
- Understand the structure of LangChain agents.
- Learn how tools can be created and invoked dynamically by an LLM.
- Set up a basic command-line interface for interaction.

---

## 🚀 Features

- 🛠️ **Tool-Enabled Agent**  
  Includes two basic tools:
  - `calculator`: Adds two numbers from a string like `'3,7'`.
  - `say_hello`: Greets the user with a personalized message.

- 🤖 **LLM Integration with Azure OpenAI**  
  Configured with environment variables using `python-dotenv`.

- 💬 **Interactive CLI Interface**  
  Simple text-based loop for back-and-forth communication with the agent.

- 📡 **AgentType.OPENAI_FUNCTIONS**  
  Used to enable function-style tool calling via LangChain’s agent executor.

---

## 🛠️ Tech Stack

- Python
- LangChain
- Azure OpenAI (Chat Model)
- Python Dotenv

---

## 🌟 Key Learnings

- 🧠 Learned how tools are defined using decorators in LangChain.
- 🔁 Understood the flow of agent initialization and tool selection.
- 📦 Hands-on with `initialize_agent()` and `AgentType.OPENAI_FUNCTIONS`.
- 🔐 Gained experience in securely managing credentials via `.env` files.

---

## 🔧 Example Tools

```python
# @tool
def calculator(input: str) -> str:
    """Adds two numbers given as '4,5'."""
    ...

# @tool
def say_hello(name: str) -> str:
    """Returns a greeting for the given name."""
    ...
    


✅ Pros & Cons
Pros:

Very useful for learning and debugging how agents and tools interact.

Simple structure makes it easy to extend with new tools.

Cons:

Not production-ready or context-aware.

No UI, only CLI-based interaction.