# Prompt Engineering Workout

This repository contains **hands-on workout problems and experiments for Prompt Engineering**, implemented as a Jupyter Notebook. It is designed to help understand, compare, and practice prompting techniques across **multiple Large Language Models (LLMs)** including **Anthropic Claude, OpenAI GPT, and Google Gemini**.

---

## 📌 Overview

The notebook focuses on **practical prompt engineering**, not theory alone. It demonstrates how different prompts behave across models, how to structure prompts effectively, and how to test and iterate on them programmatically.

Key goals:

* Learn prompt construction through real code
* Compare responses from different LLM providers
* Practice structured, reusable prompting patterns
* Understand environment setup and API handling

---

## 🧠 Topics Covered

* Prompt Engineering basics
* Multi-model prompt execution (Claude, GPT, Gemini)
* Zero-shot prompting
* Few-shot prompting
* Prompt reuse through functions
* Model response comparison
* Environment variable management for API keys
* Practical experimentation and iteration

---

## 🛠️ Technologies & Tools

* **Python**
* **Jupyter Notebook**
* **Anthropic API (Claude)**
* **OpenAI API (GPT models)**
* **Google Generative AI (Gemini)**
* `dotenv` for environment variable management

---

## 📦 Required Installations

Install the required dependencies before running the notebook:

```bash
pip install anthropic
pip install openai
pip install google-generativeai
pip install python-dotenv
```

---

## 🔐 Environment Setup

Create a `.env` file in the project root and add your API keys:

```env
ANTHROPIC_API_KEY=your_anthropic_key
OPENAI_API_KEY=your_openai_key
GEMINI_API_KEY=your_gemini_key
```

The notebook loads these keys securely using `dotenv`.

---

## 📁 Project Structure

```
├── prompt_workout.ipynb   # Main notebook with all exercises
├── .env                  # API keys (not committed)
├── README.md              # Project documentation
```

---

## ▶️ How to Run

1. Clone the repository
2. Install dependencies
3. Set up `.env` with valid API keys
4. Open the notebook:

```bash
jupyter notebook prompt_workout.ipynb
```

Run cells sequentially to observe prompt behavior across models.

---

## 🧪 What This Notebook Demonstrates

* How the **same prompt** produces **different outputs** across LLMs
* Why prompt phrasing, structure, and constraints matter
* How to wrap prompts into reusable Python functions
* How to safely handle missing models or API failures

---

## 🎯 Intended Audience

* Students learning **Prompt Engineering**
* Beginners exploring **LLM APIs**
* Developers experimenting with **multi-model AI workflows**
* Anyone preparing for **AI / LLM interviews or demos**

---

## 🚀 Future Enhancements

* Add Chain-of-Thought prompting examples
* Include ReAct-style prompts
* Introduce prompt evaluation metrics
* Add comparison tables for model outputs
