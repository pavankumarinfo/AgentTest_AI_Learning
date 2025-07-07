
# Session 01 – Prompt Engineering Basics

## 🎯 Goals
- Understand what a *prompt* is and why it's important.
- Learn the different types of prompts.
- Practice crafting prompts to get better, more useful AI outputs.

---

## 🧠 1. What Is a Prompt?

A **prompt** is the input you give to an AI to generate a response. It could be a question, instruction, description, or a mix. How well the AI performs depends heavily on how clear and well-structured your prompt is.

**Example:**
- ❌ *Bad prompt:* `Tell me something.`
- ✅ *Good prompt:* `Give me three unusual facts about deep sea creatures, and explain each in two sentences.`

---

## 🔍 2. Types of Prompts

| Type                | Description                                               | Example |
|---------------------|-----------------------------------------------------------|---------|
| **Instructional**    | Tell the AI to do something specific                      | `"Summarize this article in 3 bullet points"` |
| **Descriptive**      | Describe what you want the AI to generate                 | `"Write a product description for a luxury smartwatch"` |
| **Conversational**   | Engage in dialogue for step-by-step help                  | `"Help me debug this error in my Python code"` |
| **Few-shot / Examples** | Provide examples to guide the AI's response          | `"Translate: 'Hello' → 'Hola', 'Goodbye' → 'Adiós'. Translate: 'Thanks' →"` |

---

## 🛠️ 3. Best Practices

- ✅ **Be specific**: Tell the AI *what* you want and *how* you want it.
- ✅ **Use context**: Include necessary background or examples.
- ✅ **Iterate**: Refine the prompt based on output quality.

---

## ✍️ 4. Exercises

### 🔸 Exercise A – Rewrite a Basic Prompt

> Original: `Write about AI.`  
**Task**: Rewrite this to be more focused and useful.

---

### 🔸 Exercise B – Give Instructions

> You want the AI to: generate a weekly plan for learning Python (2 hours/day, beginner level).  
**Task**: Write an effective prompt.

---

### 🔸 Exercise C – Create a Few-Shot Prompt

> You’re building an AI assistant that formats dates.  
Example:  
- `"Jan 1, 2025"` → `"2025-01-01"`  
- `"March 12, 2023"` → `"2023-03-12"`  
**Task**: Write a prompt using these examples and ask it to convert `"July 4, 2024"`.

---

---

## 🧪 Practice Answers & Feedback

### ✅ Exercise A – Rewrite a Basic Prompt

**Your Answer:**  
"Describe about AI in 2 sentance for School students for 3 major topics."

**Feedback:**  
- Great structure! You included audience, format, and number of topics.
- Minor improvements: fix grammar ("Describe about" → "Describe"; "sentance" → "sentence").

**Improved Version:**  
"Write a two-sentence explanation of Artificial Intelligence for school students, covering three major topics: machine learning, natural language processing, and robotics."

---

### ✅ Exercise B – Give Instructions

**Your Answer:**  
"Act as Python trainner. Provide me course for one week and share me course plan to spend daily 2 hours of time. Consider the course is for the beginner in python."

**Feedback:**  
- Clear intent and structure.
- Grammar fixes: "trainner" → "trainer".
- You can ask for topics, exercises, and resources.

**Improved Version:**  
"Act as a Python trainer. Create a beginner-friendly 7-day course plan for learning Python, with 2 hours of study time per day. Include topics, practice exercises, and recommended resources for each day."

---

### ✅ Exercise C – Few-Shot Prompt

**Your Answer:**  
"I like to provide input and output format and provide me similar input and what would be output. the data is 1. 'Jan 1, 2025' → '2025-01-01', 2. 'March 12, 2023' → '2023-03-12' and what is the output for 'July 4, 2024' ?"

**Feedback:**  
- Excellent use of examples (few-shot).
- Improve clarity and grammar for better response quality.

**Improved Version:**  
"Convert the following dates into the YYYY-MM-DD format:  
'Jan 1, 2025' → '2025-01-01'  
'March 12, 2023' → '2023-03-12'  
What is the output for: 'July 4, 2024' → ?"

---
