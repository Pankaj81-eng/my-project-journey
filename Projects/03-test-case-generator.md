# 03 - Test Case Generator

## 🧪 Summary
A smart application that generates test cases from natural language prompts using the Mistral-7B model via Hugging Face. Designed to simplify manual test case creation and enhance QA efficiency by auto-generating structured test cases based on the context provided.

---

## 🚀 Features

- 🤖 **LLM-Driven Test Case Creation**  
  Uses Mistral-7B-Instruct-v0.3 from Hugging Face to interpret user prompts and generate test cases.

- 📥 **Excel Export**  
  Automatically exports the test cases to a neatly formatted `.xlsx` file.

- 🖼️ **Web UI with Gradio**  
  A simple and interactive web interface for entering prompts and viewing outputs.

- 📚 **Prompt-Based Input**  
  Accepts plain English descriptions or feature summaries as input.

- 🧠 **Tavily Search Integration** (planned)  
  Implements Retrieval-Augmented Generation (RAG) with Tavily API to enrich context before test case generation.

---

## 🛠️ Tech Stack

- Python
- Mistral AI (via Hugging Face Inference API)
- Gradio
- Pandas
- OpenAI-compatible prompting
- Tavily (for enhanced context fetching)
- dotenv

---

## 🌟 Key Learnings

- 🧠 Applied retrieval techniques to improve generation quality.
- 💡 Improved prompt engineering for QA-specific output.
- 📦 Learned to structure multi-step workflows (search → enrich → generate → export).
- 🧩 Explored lightweight UI integration with Gradio for faster experimentation.

---

## ✅ Pros & Cons

**Pros**:
- Saves time in test case design.
- Easy to extend with PDF/image input later.
- Promotes consistency in test coverage.

**Cons**:
- Model accuracy depends on prompt quality.
- Complex logic may still need human validation.

---
