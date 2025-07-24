# Session 10 
## Step 1 – Replay Memory as Semantic QA History  
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

