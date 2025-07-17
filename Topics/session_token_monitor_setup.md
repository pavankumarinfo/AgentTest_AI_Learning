## ✅ Instructions for ChatGPT

When this instruction is active, you must:

1. Monitor session token usage.
2. When tokens drop below **100 remaining**, immediately:
   - ⚠️ Alert the user: “Tokens are running low”
   - Ask: “Do you want to continue in a new session?”
   - Provide a reusable memory prompt for continuation.

---

## 🧪 Reusable Prompt to Enable Token Monitoring

Use this at the start of any long session:

````markdown
## 🧠 Session Setup Prompt: Enable Token Limit Alert & Continuation

For this session, please monitor the token usage.

🔔 When we are nearing 100 tokens left in the current session:
1. Alert me: “⚠️ Tokens are running low”
2. Ask: “Do you want to continue in a new session?”
3. Provide the exact continuation memory prompt I should copy/paste into the new session to resume seamlessly from where we stopped.

This applies to all exercises, markdown logs, and structured training sessions. Please do not auto-end without checking with me first.
````

---

## 📅 Activated On

2025-07-17

This setting applies to all future deep-dive QA sessions and structured prompt engineering work related to AgentTest – AI QA Copilot.
