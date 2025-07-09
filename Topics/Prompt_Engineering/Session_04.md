# 🧠 AI Prompt Engineering - Session 04: Structuring AI Outputs

This session teaches how to design AI prompts that result in **clear, consistent, and structured outputs**. Ideal for use in multi-step workflows, freelance product design, agent chaining, and real-world tools.

---

## 🎯 Objective

Design prompts that guide the AI to generate outputs in structured formats such as JSON, Markdown, HTML, or tables, making them reusable and machine-readable.

---

## 📚 Key Concepts

### 1. Output Format Control

- Specify formats: JSON, Markdown, HTML, YAML, etc.
- Use instructions like:
  - `Respond only with valid JSON.`
  - `Use GitHub-flavored Markdown.`
  - `Return output in HTML format.`

### 2. Field-Level Instructions

Give detailed instructions for each field in the output. Example:

```text
{
  "title": "Short name of the feature",
  "description": "2–3 sentences max",
  "target_users": ["type1", "type2"],
  "value_proposition": "Short benefit summary",
  "implementation_notes": "High-level dev guidance"
}
```

### 3. Schema-Based Prompts

Embed schemas directly in your prompt to guide the structure. Example:

```json
{
  "id": "number",
  "name": "string",
  "actions": ["string"]
}
```

### 4. Guardrails via Prompt Constraints

Use constraints like:
- Max sentence/word count
- Strict key naming (e.g., camelCase)
- “No explanations or commentary outside the object”

---

## 🧪 Exercises

### 🔹 4.1 Structured Output Prompting

Create a prompt to generate product feature specs in JSON with:
- title
- description
- target_users
- value_proposition
- implementation_notes

### 🔹 4.2 Enforcing Format Reliably

Techniques:
- Use fenced code blocks (```json)
- Remove all commentary
- Say “valid, parseable JSON only”
- Use “format-first” phrasing

### 🔹 4.3 Designing Templates for Reuse

Structure prompts using:
- Parameterized variables like `{{feature}}`, `{{app_type}}`
- Consistent field types and schemas
- Modular sections for reuse across tools or clients

### 🔹 4.4 Structured Responses for Multi-Agent Workflows

Chain prompts for:
1. JSON spec generation
2. Marketing copy generation
3. UI schema generation

Use predictable fields, clear keys, and routing metadata like:
```json
"nextAgent": "uiWriter"
```

### 🔹 4.5 Debugging Messy Outputs

Common fixes:
- Invalid JSON? ➝ enforce fencing and use `JSON.parse()` validation
- Wrong keys? ➝ enforce camelCase and schema samples
- Commentary? ➝ "No extra text. JSON only."
- Missing fields? ➝ define all fields as required in schema

---

## 🧰 Tips

- Use temperature=0 for deterministic structure
- Validate outputs with tools like [jsonlint.com](https://jsonlint.com)
- Design for agents, not just humans

---

## ✅ End of Session 04

You’ve learned to produce **well-structured, reliable outputs** that plug into any downstream AI agent or app with confidence.
---

## 🧪 Exercises with Examples & Learnings

---

### 🔹 4.1 Structured Output Prompting

**Prompt:**
```
Act as a Product Feature Specialist.

Generate a product feature specification in strict JSON format with:
- title: concise name (max 50 characters)
- description: 2–3 sentence explanation
- target_users: who benefits from the feature
- value_proposition: how it adds value
- implementation_notes: high-level tech notes
Respond with JSON only. No extra text.
```

**Output:**
```json
{
  "title": "Daily Symptom Tracker",
  "description": "Allows cancer patients to log daily symptoms. Doctors can monitor trends for early intervention.",
  "target_users": ["Patients", "Oncologists", "Care coordinators"],
  "value_proposition": "Enables early detection and better outcomes through real-time monitoring.",
  "implementation_notes": "Uses mobile inputs stored in FHIR-compliant format with alert notifications."
}
```

**Learnings:**
- JSON formatting is clear, strict, and reusable.
- Role + format + structure = consistent outputs.

---

### 🔹 4.2 Enforcing Format Reliably

**Prompt:**
```
Generate a Markdown card with:
- bold title
- 2–3 sentence paragraph description
- 3 bullet points (user types)
- blockquote (value prop)
- italicized implementation note
Only return Markdown.
```

**Output:**
```markdown
**Daily Symptom Tracker**

Enables daily symptom logging by cancer patients. Doctors receive real-time alerts for severe trends.

- Patients
- Oncologists
- Nurses

> Enables proactive care through timely data.

*Integrates mobile logging with FHIR backend and notifications.*
```

**Learnings:**
- Markdown is a readable format for UI and copy teams.
- Layout structure matches AI card/agent use cases.

---

### 🔹 4.3 Designing Templates for Reuse

**Prompt Template:**
```
Act as a Product Designer.

Generate JSON with:
- title: "{{feature_name}} in {{app_type}}"
- description: How it helps {{domain}}
- value_proposition: Benefits to {{users}}
- implementation_notes: Top 3 points for {{audience}}
Respond with JSON only.
```

**Learnings:**
- Parameterization makes prompts reusable across clients and tools.
- Great for libraries and prompt chaining.

---

### 🔹 4.4 Multi-Agent Workflow Prompt

**Flow:**
1. JSON Spec ➝ 2. Markdown Copy ➝ 3. UI Schema

**Input JSON:**
```json
{
  "featureId": 101,
  "title": "Symptom Tracker",
  "description": "Lets patients log symptoms. Doctors view trends.",
  "users": "patients, doctors, coordinators",
  "audience": "oncology professionals"
}
```

**Marketing Markdown Output:**
```markdown
***Symptom Tracker***

Track fatigue, nausea, and pain. Real-time insights give doctors a clearer view of patient progress.
```

**UI Component Output:**
- Dropdown for symptoms
- Slider for intensity
- Calendar for date
- Multi-line notes

**Learnings:**
- Clean structure enables easy routing across agents.
- Perfect for use in AutoGen or LangGraph.

---

### 🔹 4.5 Debugging Messy Output

**Broken Output:**
```
Sure! Here's your JSON:
{
  "Title": "Tracker",
  "Desc": "logs stuff",
// to be continued
}
```

**Prompt to Fix:**
```
Act as Product Designer & Technical Assistant.

Clean and reformat to:
- camelCase keys
- string/array types
- no comments
- valid JSON only
Add a comment above JSON to describe what it is.
Ask questions if anything's unclear before you clean.
```

**Fixed Output:**
```json
// Feature spec for cancer tracking tool
{
  "title": "Tracker",
  "description": "Logs symptoms for doctors to review.",
  "users": ["Patients", "Doctors"]
}
```

**Learnings:**
- Fence + structure = parseable output
- Validation guardrails improve reliability
