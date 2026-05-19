# EduPilot 🚀 — AI-Powered Course Recommender

A conversational course advising chatbot built for Indiana University students. EduPilot takes natural language input about a student's career goals and recommends tailored courses from the MSDS catalog using the **DeepSeek-V3** large language model via Hugging Face Inference API.

Built at the **Luddy Hackathon**.

---

## Demo

> "I want to become a data analyst with strong visualization skills"

EduPilot responds with 3–5 personalized course recommendations, including credits, prerequisites, semester availability, and a short justification for each pick.

---

## Features

- 💬 Chat-based UI built with Streamlit
- 🤖 LLM-powered recommendations via DeepSeek-V3-0324 (Hugging Face / Novita provider)
- 📋 Reads live course catalog from a CSV (no hardcoding)
- 📊 Embedded Power BI dashboards (Course Dashboard & Professor Dashboard)
- 📚 Direct links to Course Catalog and Enrollment Guide
- 🎨 Custom IU-branded UI (sidebar, header, chat bubbles)

---

## Project Structure

```
├── model.py              # LLM backend — loads catalog, builds prompt, calls DeepSeek API
├── gpt_ui.py             # Streamlit frontend — chat UI, sidebar, session state
├── dataset.csv           # Course catalog (must be present in root directory)
└── Project Logo.png      # Logo used in footer (optional)
```

---

## How It Works

1. `model.py` reads `dataset.csv` and formats all course metadata into a structured text catalog.
2. When a user submits a message, the catalog + user input are combined into a prompt.
3. The prompt is sent to `deepseek-ai/DeepSeek-V3-0324` via Hugging Face's `InferenceClient`.
4. The model returns a structured recommendation list, which is displayed in the chat UI.

---

## Course Catalog Format

`dataset.csv` should contain the following columns:

| Column | Description |
|--------|-------------|
| `Course Code` | Unique course identifier |
| `Course Title` | Full course name |
| `Credits` | Credit hours |
| `Description` | Course description |
| `Prerequisites` | Required prior courses |
| `Skills` | Skills taught |
| `Semester Offered` | Fall / Spring / Both |
| `Delivery Mode` | In-person / Online / Hybrid |
| `Project Based` | Yes / No |
| `Instructor Name` | Faculty name |
| `Instructor Rating` | Numerical rating |
| `Course Value Score` | Composite quality score |
| `Total Feedback Count` | Number of student reviews |
| `Positive Percentage` | % positive feedback |

---

## Requirements

```bash
pip install streamlit pandas huggingface_hub Pillow
```

## Running the App

```bash
streamlit run gpt_ui.py
```

Make sure `dataset.csv` is in the same directory as both Python files before running.

---

## Configuration

The Hugging Face API key is set directly in `gpt_ui.py`. To use your own key, replace the `api_key` value in:

```python
reply = model.get_recommendations_from_input(user_input, api_key="your_hf_key_here")
```

---

## External Integrations

| Resource | Link |
|----------|-------|
| 📘 Course Dashboard | Power BI — course-level analytics |
| 🧑‍🏫 Professor Dashboard | Power BI — instructor-level analytics |
| 🗂️ Course Catalog | SharePoint document |
| 📄 Enrollment Guide | MSDS enrollment PDF |

Links are embedded in the app sidebar and accessible without authentication.
