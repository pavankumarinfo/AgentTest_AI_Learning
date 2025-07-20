
# Session 08 – Step 3: Match Types = Assertion Strategies

**Date**: 2025-07-20
**Session**: Deep Dive – AI Testing Concepts ↔ QA Automation
**Product**: AgentTest – AI QA Copilot

## ✅ Concept: Match Types = Assertion Strategies

In software testing, an **assertion strategy** defines how we *compare actual vs. expected* results. The same concept applies in **AI testing**, where we verify if the LLM output matches expectations under different comparison types.

We call these **Match Types**. They determine *how strict or flexible* our prompt validation should be.

### 🔢 Core Match Types (AI ↔ QA Mapping)

| Match Type           | QA Assertion Equivalent             | Use When... |
|----------------------|--------------------------------------|-------------|
| `equals`             | `assertEquals`                      | Exact match required |
| `contains`           | `assertIn`, `assertContains`        | Partial phrase must appear |
| `regex`              | `assertRegex`                       | Pattern expected in output |
| `semantic-similar`   | `assertAlmostEqual` (semantic)      | Meaning must match, even if wording varies |
| `json-match`         | `assertDictEqual`                   | Structured output (JSON/YAML) must match |
| `list-contains-all`  | `assertItemsEqual` or subset match | List must include expected elements |
| `llm-judge`          | Human-style assertion judgment      | Let another LLM judge correctness (e.g., for open-ended or creative output) |

### 🧠 Why Match Types Matter

- Helps choose **appropriate precision** for your test: strict vs fuzzy  
- Encourages modular testing of **individual behaviors**  
- Critical for test suites like `Reasoning`, `Structure`, `Factuality`, `Safety`, etc.

---

## 🧪 Exercises + Pavan's Answers

### Test Case 1
- **Prompt**: “List 3 advantages of containerization in software development.”
- **Expected**: “Lightweight, fast deployment, consistent environments”
- **Your Match Type**: `list-contains-all` ✅
- **Feedback**: Correct — checks that all expected elements are present, regardless of order or form.

### Test Case 2
- **Prompt**: “Generate a valid JSON object with keys: name, age, country.”
- **Expected**: JSON schema: `{ "name": str, "age": int, "country": str }`
- **Your Match Type**: `json-match` ✅
- **Feedback**: Correct — ensures structure and key presence, not string content.

### Test Case 3
- **Prompt**: “What is the purpose of unit testing?”
- **Expected**: Phrase _“verifies individual components”_ appears
- **Your Match Type**: `contains` ✅
- **Feedback**: Correct — validates partial phrase presence in open-form response.

### Test Case 4
- **Prompt**: “Describe the lifecycle of a Docker container.”
- **Expected**: Must include start, run, stop, remove
- **Your Match Type**: `semantic-similar` ✅
- **Feedback**: Correct — wording may vary, but meaning must align.

### Test Case 5
- **Prompt**: “Write a haiku about refactoring code.”
- **Expected**: Creative expression around the theme
- **Your Match Type**: `semantic-similar` ✅
- **Feedback**: Valid — semantic match is appropriate here, though `llm-judge` is an optional alternative.

---
✅ **Step 3 Complete**  
Next: Step 4 – Prompt Coverage = Code Coverage
