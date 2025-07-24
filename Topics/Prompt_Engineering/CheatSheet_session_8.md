
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
# Cheatsheets – Session 09 Step 3 & Step 4

📌 This file contains raw, unedited training content including full prompts, inputs, outputs, and feedback.

---

## ✅ Cheatsheet – Step 3: Logging, Feedback Loops, and Regression Tracking

| Key | Meaning |
|-----|---------|
| `prompt` | The exact input instruction sent to the LLM. |
| `fixture_input` | The data or context the model should use to respond (e.g., Gherkin, requirement text, etc.). |
| `llm_output` | The generated response from the LLM. |
| `match_type` | The method or strategy used to verify correctness (e.g., `keyword-inclusion`, `exact-match`, `summary-contains-key-requirements`). |
| `oracle_verdict` | Ground-truth answer from a human expert — usually `"pass"` or `"fail"`. |
| `assertion_verdict` | Result of automated assertion logic — `"pass"` or `"fail"`. |
| `result_classification` | Final verdict: `"TP"` (True Positive), `"FP"` (False Positive), `"FN"` (False Negative), `"TN"` (True Negative). |
| `comments` | Notes about edge cases, unusual behavior, or additional validation insights. |

---

## 🔁 Cheatsheet – Step 4: Feedback Loop Mechanics & Test Memory

| Key | Meaning |
|-----|---------|
| `test_id` | Unique identifier for the test or case (e.g., `01-fn-alk-mutation`). |
| `prompt` | The original instruction tested (same as in Step 3). |
| `fixture_input` | The specific case or data used for the test run. |
| `llm_output` | The output received from the model. |
| `oracle_verdict` | Human judgment on correctness — `"pass"` or `"fail"`. |
| `assertion_verdict` | Automated logic's result — `"pass"` or `"fail"`. |
| `result_classification` | `"TP"`, `"FP"`, `"FN"`, or `"TN"` — classification of test outcome. |
| `issue_identified` | Explanation of what failed (e.g., “missing ALK mutation”). |
| `suggested_fix` | Recommendation to improve prompt, model, or logic. |
| `feedback_action` | What to do next: re-prompt, tag, escalate, log to memory, etc. |

---


## 🧠 Cheatsheet – Step 5: Regression and Replay Memory

| Term | Meaning |
|------|--------|
| **Replay Memory** | Stores previous prompt-input-output combinations with verdicts for retesting and validation |
| **Regression Detected** | A previously passing test now fails in a newer version |
| **Regression Resolved** | A previously failing test now passes (important to track for history and release notes) |
| **last_known_verdict** | The outcome from the most recent known execution |
| **current_verdict** | The outcome from the latest test run |
| **expected_match_type** | Strategy used to compare LLM output to the test oracle (`exact`, `fuzzy_contains`, etc.) |
🧠 Compiled by: Pavan Kumar  
🗓️ Date: 2025-07-21

---
## 🧠 Cheatsheet – Step 6: Regression Labels and Heuristics

| Field | Purpose |
|-------|---------|
| `regression_label` | Tags root cause or fix reason (e.g., `false_negative`, `intent_changed`) |
| `replay_heuristic` | Defines when test should be replayed |
| `confidence_score` | Probability that the verdict is accurate (0.0 = unsure, 1.0 = certain) |
