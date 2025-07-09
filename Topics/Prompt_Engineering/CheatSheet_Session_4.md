# 📌 Session 04 Cheatsheet: Structuring AI Outputs

## 🛠 Output Format Types
- JSON
- Markdown
- HTML
- YAML
- Tables

## 📦 Field-Level Pattern
```json
{
  "title": "string",
  "description": "2-3 sentences",
  "target_users": ["User1", "User2"],
  "value_proposition": "Short summary",
  "implementation_notes": "High-level dev notes"
}
```

## 🔐 Guardrails
- Use fenced code blocks: ```json
- Enforce camelCase keys
- Say: “Respond only with valid JSON.”
- Disallow extra text or explanations

## 🔄 Prompt Reuse Pattern
```text
Act as a {{role}}. Generate a {{format}} with:
- title: {{feature}}
- description: {{value}}
- target_users: {{list of users}}
```

## 🔗 Multi-Agent Output Fields
```json
{
  "featureId": 1,
  "title": "string",
  "summary_for_writer": "Use this for hero section",
  "nextAgent": "uiWriter"
}
```

## 🐞 Debug Checklist
- ❌ Invalid format ➝ Use fenced code
- ❗Wrong keys ➝ Match schema
- 💬 Extra commentary ➝ Remove
- 🧩 Partial fields ➝ Specify all in schema

---
✅ Use temperature=0 for deterministic format.
✅ Validate JSON with JSON.parse or jsonlint.com
---

## 🧪 Common Exercise Patterns

### 🔹 JSON Feature Spec
```json
{
  "title": "string",
  "description": "2-3 sentences",
  "target_users": ["User1", "User2"],
  "value_proposition": "Short benefit",
  "implementation_notes": "Tech insight"
}
```

### 🔹 Markdown Feature Card
```markdown
**Feature Title**

Short paragraph describing the feature.

- User Type 1
- User Type 2

> Value proposition here

*Implementation notes here*
```

### 🔹 Debug Fix Pattern
Broken:
```json
{
  "Title": "Example",
  "Desc": "Unclear",
// unfinished
}
```

Fix Prompt:
> “Clean and reformat into valid JSON with camelCase keys, no comments, and correct types.”

---

## ✅ Chain Output Handoff Example

**Step 1** – JSON Output
```json
{
  "title": "Symptom Tracker",
  "description": "Logs symptoms for doctors."
}
```

**Step 2** – Markdown for Marketing
```markdown
***Symptom Tracker***

Track fatigue, pain, nausea. Real-time doctor alerts and summaries.
```

**Step 3** – UI Design Notes
- Dropdown (symptoms)
- Slider (intensity)
- Date (calendar)
- Notes (multiline)
