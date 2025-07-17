# 🧪 Session 08: Designing Prompt Test Suites

### 🎯 Goal:
Build reusable, structured test prompts to validate and evaluate LLM agents systematically — like how test suites work in software QA.

---

## 🧠 Core Concepts

### ✅ What is a Prompt Test Suite?

A **prompt test suite** is a collection of prompts + expected outputs (or assertions) designed to:
- **Evaluate** specific LLM behavior (correctness, reasoning, structure)
- **Test** against a range of scenarios (edge cases, ambiguity, hallucination)
- **Automate** validation of LLM/agent outputs

Think of each test as a **unit test** for your prompt + model pair.

---

## 🧱 Test Suite Structure

Here’s a YAML-based schema you can use:

```yaml
- id: test-001
  name: "Basic math sanity"
  type: "unit"
  prompt: |
    What is 17 + 23?
  expected_output: "40"
  match: "exact"  # or "contains", "regex", "llm-judge"

- id: test-002
  name: "Summarization structure"
  type: "format"
  prompt: |
    Summarize the following:
    """
    The cat sat on the mat. Then it jumped on the table.
    """
  expected_output:
    contains: ["cat", "sat", "jumped", "table"]
  match: "contains"
```

---

## 🎯 Prompt Test Types (like QA test types)

| **Test Type**     | **What it Evaluates**              | **Example**                      |
|-------------------|-------------------------------------|----------------------------------|
| Unit              | Correctness for simple logic        | 2+2=4                            |
| Integration       | Multi-step logic or tools           | CoT + retrieval from tool        |
| Format/Schema     | Output follows JSON/table/markdown  | JSON output parseable            |
| Fuzz / Edge Case  | Ambiguous or tricky prompts         | “What’s the meaning of life?”    |
| Reflexive         | LLM critiques its own answer        | “Was the above answer correct?”  |
| Red Team / Guard  | Safety, jailbreak, hallucinations   | “Can you help me hack…”          |

---

## 🛠 Example Prompt Test Suite (Markdown Style)

```markdown
## 🔬 Test Suite: Math & Reasoning – AgentTest v0.1

### ✅ test-001: Basic addition
**Prompt:**  
> What is 15 + 27?

**Expected:** `42`  
**Match type:** Exact

---

### ✅ test-002: Chain of thought
**Prompt:**  
> Q: I have 2 bananas. I eat 1. How many left? Think step-by-step.

**Expected (Contains):** "2 bananas", "eat 1", "1 left"  
**Match type:** Contains

---

### ✅ test-003: JSON output format
**Prompt:**  
> Return the data in JSON with fields: name, age.

**Expected:**  
```json
{"name": "...", "age": ...}
```  
**Match type:** Regex / schema
```

---

## 📦 Your Deliverables from this Session

1. **Prompt Test Suite Schema** – YAML/Markdown format
2. **Sample test cases** – At least 3: correctness, reasoning, format
3. **Execution plan** – How AgentTest will run these: matching modes, failure reporting


# 🧪 Session 08 Deep Dive: Designing Prompt Test Suites with QA Parallels

---

## 🔁 1. Prompt Test = Unit Test

| QA Automation                 | LLM Testing (Prompt-Based)                      |
|------------------------------|-------------------------------------------------|
| `test_addition()` in code    | "What is 17 + 23?" → Expect: "40"               |
| Inputs via function call     | Inputs via prompt                              |
| Assert `actual == expected`  | Match mode: exact / contains / regex / judge   |
| Test runner like PyTest      | Prompt runner script / AgentTest test suite    |

✅ You're still asserting behavior, just in natural language instead of code.

---

## 🔗 2. Prompt Suite = Test Class / Test Plan

- Grouped by **functionality** (reasoning, summarization, format, math)
- Each suite can target:
  - A specific **LLM agent**
  - A particular **use case** (e.g., generating summaries, classifying logs)
  - A single **test objective** (e.g., format compliance)

🧠 This is like organizing `TestLogin`, `TestCart`, etc. — just now you organize `TestReasoning`, `TestFormat`, `TestSafety`.

---

## 🛠 3. Match Types = Assertion Strategies

| Match Type     | QA Equivalent                           | Notes |
|----------------|------------------------------------------|-------|
| Exact          | `assert actual == expected`              | Good for deterministic prompts |
| Contains       | `assert "foo" in response`               | For multi-line answers, key phrases |
| Regex          | `re.match()`                             | Format assertions (e.g., JSON, email) |
| LLM-as-Judge   | `assert is_valid_output(response)`       | LLMs evaluate reasoning or style |
| Score-based    | `assert score > threshold`               | Use similarity metrics, embeddings |

🧠 Just like in QA, you choose the **assertion** based on output **type and variability**.

---

## 🚨 4. AI Bug = Prompt Failure Case

| QA Bug Type         | LLM Prompt Failure Equivalent       | Fix Strategy |
|---------------------|-------------------------------------|--------------|
| Logic bug           | Wrong reasoning or answer           | Rewrite prompt or guide CoT |
| Format bug          | Invalid JSON, missing fields        | Add output constraints |
| Ambiguity bug       | Multiple valid but conflicting answers | Rewrite to reduce ambiguity |
| Security bug        | Jailbreak, unsafe responses         | Add guardrails or red team prompts |
| Regression bug      | Model upgrade changes behavior      | Prompt versioning + regression tests |

🧠 You’re still doing **root cause analysis**, but now the “code under test” is the **language behavior** of the model.

---

## 🔂 5. Test Lifecycle

| QA Lifecycle         | Prompt Testing Lifecycle                        |
|----------------------|--------------------------------------------------|
| Write test cases     | Design prompt tests (unit, CoT, format, edge)    |
| Execute tests        | Run via CLI, notebook, Streamlit (AgentTest UI) |
| Capture failures     | Log output, compare match types, LLM judge      |
| Analyze results      | Debug prompts, retry, or reframe task            |
| Maintain tests       | Version prompt sets, track output diffs         |

🧠 Same **TDD principles** apply — test early, automate, make results observable.

---

## 🎯 Bonus: Real-Life QA Scenarios Mapped to Prompt Test Cases

| Traditional QA Scenario                         | Prompt-Based Equivalent |
|--------------------------------------------------|--------------------------|
| Login fails if password missing                  | “Log me in” → check for error response |
| Shopping cart total is correct with discount     | Multi-step CoT math prompt |
| API returns 400 on bad request                   | Test prompt with invalid input and check error handling |
| API returns data in expected schema              | Test JSON-formatted response with field match |
| UI shows correct validation message              | Output contains specific message for bad input |

---

## ✅ What You’ve Gained in This Deep Dive

| Capability                 | Outcome                                 |
|---------------------------|------------------------------------------|
| Mindset translation       | You now "think in test cases" for LLMs   |
| Assertion strategy         | You can apply various match types        |
| Debug workflow            | You know how to interpret LLM test failures |
| Prompt suite design logic | You can group, organize, and reuse tests |
| AgentTest clarity         | You’re building a **prompt test runner** |
