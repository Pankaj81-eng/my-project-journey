# 02 - Test Data Generator

## 🧪 Summary
A lightweight Flask-based web application designed to simplify the generation of structured, synthetic test data for QA purposes. Users can define custom fields with constraints and generate realistic data powered by OpenAI. The output is downloadable in Excel format, making it suitable for both manual and automated testing workflows.

---

## 🚀 Features

- ✅ **Custom Field Definitions**  
  Define any number of fields with labels, data types, and optional constraints (e.g., length, required/optional).

- 💾 **SQLite Storage**  
  Store and manage your field definitions in a local SQLite database for reuse across sessions.

- 🧹 **Clear and View Field Options**  
  UI to view all existing definitions and clear them as needed.

- 🤖 **AI-Powered Test Data Generation**  
  Uses OpenAI (Azure deployment) to generate human-like synthetic data based on the defined schema.

- 📥 **Excel Export**  
  Automatically formats and exports the generated data into `.xlsx` files using Pandas and XlsxWriter.

---

## 🛠️ Tech Stack

- **Backend**: Python, Flask  
- **Frontend**: HTML (Jinja2 templating)  
- **Data Storage**: SQLite  
- **APIs**: OpenAI (via Azure endpoint)  
- **Utilities**: Pandas, XlsxWriter, python-dotenv

---

## 🌟 Key Learnings

- 🔐 **Environment Management**  
  Used `.env` to securely manage API keys and environment-specific configurations.

- 📚 **Prompt Engineering**  
  Learned how to craft effective prompts for OpenAI to generate structured data aligned with QA needs.

- 🗃️ **Database Integration**  
  Gained experience in integrating Flask with SQLite to persist and retrieve structured definitions.

- 🧱 **Modular Design**  
  Structured the codebase to separate logic for route handling, data generation, and file export—enabling easier maintenance and potential scaling.

- 📊 **Export Logic**  
  Implemented logic to write structured dictionaries to Excel with good formatting, enhancing QA usability.

- 🧪 **QA Utility Perspective**  
  Built with the intent to reduce time spent on manual test data creation, improving both efficiency and test case coverage.

---

## 📸 Screenshots (optional)

_Add screenshots here later to visually demonstrate field input, generation output, and Excel export._

---

## 📌 Future Enhancements

- Add validation checks for more robust user input.
- Support CSV export in addition to Excel.
- Add login-based access to save user-specific field templates.
- Integrate with test case tools to auto-fill scenarios with generated data.

