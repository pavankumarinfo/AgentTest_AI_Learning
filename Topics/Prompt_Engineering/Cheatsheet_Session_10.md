## 🧠 Cheatsheet – Session 10 - Step 1 : Semantic QA Memory (with Examples)

| Field | Purpose | Example |
|-------|---------|---------|
| `intent_description` | Human-readable test goal | `"Validates that the reset password link expires correctly after the defined expiration period."` |
| `semantic_tags` | Topics or system areas | `["auth", "expiry", "security"]` |
| `linked_failures` | Past related failures or overlapping tests | `["01-reset-invalid-token", "03-reset-link-expired-assertion"]` |
| `fix_version` | When it started passing | `"v2.0.1"` |
| `failure_history` | Audit trail of verdicts across LLM versions | `[{"version": "v2.0.0", "verdict": "FAIL"}, {"version": "v2.0.1", "verdict": "PASS"}]` |

---

You now have a memory structure ready for:
- Semantic version comparison
- Historical test impact reporting
- Agent learning over test logs

---

# Cheatsheet – Session 10 Step 2: Embedding & Indexing  
📌 This file contains the summarized key terms and examples for quick reference.

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

