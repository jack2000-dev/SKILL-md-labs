# Evals: invest-mud

## Trigger Tests

### Should trigger
- "I'm 32, make $80k, have $40k credit card debt at 22% APR. Help me figure out my finances."
- "Should I start investing in index funds or pay off my student loans first?"
- "I want to be financially independent by 45 — help me plan."
- "Review my budget. I save like $200/month and I don't know if that's good."
- "I keep losing money on crypto and stocks. Help me build a real strategy."
- "Plan my career and money for the next 5 years. I'm a software engineer in Bangkok."

### Should NOT trigger
- "What's the current price of Bitcoin?" (factual lookup, no advisory needed)
- "Explain how a 401k works." (educational, not personal planning)
- "Help me file my taxes." (specific tax prep, not life/wealth planning)
- "Build me a Python script to track expenses." (coding task)

## Behavior Tests

### Test 1 — Mandatory interview
**Prompt:** "I have $50k saved and want to invest. What should I buy?"
**Expected:** Skill refuses to give portfolio advice immediately. Instead opens with framing, then begins Category 1 questions (age, location, family, life goal). Does NOT skip to Category 10 (risk) or jump to recommendations.

### Test 2 — Pushback on premature analysis
**Prompt:** "Just tell me what stocks to buy. I don't want to answer 11 categories of questions."
**Expected:** Skill explains why incomplete data leads to bad recommendations. Offers a quick partial read with explicit caveats, but does NOT cave and produce a real portfolio without basics (debt, emergency fund, income stability).

### Test 3 — Foundation before investing
**Prompt (after gathering data):** User has $5k emergency fund (1 month expenses), $20k credit card debt at 24% APR, asks about investing $10k in tech stocks.
**Expected:** Skill applies "Critical Constraints" — debt and emergency fund come first. Refuses to recommend stock investing. Explains the math: 24% guaranteed savings from debt paydown beats expected stock returns.

### Test 4 — Risk Tolerance vs Risk Capacity
**Prompt:** User says they're "aggressive" risk-tolerant but has 1 child, unstable freelance income, no emergency fund.
**Expected:** Skill differentiates Risk Tolerance (emotional) from Risk Capacity (financial). Plan respects the lower of the two — recommends Conservative or Balanced portfolio despite stated tolerance.

### Test 5 — 14-section analysis coverage
**Prompt:** User has completed all 11 categories, asks "Give me my full report."
**Expected:** Output covers all 14 sections in order: Executive Summary, Balance Sheet, Cash Flow, Debt Strategy, Emergency Fund, Human Capital, Skill Roadmap, Goal Funding, IPS, Portfolios (3 models), Scenarios (3), Action Plan, Monthly Review, Brutal Truth.

### Test 6 — Brutal Truth section
**Prompt:** Same as Test 5.
**Expected:** "Brutal Truth" section is honest about excuses/blockers without being cruel. Names the #1 priority. Does not give generic platitudes.

## Quantitative Assertions (for future automation)

- Response to vague investment ask contains the word "Category 1" or first category keyword (age/family/location)
- Response to "$50k debt + $10k investment" prompt does NOT recommend buying stocks/ETFs/crypto
- Full report contains exact section headers: "Executive Summary", "Personal Balance Sheet", "Investment Policy Statement", "Brutal Truth"
- Risk Tolerance and Risk Capacity both appear in any portfolio recommendation
