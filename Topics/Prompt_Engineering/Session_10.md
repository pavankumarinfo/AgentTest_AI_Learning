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

# Session 10 – Step 2: Memory Indexing + Embedding Support  
📌 This file contains raw, unedited training content including full prompts, inputs, outputs, and feedback.

---

## 🎯 Objective

Prepare replay memory entries for semantic search by:
- Creating embedding vectors from key fields
- Indexing memory into a vector database
- Supporting natural language queries

---

## 🧱 Embedding Fields Selected

| Field | Included | Reason |
|-------|----------|--------|
| `intent_description` | ✅ | Core meaning of the test |
| `prompt` | ✅ | Often contains testing logic |
| `semantic_tags` | ✅ | Helps topical grouping |
| `fix_version` | ✅ | Tracks when issues are resolved |
| `failure_history` | ✅ | Time-series of verdicts, flattened for context |

---

## 🧾 User-Provided Embedding Input

```txt
Test Intent: The test intent is to make sure this is verified with new software version v2.0.1  
Prompt: Act as AI test engineer, make sure this test is recorded with v2.0.1 is passed and have history tracking of preivous and future version releases.  
Tags: security, regression, smoketest  
Fix Version: v2.0.1  
Failure History: v2.0.0 = Fail, v2.0.1 = Pass
```

---

## 🧠 Embedding Simulation

**Model Used:** `all-MiniLM-L6-v2`  
**Vector Dimensions:** 384  
**Simulated Output:**
```json
{
  "embedding_model": "all-MiniLM-L6-v2",
  "dimensions": 384,
  "vector_sample": [0.021, -0.108, 0.056, ..., 0.003]
}
```

---

## 💾 Vector Indexing Options

| Tool | Type | Notes |
|------|------|-------|
| FAISS | Local | Lightweight, fast |
| Chroma | Local API | Python-native, simple |
| Weaviate, Pinecone | Cloud | Full-featured but require credentials |

### Sample: Add to Chroma

```python
import chromadb
client = chromadb.Client()
collection = client.create_collection(name="test_logs")

collection.add(
  documents=[your_input_string],
  embeddings=[embedding_vector],
  metadatas=[{"test_id": "02-reset-link-expiry"}],
  ids=["log_001"]
)
```

---

## 🔍 Example Semantic Queries

### 1. _“Show me all tests fixed in v2.0.1”_
- Embed query
- Search `fix_version` and `intent_description` fields

### 2. _“Find tests related to expiry or auth that failed last version”_
- Filter by tags
- Check `failure_history` for latest verdict = FAIL

### 3. _“What was the last known failure similar to reset link issue?”_
- Embed phrase
- Search across `intent_description` + `prompt`

---

## 🧠 Cheatsheet – Step 2: Embedding & Indexing (with Examples)

| Term | Meaning | Example |
|------|---------|---------|
| `Embedding` | Vector representing text meaning | `[0.013, -0.022, ..., 0.045]` |
| `Vector Index` | Database of embeddings for similarity search | `Chroma`, `FAISS` |
| `Embedding Fields` | Which parts of memory are encoded | `"intent_description"`, `"prompt"`, `"tags"` |
| `Semantic Query` | Query that searches by meaning | `"tests failing in expiry flow"` |
| `Failure History` | Time-stamped verdicts | `{"v2.0.0": "FAIL", "v2.0.1": "PASS"}` |

---

You are now ready for **Step 3: Search & Inference** — building logic to query this vector memory with natural language.


---

## 🗒️ Full Training Dialogue – Step 2

### 🧠 Objective Recap
Build support for:
- Embedding replay memory using sentence transformers or OpenAI APIs
- Indexing logs in a vector DB (Chroma, FAISS)
- Searching logs with natural queries

---

### 🧾 Initial Field Inclusion Plan

| Field | Include? | Reason |
|-------|----------|--------|
| `intent_description` | ✅ | Core to test’s meaning |
| `prompt` | ✅ | Contains test logic |
| `semantic_tags` | ✅ | Groups tests by type |
| `current_llm_output` | ❌ | Optional |
| `fix_version` | ❌ (initially) | Not semantically relevant |
| `failure_history` | ❌ (initially) | Not semantic text |

---

### 🧾 User Change Request

User requested to include:
- `fix_version`
- `failure_history`

✅ Plan updated to embed:
- `intent_description`
- `prompt`
- `semantic_tags`
- `fix_version`
- `failure_history`

---

### 📝 User Submission – Embedding Input

```txt
Test Intent: The test intent is to make sure this is verified with new software version v2.0.1  
Prompt: Act as AI test engineer, make sure this test is recorded with v2.0.1 is passed and have history tracking of preivous and future version releases.  
Tags: security, regression, smoketest  
Fix Version: v2.0.1  
Failure History: v2.0.0 = Fail, v2.0.1 = Pass
```

---

### 🤖 Embedding Simulation

Model: `all-MiniLM-L6-v2`  
Output: `[0.021, -0.108, ..., 0.003]`  
Vector length: 384-dim

---

### 🗃️ Indexing Sample Code (Chroma)

```python
import chromadb
client = chromadb.Client()
collection = client.create_collection(name="test_logs")

collection.add(
  documents=[your_input_string],
  embeddings=[embedding_vector],
  metadatas=[{"test_id": "02-reset-link-expiry"}],
  ids=["log_001"]
)
```

---

### 🧠 Query Examples

1. "Show me all tests fixed in v2.0.1" → match `fix_version`
2. "Find tests related to expiry/auth that failed last version" → tag + verdict logic
3. "Last failure like reset link issue" → cosine similarity of `intent_description`

---

