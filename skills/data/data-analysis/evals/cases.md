# Evals: data-analysis-frameworks

## Trigger Tests

### Should trigger
- "perform data analysis on this dataset"
- "analyze data from our sales report"
- "can you analyze this data?"
- "do data analysis for me"

### Should NOT trigger
- "analyze this code"
- "analyze the error message"
- "explain data structures"

## Behavior Tests

### Test 1 — Phase coverage
**Prompt:** "Perform data analysis on monthly churn rates"
**Expected:** Response covers all 6 phases (Ask → Prepare → Process → Analyze → Share → Act) applied to churn context

### Test 2 — Ask phase depth
**Prompt:** "Analyze data" (vague)
**Expected:** Claude asks clarifying questions before proceeding (Ask phase behavior)

### Test 3 — Tool recommendation
**Prompt:** "Perform data analysis on a CSV of 50k rows"
**Expected:** Recommends appropriate tools (Python/pandas or SQL) in the Analyze phase
