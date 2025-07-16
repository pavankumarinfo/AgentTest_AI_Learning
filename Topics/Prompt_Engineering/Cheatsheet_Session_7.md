## Session 07 Cheat Sheet: Testing LLM Agents

### 🔍 Prompt Design
- Use assertive tones: "Only respond with…", "Always cite…"
- Include constraints: token length, response format, source validation

### ⚔️ Adversarial Techniques
- Feed ambiguous or misleading inputs
- Use inverted assumptions ("The answer is X — explain why")
- Reword to trick the model

### 🚫 Negative Testing
- Supply obviously false premises
- Expect graceful refusal, not confident hallucination

### 🔁 Self-Consistency
- Run the same prompt multiple times
- Look for logical or factual drift

### 🧪 Evaluation Metrics
- Accuracy
- Consistency
- Safety (no hallucination)
- Robustness to trick inputs

