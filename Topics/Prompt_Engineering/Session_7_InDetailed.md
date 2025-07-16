# Topic 1: Assertive Prompting – Exact Notes

## 🧠 Topic 1: Assertive Prompting

### 📌 What Is Assertive Prompting?

**Assertive prompting** is the practice of using **precise, constraint-based instructions** to shape an LLM’s output. You **don’t ask gently** — you **instruct clearly**, often with format expectations, content limits, and rules for refusal or uncertainty.

It’s a way to turn **soft natural language** into something that behaves more like **code contracts**.

---

### 🎯 Why Does This Technique Exist?

LLMs like GPT or Claude are trained to be **helpful, flexible, and verbose**. But for QA, we want:
- **Precision**
- **Predictability**
- **Repeatable formats**
- **Safe fallbacks when unsure**

So, assertive prompting evolved to:
- Prevent hallucinations
- Ensure **machine-readable outputs** (e.g., JSON for test harnesses)
- Detect when the model is **unsure or outside its scope**
- Make model behavior more **testable and auditable**

In traditional QA, we have **assert statements**, **validation rules**, and **guard clauses**.  
In LLMs, assertive prompts **mimic those behaviors through language**.

---

## 🧪 Quick Example

### ❌ Weak Prompt (not assertive):
> “Can you help me figure out what's wrong with this patient?”

### ✅ Assertive Prompt:
> “You are a diagnostic agent. Return your output strictly in this JSON format:  
```json
{ "diagnosis": "<condition>", "confidence": 0-1, "needsHumanReview": true|false }
```
If you're unsure, set `"needsHumanReview": true`. Do not guess. Do not explain anything outside the JSON.”

---

## 🔍 QA Analogy Table

| QA Concept               | Assertive Prompting Equivalent         |
|--------------------------|----------------------------------------|
| `assertTrue(value)`      | "Only output YES or NO. Nothing else." |
| Schema validation (JSON) | Prompt that demands JSON-only output   |
| Input validator          | Prompt refuses unknown/missing data    |
| Guard clause             | "If uncertain, reply with: 'I don’t know'" |

---

## ✅ Next Step

Would you like to go deeper into **types of assertive prompts** next (format enforcing, refusal enforcing, etc.) before exercises?

Or shall I guide you through **hands-on exercises and QA comparisons now**?

👉 Please reply: **Types First** or **Go to Exercises**
