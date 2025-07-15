# 🧠 Prompt Engineering Cheat Sheet

# ✅ Sessions 1–3: Prompt Basics, Advanced Techniques, and Chains

---

## 📘 Session 1: Prompt Basics

### 🔹 What is a Prompt?
A prompt is the input you give to an AI model to instruct it what to do.

### 🔹 Prompt Best Practices
- **Be specific**: Clarity reduces ambiguity.
- **State the output format**: JSON, list, paragraph, etc.
- **Use role-based instructions**: "You are a legal advisor…"
- **Set constraints**: Word limits, tone, perspective.

---

### 🔹 Basic Prompt Templates
```
Explain [concept] in simple terms.
List 5 key facts about [topic].
You are a [role]. Based on the input below, perform [task].
```

---

## ⚙️ Session 2: Advanced Prompt Techniques

### 🔹 Techniques for Better Prompts
| Technique | Description | Example |
|----------|-------------|---------|
| **Few-shot prompting** | Provide examples | “Classify: ‘This is great!’ → Positive” |
| **Zero-shot prompting** | No examples | “Classify sentiment: ‘I hate this.’” |
| **Chain-of-thought** | Ask the model to reason step-by-step | “Think step-by-step: Why is the sky blue?” |
| **Self-reflection** | Ask model to critique/improve its answer | “Now improve your answer with 3 more ideas.” |

---

### 🔹 Prompt Refinement Tips
- Add sample inputs/outputs
- Break complex tasks into smaller ones
- Use delimiters like triple quotes for long inputs (e.g., '''text''')
- Avoid vague instructions like "Be creative" unless intentional

---

## 🔗 Session 3: Prompt Chains & Modular Design

### 🔹 What Are Prompt Chains?
A sequence of prompts where the output of one becomes the input of the next.

### 🔹 Benefits of Prompt Chaining
- Handle complex tasks
- Improve accuracy and formatting
- Add modularity and control

---

### 🧱 Common Chain Patterns
| Step | Role | Function |
|------|------|----------|
| 1 | Extractor | Pull key facts from raw input |
| 2 | Transformer | Convert to desired tone/format |
| 3 | Composer | Generate final output (e.g., report, email) |

---

### 🔹 Example Chain Flow
```
Step 1: Extract data from user input (as JSON)
Step 2: Rewrite it in a formal tone
Step 3: Generate a formatted letter/email
```

---

## 🧰 Pro Tips
- Test each step separately before chaining
- Use consistent formats between steps
- Store prompts in version control
- Document edge cases

---

Let me know if you'd like a visual prompt map, LangChain version, or production API design next!

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


# ✅ Sessions 5 & 6: Use Cases & Architectures

---

## 🧩 Session 5: Real-World Use Cases for Prompting

### 🔹 Common Use Case Categories
| Category | Description | Example Prompt Function |
|----------|-------------|--------------------------|
| **Summarization** | Condense large inputs | "Summarize this PDF in 5 bullet points." |
| **Extraction** | Pull structured info from text | "Extract patient name, diagnosis, treatment from this clinical note." |
| **Classification** | Assign labels or tags | "Classify this feedback as positive, neutral, or negative." |
| **Transformation** | Convert format or tone | "Rewrite this email in a professional tone." |
| **Generation** | Create new content | "Write a JIRA ticket based on this bug report." |
| **Reasoning** | Provide explanation or logic | "Explain why this treatment is medically necessary." |

---

### 🔹 Examples of Real-World Prompts
\`\`\`text
Transform: "Convert these bullet points into a LinkedIn post."
Summarize: "Summarize this contract into key obligations."
Classify: "Is this email urgent, important, or informational?"
Extract: "From the given resume, extract education, skills, and work experience as JSON."
\`\`\`

---

## 🏗️ Session 6: Prompt-Driven Architectures

### 🎯 What Is a Prompt Pipeline?
A chain of prompts that act as logical blocks — each step:
- Accepts input
- Applies transformation/classification
- Produces output for the next step

---

### 🔹 Typical 3-Step Prompt Pipeline
| Step | Prompt Role | Description | Output |
|------|-------------|-------------|--------|
| 1 | Extractor | Extract structured data | JSON |
| 2 | Transformer | Generate insights or rewrite | Natural language |
| 3 | Composer | Create formatted output | Email, Letter, Report, etc. |

---

### 🧱 Prompt Architecture Design Steps
1. **Define Domain & Use Case** (e.g., QA, Cybersecurity, HealthTech)
2. **Break Down Workflow** into stages
3. **Assign Prompt Role** (Extract, Summarize, Transform, Compose)
4. **Design Prompt Templates** (Reusable, parameterized)
5. **Test Outputs and Tune Iteratively**

---

### 💡 Prompt Template Patterns
\`\`\`text
"You are a [role/persona]. Based on the input below, perform [task]."
"Input: {input_data}"
"Output:"
\`\`\`

---

## 🔄 Scaling with LangChain / crewAI

| Tool | Role | Use |
|------|------|-----|
| **LangChain** | Chains + Memory + Tools | Automate workflows end-to-end |
| **crewAI** | Agent Collaboration | Assign roles like Extractor, Rewriter, Validator |
| **Vector Store** | Add knowledge context | Retrieve insurance rules, JIRA docs, SOPs |

---

## 🧰 Pro Tips
- **Design prompts like functions** — clear inputs, outputs
- **Avoid overloading a single prompt** — split into steps
- **Include instructions + formatting expectations**
- **Add example outputs when possible** to guide the model
- **Use role-play and personas** for domain-specific outputs
