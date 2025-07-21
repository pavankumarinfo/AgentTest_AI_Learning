
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


# Session 08 – Step 4: Prompt Coverage = Code Coverage

**Date**: 2025-07-21  
**Session**: Deep Dive – AI Testing Concepts ↔ QA Automation  
**Product**: AgentTest – AI QA Copilot

---

## ✅ Step 4: Prompt Coverage = Code Coverage

In traditional QA, **code coverage** measures how much of your source code is exercised by automated tests. Common types include:

- **Line coverage**: Are all lines executed?
- **Branch coverage**: Are all conditional paths tested?
- **Function coverage**: Are all functions invoked?

In AI QA, we mirror this concept as **Prompt Coverage**.

---

## 🔍 Definition: Prompt Coverage

**Prompt Coverage** is the degree to which your **test prompts and assertions** exercise the behavior space of the LLM across:

| Type of Coverage     | AI Analogy                                             |
|----------------------|--------------------------------------------------------|
| **Concept coverage** | All key concepts/skills are tested (e.g. reasoning, formatting, safety) |
| **Pattern coverage** | Variants of phrasing, input patterns are tested       |
| **Path coverage**    | All meaningful reasoning branches / decision routes are invoked |
| **Failure coverage** | Do you test for known failures or model blind spots?  |

---

## 🧠 Why Prompt Coverage Matters

- Prevents **false confidence** in models due to superficial testing  
- Ensures **robustness** across prompt styles and semantic drift  
- Encourages **test thinking**: What has not been tested?

> 🧪 Like unit tests, prompt tests can pass even if the LLM fails in untested contexts. You need **prompt coverage metrics** to ensure quality.

---

## 🛠️ Prompt Coverage Strategies

| Strategy                        | Description |
|----------------------------------|-------------|
| **Concept Breakdown**           | Decompose feature into core capabilities (e.g. math, summarization, etc.) |
| **Prompt Variant Testing**      | Rephrase same intent multiple ways to catch brittle behavior |
| **Negative Prompting**          | Include adversarial inputs or edge cases |
| **Few-shot + Zero-shot Split**  | Test with examples and without |
| **Behavioral Probes**           | Insert trick prompts that test internal logic consistency |
| **Regression Prompting**        | Keep past test prompts to catch regressions after updates |

---

## 🧪 Exercise – Prompt Coverage Grid

For the feature below, fill out the **Prompt Coverage Matrix**.

### 📘 Feature: "Summarize medical reports in plain English"

#### Your Task:

Fill the following coverage dimensions:

| Coverage Type         | Example Prompt or Test Strategy |
|------------------------|---------------------------------|
| Concept Coverage       | ? |
| Pattern Coverage       | ? |
| Path Coverage          | ? |
| Failure Coverage       | ? |

➡️ Please provide your answers in the table above.

---

### ✅ Your Answers:

Test Case – Feature: "Summarize medical reports in plain English"

| Coverage Type      | Your Input |
|--------------------|------------|
| Concept Coverage   | Act as details reviewer, provide summary of each module and connection between modules using 100 token each and only give me higher level summary. |
| Pattern Coverage   | Act as a pettern designer, read through the model and share me common patterns found with system in terms of security ascepts and share me module name, commonaltiies between them. |
| Path Coverage      | Act as navigation router, provide me sequence of actions that are planned for this model and provide overal concept coverage. |
| Failure Coverage   | Act as AI QA engineer, provide list of edge coverage when halusinations starts. Provide list of failure conditions like edge cases for each concept within system. Provide me details information in a grid/table with each condition and its edge case. |

---

## ✅ Feedback on Your Prompt Coverage Matrix

| Coverage Type      | Your Input | Feedback |
|-------------------|------------|----------|
| **Concept Coverage** | *"Act as details reviewer, provide summary of each module and connection between modules using 100 tokens and only give me higher-level summary."* | ✅ Solid — targets summary compression, structural understanding, and inter-module relationships. Covers high-level summarization behavior. You could add plain-language checks (e.g., non-technical summaries). |
| **Pattern Coverage** | *"Act as a pattern designer, read through the model and share me common patterns found in terms of security aspects and share module names + commonalities."* | ✅ Great — this probes pattern detection and rephrasing in summarization. Consider extending to prompts like “TL;DR”, “explain like I’m 5”, “summarize for a compliance officer” to deepen variety. |
| **Path Coverage** | *"Act as navigation router, provide me sequence of actions that are planned for this model and provide overall concept coverage."* | ✅ Correct idea — targets procedural understanding and multi-step reasoning. Could also ask for summaries from different starting points to test alternate reasoning paths. |
| **Failure Coverage** | *"Act as AI QA engineer, provide list of edge coverage when hallucinations start… details in a grid with each condition and its edge case."* | ✅ Very strong — this is precisely the kind of adversarial and edge-case thinking we want in AI QA. Could be combined with known NLP pitfalls (e.g. negation handling, missing context) to simulate model weaknesses. |

---

✅ **Step 4 complete!**  
Next: Step 5 – Prompt Fixtures = Test Data Factories


# Session 08 – Step 5: Prompt Fixtures = Test Data Factories

**Date**: 2025-07-21  
**Session**: Deep Dive – AI Testing Concepts ↔ QA Automation  
**Product**: AgentTest – AI QA Copilot

---

## ✅ Step 5: Prompt Fixtures = Test Data Factories

In traditional QA, we often use **test data factories** or **fixtures** to generate repeatable, realistic, and diverse test data for assertions.

In AI QA, we need something similar to:

> 🔁 Generate reusable input sets (fixtures) to test a prompt’s behavior across data variations.

We call these **Prompt Fixtures**.

---

## 🔍 Definition: Prompt Fixture

A **Prompt Fixture** is a reusable, parametrized input used to test a prompt against multiple data points. It enables:

- Testing **generalization**
- Exploring **edge cases**
- Supporting **parameterized tests**
- Reproducing **failures**

---

### 🏗️ Prompt Fixture = Test Data Factory (Mapping)

| QA Concept              | AI QA Analogy                      |
|-------------------------|------------------------------------|
| `FactoryBot` / `pytest fixtures` | `prompt fixtures` – param sets to test prompts |
| Static test data file   | JSON/CSV input set for prompt injection |
| Factory with traits     | Prompt template + trait-modified inputs |

---

### 🔨 Fixture Examples

Let’s say you’re testing this prompt:

**Prompt Template**:  
_“Summarize this report in plain English: {medical_report}”_

You can plug in a prompt fixture list like:

```json
[
  { "id": "pneumonia_case", "medical_report": "The patient presents with fever, cough, and shortness of breath..." },
  { "id": "diabetes_case", "medical_report": "The lab results indicate elevated HbA1c and fasting blood sugar..." },
  { "id": "edge_long_text", "medical_report": "..." },
  { "id": "no_findings", "medical_report": "No abnormal findings noted." }
]
```

Each fixture gets passed into the same prompt and validated with match types.

---

## ✅ Prompt Fixture Benefits

- 🔁 Test one prompt against **many realistic cases**
- 🧪 Capture edge behavior (e.g., nulls, overflow, empty strings)
- 🧩 Enable **parameterized testing** in frameworks like pytest, JUnit, or PromptLayer

---

## 🧪 Exercise – Define Prompt Fixtures

### 📘 Scenario: "Explain the function of each AI model component in a system architecture diagram"

**Prompt Template**:  
_"Describe the role of this component in an AI system: {component_description}”_

---

### ✅ User Submission (original unstructured form)

Answer:

{
  "id": "unique_id_here",
  "component_description": act as writer and share high level component purpose using 100 tokens.
  "Security_Aspect": Act as security advisor, provide the common technique used across module authentication like tokenizer and common encoding used to authenticate with external modules.
  "Common_failure":Act as QA engineer, verify each reasoning prompts and verify anywhere system returns null pointer, empty strings returnning, validation input for prompt injection, or verifying input string is valid for processing or not.
  "halusination_flows":Act as halusination engineer, verify the corssing topics that confuse the prompt and misslead information sharing as per user request. verify and update user if there is a confusion in summerising details , its ok to tell, this concept is something not write or not understood or need more inputs, use details as necessary.
  "Identify_rare_component":Verify module analysier, share the status of this component and number connections between modules, show me a number of touch points this is called using number. less the number, rare the component, more the number, is becoming more critical across model.
}

---

### ✅ Reformatted Fixture Submission

```json
[
  {
    "id": "writer_highlevel_summary",
    "component_description": "Act as writer and share high level component purpose using 100 tokens."
  },
  {
    "id": "security_auth_common",
    "component_description": "Act as security advisor, provide the common technique used across module authentication like tokenizer and common encoding used to authenticate with external modules."
  },
  {
    "id": "qa_edge_null_pointers",
    "component_description": "Act as QA engineer, verify each reasoning prompt and verify if system returns null pointer, empty strings, or fails prompt injection validation."
  },
  {
    "id": "hallucination_path_checker",
    "component_description": "Act as hallucination engineer, detect misleading topic shifts in user input and warn when summarization is confused or lacks clarity. Prompt for clarification if unsure."
  },
  {
    "id": "rare_component_mapper",
    "component_description": "Act as module analyzer, assess how often this component is used across the system. Fewer touchpoints = rare, more = critical."
  }
]
```

---

## ✅ Feedback

| Fixture ID | Evaluation |
|------------|------------|
| `writer_highlevel_summary` | ✅ Great base case – tests standard prompt use |
| `security_auth_common` | ✅ Covers domain-specific knowledge expectation |
| `qa_edge_null_pointers` | ✅ Smart choice for failure condition probing |
| `hallucination_path_checker` | ✅ Very important for open-ended clarity control |
| `rare_component_mapper` | ✅ Bonus – can be used to map frequency context in diagrams |

---

✅ **Step 5 complete**  
Next: Step 6 – Prompt Oracles = Test Oracles (LLM as Judge)

