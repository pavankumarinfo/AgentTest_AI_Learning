
# 🧠 Session 03 – Prompt Chains & Multi-Step Tasks

## 🎯 Goals
- Understand multi-step prompt design
- Use chained prompts for clarity, modularity, and reuse
- Build prompt workflows suitable for apps, agents, and tools

---

## 🔁 What Is a Prompt Chain?

A **prompt chain** is a series of prompts where:
- Each step builds on the last
- The output of one becomes the input for the next
- Steps are modular and testable

---

## ✨ Example: AI-Powered Blog Writer (Chained Version)

**Step 1 – Brainstorm Topics:**  
"List 5 blog topics about mental wellness for remote workers."

**Step 2 – Expand One Topic:**  
"Take topic #2 and outline 3 subpoints for a blog post."

**Step 3 – Write Section:**  
"Write the introduction paragraph for topic #2 using an encouraging tone."

Each step is small, focused, and testable — unlike a giant all-in-one prompt.

---

## 🤔 Why Chain Prompts?

| Benefit              | Why It Matters                                   |
|----------------------|--------------------------------------------------|
| 🎯 Better Control     | You can inspect and improve each step            |
| 🧩 More Modular       | Reuse pieces in different workflows               |
| 🧠 Clearer Reasoning  | Easier to get explanations, fix logic errors      |
| 🔧 Prepares for Agents| This is how tools like AutoGPT, LangChain work   |

---

## 🔗 Chaining Prompt Structures

| Chain Type        | Use Case Example                            |
|-------------------|---------------------------------------------|
| Reasoning Chain   | Step-by-step problem solving                |
| Generation Chain  | Create → Outline → Expand                   |
| Filtering Chain   | Generate ideas → Score them → Pick the best |
| Data Flow Chain   | Parse data → Transform → Format             |

---

## ✅ Chain 1 – Budgeting Assistant (Reasoning Chain)

### 🟩 Step 1 – Input Collection
**Prompt:**  
"Act as a budgeting assistant. Ask the user to provide their monthly income or annual salary, and list their average monthly expenses in these categories: rent, utilities, groceries, transportation, and other essential costs."

### 🟨 Step 2 – Analyze Budget
**Prompt:**  
"Based on the user’s income and listed expenses, calculate the total monthly expenses, estimate monthly savings, and provide a savings rate as a percentage. Include reasoning and calculations."

### 🟦 Step 3 – Provide Recommendations
**Prompt:**  
"From the budget analysis, provide two personalized suggestions to improve savings. For each, include a short summary and a practical example (e.g., cooking meals instead of ordering takeout)."

---

## ✅ Chain 2 – AI Travel Guide (Generation Chain)

### 🟩 Step 1 – Collect Travel Info
**Prompt:**  
"Act as a local travel expert. Ask the user for their travel destination, length of stay, reason for travel (business or holiday), and what kind of experiences they’re looking for (e.g., adventure, culture, food). Also ask about budget range and dietary preferences."

### 🟨 Step 2 – Generate Local Experiences
**Prompt:**  
"Based on the user’s input, suggest the top 3 local experiences that match their goals and budget. Include one free or low-cost option if possible. For each experience, write a short summary and why it’s worth doing."

### 🟦 Step 3 – Create Itinerary
**Prompt:**  
"Using the top recommended experience as a base, create a one-day itinerary that includes travel times, top food spots matching the user’s dietary preferences, and optional evening activities. Keep the tone light and fun."

---

## 💡 Coach Notes
- You consistently used roles, structure, and logic — excellent.
- You showed attention to user experience and real-world flow.
- Next step: format outputs (JSON, tables) and simulate tool/agent usage.

---

## 🔜 Up Next: Session 04 – Structuring AI Outputs

**Focus:** formatting structured responses for APIs, interfaces, and tools.
