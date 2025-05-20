# 04 - TechTales AI: Your Intelligent Companion

## 🧠 Summary
TechTales AI is a conversational assistant prototype built with Python and LangChain. Designed as a knowledge-aware companion, it answers technical and general queries by integrating search, LLMs, and tool usage.

---

## 🚀 Features

- 💬 **Conversational Agent Flow**  
  Built with LangChain's `initialize_agent` to handle dynamic tool usage.

- 🔍 **Search Tool Integration**  
  Uses DuckDuckGo or Tavily to fetch fresh results based on user input.

- 🧮 **Tool Use**  
  Supports calculation and web search actions as part of the agent workflow.

- 📜 **Custom Prompting**  
  Modular prompt design stored in a `.txt` file for easy tweaking.

---

## 🛠️ Tech Stack

- Python
- LangChain
- Mistral-7B (Hugging Face)
- Tavily Search API
- DuckDuckGo API
- dotenv

---

## 🌟 Key Learnings

- 🤖 Understanding agent architectures (tool-aware vs. tool-less).
- 🔁 Modular component integration (tools, models, prompts).
- 📡 Built-in streaming and real-time search application.
- 🧱 Used LangChain's `load_tools()` and agent workflow effectively.

---

## ✅ Pros & Cons

**Pros**:
- Modular and extensible for new tools.
- Real-time data fetching increases answer relevance.

**Cons**:
- LangChain overhead can slow down processing.
- Dependency on external APIs (Tavily, DuckDuckGo).

---
