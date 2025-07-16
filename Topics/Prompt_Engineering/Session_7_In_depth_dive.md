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

----
# Types of Assertive Prompts – Exact Notes

## 🧩 Types of Assertive Prompts

To test and control LLM behavior effectively, we use **different kinds of assertive strategies** depending on what we’re trying to *guarantee or constrain*.

Here are the 4 most common types, aligned with QA concepts:

---

### 1. **Format-Enforcing Prompts**

- 🔧 **What it does**: Forces output into a strict structure like JSON, YAML, or a numbered list.
- 🧪 **Why it's used**: Enables automated parsing and validation in test pipelines.
- 🧑‍💻 **QA Analogy**: Schema validation, contract tests.

#### ✅ Prompt Example:
> “Output your diagnosis in this exact JSON format:  
```json
{ "condition": "<name>", "severityScore": 0-10 }
```
Do not return any other explanation or text.”

---

### 2. **Scope-Limiting Prompts**

- 🔧 **What it does**: Restricts what the model is allowed to comment on or include.
- 🧪 **Why it's used**: Keeps the model within compliance boundaries or test scope.
- 🧑‍💻 **QA Analogy**: Function guards, domain constraints.

#### ✅ Prompt Example:
> “You are not allowed to suggest treatments. Only mention diagnostic possibilities.”

---

### 3. **Refusal-Enforcing Prompts**

- 🔧 **What it does**: Instructs the model to *refuse* to answer certain queries or acknowledge uncertainty.
- 🧪 **Why it's used**: Helps catch hallucinations or unsupported speculation.
- 🧑‍💻 **QA Analogy**: Negative test validation, error handling.

#### ✅ Prompt Example:
> “If you are not 100% certain based on the context provided, respond only with: ‘I don’t know based on this input.’”

---

### 4. **Deterministic/Token-Control Prompts**

- 🔧 **What it does**: Uses constraints like `temperature=0`, banned words, or phrasing to reduce output variability.
- 🧪 **Why it's used**: Required for regression testing or consistent automation.
- 🧑‍💻 **QA Analogy**: Test repeatability, snapshot testing.

#### ✅ Prompt Example:
> “Always respond with one of: [‘YES’, ‘NO’, ‘UNKNOWN’] — no other phrasing allowed.”

---

### 🔁 Combined Prompts (Best Practice)

You’ll often **combine multiple types** in one prompt. For example:

> “Respond only in JSON format. Use ‘UNKNOWN’ if unsure. Do not include any medical treatment suggestions. Keep output under 100 tokens.”

---

## 📊 Summary Table

| Type                     | Controls             | QA Equivalent             |
|--------------------------|----------------------|---------------------------|
| Format-Enforcing         | Output structure     | Schema validation         |
| Scope-Limiting           | Output domain        | Input guards              |
| Refusal-Enforcing        | Uncertainty behavior | Negative tests, fallbacks |
| Deterministic Prompting  | Output consistency   | Repeatable test cases     |

Or shall I guide you through **hands-on exercises and QA comparisons now**?

👉 Please reply: **Types First** or **Go to Exercises**
