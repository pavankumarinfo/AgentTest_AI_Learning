
# Session 09 – Step 1: Prompt Evaluation Metrics ↔ QA KPIs

**Date**: 2025-07-21  
**Product**: AgentTest – AI QA Copilot  
**Session**: Prompt Evaluation Metrics ↔ QA KPIs

---

## ✅ Step 1: Define QA KPIs in Classical Testing

| QA KPI              | Meaning |
|---------------------|---------|
| **Accuracy**         | % of total predictions that are correct |
| **Precision**        | % of true positives out of all predicted positives |
| **Recall**           | % of true positives out of all actual positives |
| **False Positives**  | Output marked as correct but is actually wrong |
| **False Negatives**  | Correct output missed or marked incorrect |
| **Test Coverage**    | % of code or behavior space tested |
| **Robustness**       | Stability under edge cases or noisy inputs |
| **Time to Feedback** | Time to detect, log, and respond to failures |

---

## ✅ Step 2: Mapping to AI Prompting Metrics

| QA KPI           | AI QA Equivalent |
|------------------|------------------|
| **Accuracy**      | % of LLM outputs that pass match-type assertion |
| **Precision**     | % of outputs marked “correct” that actually are |
| **Recall**        | % of all relevant outputs the prompt actually produces |
| **False Positives** | Hallucinated answers or wrongly accepted outputs |
| **False Negatives** | Good answers marked as wrong due to poor assertions |
| **Coverage**      | Prompt Coverage (Step 4) |
| **Robustness**    | Performance consistency across rephrasings, tokens, typos |
| **Time to Feedback** | How quickly test signals can be evaluated or logged |

---

## 🧪 Exercise – Map These 3 AI Test Cases to QA KPIs

### Test Case 1:
> Prompt: “List 3 cancer types with high survival rates.”  
> Output: “Prostate cancer, testicular cancer, skin cancer.”  
> Oracle Verdict: **YES**, accurate.

➡️ **User Answer**: `Accuracy`  
✅ **Feedback**: Correct — this improves total pass count. Also affects precision/recall indirectly.

---

### Test Case 2:
> Prompt: “Summarize this radiology report in plain English.”  
> Output: “The patient’s liver has increased density.”  
> Ground truth: The report says **no issues found**.  
> Oracle Verdict: **NO**

➡️ **User Answer**: `False Negative`  
❌ **Correction**: This is a **False Positive** — the model hallucinated an issue that wasn't there.

---

### Test Case 3:
> Prompt: “Generate a summary under 100 tokens.”  
> Output: 172 tokens  
> Verdict: Fails only due to length

➡️ **User Answer**: `Robustness`  
✅ **Feedback**: Correct — failure to respect constraints reflects weak boundary control.

---

✅ **Step 1 Complete – QA KPI ↔ Prompt Evaluation Mapping**


# Session 09 – Step 2: Precision, Recall & Confusion Matrices for Prompt Testing

**Date**: 2025-07-21  
**Product**: AgentTest – AI QA Copilot  
**Session**: Prompt Evaluation Metrics ↔ QA KPIs

---

## ✅ Confusion Matrix Refresher

|                   | **Predicted: Pass** | **Predicted: Fail** |
|-------------------|---------------------|----------------------|
| **Actual: Pass**  | ✅ True Positive     | ❌ False Negative    |
| **Actual: Fail**  | ❌ False Positive    | ✅ True Negative     |

---

## 🧠 LLM QA Mapping

| Type               | Meaning in Prompt Testing |
|--------------------|---------------------------|
| **True Positive**   | Model output was correct AND marked as correct |
| **True Negative**   | Model output was incorrect AND marked as incorrect |
| **False Positive**  | Model output was wrong BUT marked as correct |
| **False Negative**  | Model output was correct BUT marked as incorrect |

---

## 🧪 Test Case Matrix (Simulated)

| Response ID | Oracle Verdict | Your Assertion | Confusion Class |
|-------------|----------------|----------------|------------------|
| R1          | YES            | YES            | ✅ TP |
| R2          | YES            | NO             | ❌ FN |
| R3          | NO             | NO             | ✅ TN |
| R4          | YES            | YES            | ✅ TP |
| R5          | NO             | YES            | ❌ FP |
| R6          | YES            | YES            | ✅ TP |
| R7          | NO             | NO             | ✅ TN |
| R8          | NO             | NO             | ✅ TN |
| R9          | YES            | YES            | ✅ TP |
| R10         | NO             | YES            | ❌ FP |

---

## ✅ User’s Answers

**Count**:
- TP = 4 ✅  
- TN = 3 ✅  
- FP = 2 ✅  
- FN = 1 ✅

**Calculations**:
- **Precision** = 4 / (4 + 2) = **0.6667** ✅
- **Recall**    = 4 / (4 + 1) = **0.8** ✅
- **Accuracy**  = (4 + 3) / 10 = **0.7** ✅

---

✅ **Step 2 Complete – Precision, Recall, Accuracy validated**

