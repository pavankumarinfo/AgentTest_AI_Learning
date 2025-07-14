
# 🧠 AI Prompt Engineering – Session 05: Real-World Use Cases for Prompting

## ✅ Session Objectives
- Map AI prompting to real product and business workflows.
- Design prompt-based microtools and agents for real-world utility.
- Apply prompting inside reusable functions and agent workflows.

---

## 🔍 The 3 Layers of Real-World AI Prompt Use

| Layer | Description | Example |
|-------|-------------|---------|
| Input Layer | Collects structured/unstructured user input | Chat form, form-to-prompt |
| Prompt Logic Layer | Executes reasoning, transformation, decision logic | Prompt templates, chains, tools |
| Output Integration Layer | Converts AI output into business action | UI updates, API calls, automation |

---

## 🧠 4 Core Real-World Prompt Use Cases

### 1. Decision Assistants
Helps humans make better/faster decisions.

**Prompt Template**:
```
You are a {domain} expert. Given {input}, recommend the best course of action with pros/cons and a confidence score.
```

---

## ✅ Exercise 1 – Security QA Prompt

**Your Prompt Question**:
> Write a prompt for security engineer, by reviewing the security issues listed and share the details of this security issue and its confidence score to determine is security issue.

**Refined Prompt**:
```
You are a Security QA expert with 10+ years of experience in application security, vulnerability triage, and risk classification.

Review the following reported security issue:

{security_issue_description}

Analyze the issue based on known vulnerability patterns, severity (e.g., OWASP Top 10), context provided, and the likelihood of exploit.

Respond with the following:
1. Summary
2. Classification
3. Risk Level
4. Confidence Score
5. Suggested Next Steps
```

**Input**:
```
The login endpoint does not enforce rate limiting. A user was able to submit 500 login attempts per minute and received error messages for failed logins, indicating account validity.
```

**Output**:
```markdown
**Summary**: The login API lacks rate limiting, allowing attackers to brute-force login attempts. Error responses leak account validity.

**Classification**: Brute Force / Authentication Misconfiguration

**Risk Level**: High – This vulnerability could allow account takeover with credential stuffing.

**Confidence Score**: 92

**Suggested Next Steps**: Escalate to Security Team for immediate mitigation. Implement rate-limiting and generic error messages.
```

---

## ✅ Exercise 2 – Test Plan Transformer

**Your Prompt Question**:
> Transform the given test plan with all the tickets of different priority and servority. classify them with different modules affected and share the summary in an json or csv file format with showing of {test name},{test case description},{priority},{severity},{module}. the severity is test case serverity (low, medium, high, and critical) and similar lines for priority.

**Refined Prompt**:
```
You are a QA Automation Lead with expertise in release risk assessment and structured test planning.

Transform the following test plan into a structured summary. Your output should be in either JSON or CSV format with the following fields:

- test_name  
- test_case_description  
- priority (low, medium, high, critical)  
- severity (low, medium, high, critical)  
- module  

Instructions:
- Parse and classify the test cases correctly by module.
- Derive missing priority or severity using test impact and failure effect.
- If a test affects multiple modules, list all relevant modules.
```

**Input**:
```
1. Verify login fails after 5 wrong attempts – should lock the user. Affects auth service.
2. Test image upload fails with unsupported format – affects media module. Medium priority.
3. Checkout flow skips payment step on Safari. High severity.
4. Test if email validation works during signup. Affects auth and notifications.
5. Confirm order summary calculation handles discount logic.
```

**Output (CSV)**:
```csv
test_name,test_case_description,priority,severity,module
Login Lockout,Verify login fails after 5 wrong attempts,high,high,auth
Image Format Upload Error,Test image upload fails with unsupported format,medium,medium,media
Safari Checkout Bug,Checkout flow skips payment step on Safari,high,high,checkout
Signup Email Validation,Test if email validation works during signup,medium,medium,auth;notifications
Discount Calculation Test,Confirm order summary calculation handles discount logic,medium,medium,checkout
```

---

## ✅ Exercise 3 – JIRA Ticket Assistant

**Your Prompt Question**:
> Act as AI agent assistant, review the process of creating JIRA bug ticket to help user. As step-by-step details of bug to fill different details for Jira ticket as follows...

**Refined Prompt**:
```
You are an AI assistant that helps users create detailed and high-quality JIRA bug tickets. 
Ask the user for each required field step-by-step, then summarize the ticket and confirm submission.

Steps:
1. Title
2. Description: version, environment, steps, expected, actual, attachments
3. Priority
4. Severity
5. Final summary and confirmation
```

**Example Input (conversation)**:
- Title: Uploading images fails with “Unsupported file type” error  
- Version: v2.3.1  
- Env: Staging  
- Steps: Go to Profile → Upload → Select `.webp`  
- Expected: Should allow `.webp`  
- Actual: Error shown  
- Priority: Medium  
- Severity: High

**Summary Output**:
```
Title: Uploading images fails with “Unsupported file type” error
Description: On v2.3.1 in Staging, uploading `.webp` causes a failure.
Expected: Upload should succeed
Actual: Error shown
Priority: Medium
Severity: High
```

---

## ✅ Exercise 4 – Freelance Onboarding Bot

**Your Prompt Question**:
> Act as AI Assistant for a freelance works and helping in onboarding new new clients to the company. Guide the clients by step-by-step to gather below information:
{Client name} : request for full client name, email, location, contact information
{Client location} : ask client location details to make sure, required remote member or onsite.
{Task summary} : request for task that is required to complete. Once task is provided, ask them to rephrase their request to transform this to functional message, if they say yes, transform and get confirmation of the summary is correct. do this until the client is comfortable.
{duration to finish}: request no of days, date to be completed.
{price/rate}: get an estimate number that they are willing to provide. Provide them, will review this numbers and drop an email from finiance team. 
{anyspecial skill looking}: check with client needs any special tools, software, skills looking.
{team size}: ask for team size they are looking to complete this job and they need team onsite, or remote and also check any inside country, or outof country.
At the end, ask client do they have any other questions or details looking. 
Once done, share summary of job and send them an acknowledgment email with an freelance job id and quick summary (not too detailed).
Once the above information is collected, tramsform this information into excel, csv, to share summary to management with all list of tasks, clientnames, timeline, costs, team size and priority levels and provide details based on priority as sort.


**Refined Prompt**:
```
You are an AI assistant responsible for onboarding new freelance clients. Guide the client step-by-step and collect all required information to initiate a project request.

Start the conversation in a friendly and professional tone.

---

**Step 1: Client Information**  
"Welcome! Let's get started with some basic information:  
• What is your full name?  
• Your email address?  
• Your current location?  
• A phone number or WhatsApp contact?"

---

**Step 2: Project Location Context**  
"Is this project intended for:  
- Onsite work  
- Remote work  
- Or a hybrid model?"  
(Also confirm if the team needs to be in a specific region or country.)

---

**Step 3: Task Summary**  
"What task or problem would you like our freelance team to help you with?"

After receiving the task, continue:

🧠 "Would you like me to rephrase this into a more functional statement for clarity? (Yes/No)"

If **Yes**:  
• Suggest a rephrased version  
• Ask: “Does this summary sound right to you?”  
Repeat until client confirms.

---

**Step 4: Timeline**  
"When would you like this work to be completed?  
• How many days do you estimate?  
• What’s the latest acceptable delivery date?"

---

**Step 5: Budget Estimate**  
"Do you have a budget or rate range in mind for this task? (Daily/Fixed)  
I’ll share this with our finance team for review."

---

**Step 6: Special Skills or Tools**  
"Are there any specific tools, software, languages, or certifications you’re looking for in the team?"

---

**Step 7: Team Requirements**  
"How many people do you need for this task?  
Do you prefer the team to be:  
• Fully remote  
• Fully onsite  
• Mixed?  
Also, should the team be:  
• Based in your country  
• Or can they work from abroad?"

---

**Step 8: Final Check**  
"Do you have any other requirements, details, or questions before we proceed?"

---

### 📋 Summary Acknowledgment

"Thank you! Here is a brief summary of your project request:

• **Client**: {client_name}, {email}, {location}  
• **Project Type**: {task_summary}  
• **Timeline**: {duration}, Target Date: {date}  
• **Budget**: {budget}  
• **Team Size**: {team_size}, Location Preference: {team_location}  
• **Special Skills**: {skills}  
• **Freelance Job ID**: FL-{autogenerated_id}

We’ll send an official acknowledgment email with the job ID and next steps shortly."

---

### 🧾 Output Format (CSV or Excel)

Once onboarding is complete, auto-transform the collected data into structured format for tracking and prioritization.

#### **Fields**:
- client_name  
- email  
- location  
- task_summary  
- final_functional_summary  
- days_required  
- target_date  
- budget_estimate  
- special_skills  
- team_size  
- team_location_pref  
- job_id  
- priority_level *(auto-tagged or manual)*

📤 The final file can be exported as `.csv` or `.xlsx` for internal management review.

🔽 **Sorting Suggestion**:  
Sort by `priority_level` (High to Low), then `target_date` (nearest first).

---

### 🛠️ Agent Enhancements (Optional)

- Auto-detect **priority** based on budget/timeline complexity  
- Auto-assign **job ID** with client initials + timestamp  
- Integrate with **email/SMS API** for real-time acknowledgment  

---

Would you like me to:
- Build this as a **Streamlit app or chatbot prototype**?
- Provide a **Jupyter Notebook version** for testing?
- Move to **Session 06: Prompt-Driven Product Architectures**?

Let’s keep your freelance AI toolkit growing!

```

**Example Output (JSON)**: this output need to redefined again.
```json
{
  "client_name": "Aarti Sharma",
  "email": "aarti@example.com",
  "location": "Dubai, UAE",
  "contact": "+971-50-1234567",
  "task_summary": "Build internal portal",
  "functional_summary": "Design and develop internal web portal with dashboard and secure login",
  "days_required": 15,
  "target_date": "2025-07-31",
  "budget_estimate": "$2500",
  "special_skills": "React, Flask, Tailwind",
  "team_size": 2,
  "team_location_pref": "Remote",
  "priority_level": "Pending Review",
  "job_id": "FL-8DH3KF2A"
}
```

---

## 🔁 Prompt Chain Expansion Ideas
- Extract → Classify → Summarize
- Chain prompts to guide step-by-step workflows
- Make each step testable or reusable

---

## 📦 Output Formats
Use `JSON`, `CSV`, or display via chatbot or app UI.

---

## 🔮 Coming Next: Session 06 – Prompt-Driven Product Architectures
Learn how prompts integrate with APIs, agents, and multi-step tools to build entire AI systems.
