## 🧠 Cheatsheet – Session 10: Semantic QA Memory (with Examples)

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

Next up: **Memory Indexing + Embedding Support**
