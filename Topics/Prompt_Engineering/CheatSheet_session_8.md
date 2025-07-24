
# AgentTest – AI QA Copilot  
## ✅ Session 08 Cheatsheet: Steps 3–6 Summary  
**Date**: 2025-07-21

---

### 🔹 Step 3: Match Types = Assertion Strategies

| Match Type           | QA Assertion Equivalent             | Use When... |
|----------------------|--------------------------------------|-------------|
| `equals`             | `assertEquals`                      | Exact match required |
| `contains`           | `assertIn`, `assertContains`        | Partial phrase must appear |
| `regex`              | `assertRegex`                       | Pattern expected in output |
| `semantic-similar`   | `assertAlmostEqual` (semantic)      | Meaning must match, wording can vary |
| `json-match`         | `assertDictEqual`                   | Structured JSON must match |
| `list-contains-all`  | `assertItemsEqual` or subset match | List must include all expected items |
| `llm-judge`          | Custom test oracle                  | Another LLM judges output quality |

---

### 🔹 Step 4: Prompt Coverage = Code Coverage

| Coverage Type         | Description |
|------------------------|-------------|
| **Concept Coverage**   | Covers all key features/skills of the prompt |
| **Pattern Coverage**   | Rephrased inputs, syntax variation |
| **Path Coverage**      | Trigger different logic or steps in reasoning |
| **Failure Coverage**   | Known model flaws, edge cases, adversarial input |

**Test Strategy Examples**:
- Prompt variant testing
- Few-shot vs zero-shot
- Regression prompting
- Edge-case injection

---

### 🔹 Step 5: Prompt Fixtures = Test Data Factories

- Reusable input sets injected into prompt templates
- Allows generalized, parameterized prompt testing

**Fixture Format Example**:
```json
{
  "id": "qa_edge_null_pointers",
  "component_description": "Act as QA engineer, test prompt input validation and null handling."
}
```

**Use Cases**:
- Edge behavior
- Domain coverage
- Failure reproduction
- Parameter sweeping

---

### 🔹 Step 6: Prompt Oracles = Test Oracles

- An LLM acts as a **judge** to verify the correctness of another LLM’s output.
- Needed when correctness is fuzzy, subjective, or contextual.

**LLM-as-Judge Prompt Format**:
```text
Given a prompt, input, and model output:
1. Check content relevance
2. Check formatting/constraints (e.g. plain English, <100 words)
3. Respond YES/NO with reason
```

**Example Criteria**:
- Match to source input
- Tone/style (e.g., beginner-friendly)
- Length limit
- No hallucinations

---

✅ Use this cheatsheet to rapidly design, test, and evaluate prompts in your AI QA pipeline.



## 🧾 Cheatsheet – Step 4: Feedback Loop Mechanics

| Concept | Description |
|--------|-------------|
| **Feedback Loop** | A process to learn from test verdicts (TP, FP, FN, TN) and adjust prompts, examples, or memory. |
| **Test Memory** | Persistent storage of past prompt/input/output/verdict for reuse and comparison. |
| **Result Classification** | `"TP"`: Passed correctly; `"FP"`: Incorrect pass; `"FN"`: Missed expectation; `"TN"`: Correct fail |
| **Suggested Fix** | Targeted prompt tweak, example injection, or model escalation based on failure mode. |
| **Feedback Action** | Logging, tagging, retrying, or enriching prompt chain to prevent repeat failures. |

---
