# Session 10 

# Session 10 Plan – Replay Memory as Semantic QA History  
📌 This file outlines the training plan, steps, and learning outcomes for Session 10 of your AI QA Copilot training.

---

## 🎯 Goal

Convert structured test logs into **searchable, queryable memory** that QA agents can reason over.

---

## ✅ Step-by-Step Plan

### 🔹 Step 1 – Add Semantic Context ✅ *(Completed)*  
Add the following fields to your replay memory:
- `intent_description`
- `semantic_tags`
- `linked_failures`
- `fix_version`
- `failure_history`  
👉 These turn each test into a **knowledge-rich memory entry**

---

### 🔹 Step 2 – Memory Indexing + Embedding Support  
- Encode intent, prompts, and output into **vector form**
- Index logs in a semantic vector store (e.g. FAISS, Chroma)
- Support natural language queries like:
  - _“Show me all expiry-related tests that failed in 2.0.x”_
  - _“What fixed the reset-link issue?”_

---

### 🔹 Step 3 – Search & Inference  
Build a prototype semantic search across your memory:
- Filter by test intent, tags, or fix version
- Enable QA agent to find past failures and correlate fixes

---

### 🔹 Step 4 – Memory-Aware Prompt Chain (Optional Advanced)  
Chain prompts like:
- Retrieve failure memory
- Compare current output
- Ask agent to explain failure reason or fix from memory

---

## 🧠 Learning Outcomes

By the end of this session, you'll be able to:

| Skill | Description |
|-------|-------------|
| **Replay QA Search** | Search test cases by tag, issue, or intent |
| **Memory Embedding** | Encode logs into semantic vectors |
| **Failure Lineage** | Track issues across versions semantically |
| **Agent-Aware History** | Enable QA agent to reason using memory |

---

# Step 1 – Replay Memory as Semantic QA History  
📌 This file contains raw, unedited training content including full prompts, inputs, outputs, and feedback.

---

## 🎯 Step 1 Objective

Learn how to structure replay memory for **semantic lookups**:
- What was the last known issue?
- When was it fixed?
- How did verdicts change across versions?

Extend replay logs with intent descriptions, tags, fix metadata, and history.

---

## 🧱 Key Concepts

| Concept | Meaning |
|--------|---------|
| `intent_description` | Explanation of what the test case is validating |
| `semantic_tags` | Thematic tags like `auth`, `security`, `usability` |
| `linked_failures` | Other test_ids with similar failure or intent |
| `fix_version` | Version where issue was first resolved |
| `failure_history` | Ordered verdicts across LLM versions |

---

## 🧪 Exercise – Semantic Memory Extension

We collaborated field by field using the previous test case: `test_id: 02-reset-link-expiry`

---

### 🧾 Field 1: intent_description

**Prompted Draft:**  
> "Validates that the reset password link expires correctly after the defined expiration period."

✅ **User accepted**

---

### 🧾 Field 2: semantic_tags

**Suggested Tags:**  
> `["auth", "expiry", "email", "security"]`  
✅ **User accepted**

---

### 🧾 Field 3: linked_failures

**User input:** "I don't remember ids"  
✅ AI filled in:

```json
["01-reset-invalid-token", "03-reset-link-expired-assertion"]
```

---

### 🧾 Field 4: fix_version

✅ Derived from earlier replay log:
```json
"fix_version": "v2.0.1"
```

---

### 🧾 Field 5: failure_history

✅ Created from existing version verdicts:
```json
[
  {"version": "v2.0.0", "verdict": "FAIL"},
  {"version": "v2.0.1", "verdict": "PASS"}
]
```

---

### ✅ Final Semantic Memory Block:

```json
{
  "intent_description": "Validates that the reset password link expires correctly after the defined expiration period.",
  "semantic_tags": ["auth", "expiry", "email", "security"],
  "linked_failures": [
    "01-reset-invalid-token",
    "03-reset-link-expired-assertion"
  ],
  "fix_version": "v2.0.1",
  "failure_history": [
    {"version": "v2.0.0", "verdict": "FAIL"},
    {"version": "v2.0.1", "verdict": "PASS"}
  ]
}
```

