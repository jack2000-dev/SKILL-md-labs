# Evals: super-explainer

## Trigger Tests

### Should trigger
- "What is a Merkle tree?"
- "Compound interest explained"
- "Tell me about retrieval-augmented generation"
- "Explain the Federal Reserve to me"
- "Help me understand Kubernetes"
- "What's the deal with Bayesian inference?"
- "Quantum entanglement for beginners"
- "I don't really understand zero-knowledge proofs"
- "How does PCA work?" (conceptual, not code)
- "What's CAP theorem in simple terms?"

### Should NOT trigger
- "How do I install Node.js?" (tutorial, not concept)
- "Fix this bug in my Python code." (debugging)
- "What's the weather today?" (factual lookup)
- "Translate this sentence to French." (task)
- "Write me a function that sorts an array." (code generation)
- "What time is the meeting?" (lookup)

## Behavior Tests

### Test 1 — Section structure compliance
**Prompt:** "What is a hash function?"
**Expected:** Output contains all 5 sections in order, with these exact headings:
1. "Why This Matters"
2. "Prerequisites & Difficulty"
3. "The Explanation" (or close variant containing "Plain English" framing)
4. "Core Takeaways" + "Conclusion" + "Practical Adaptation"
5. "Origin & Timeline" + "Further Reading" + "Glossary"

### Test 2 — Motivation comes first
**Prompt:** "Explain dynamic programming"
**Expected:** First substantive section is WHY (benefits, when to use, when not to), NOT a definition. Definition appears in Section 3.

### Test 3 — Prerequisites table populated
**Prompt:** "What is general relativity?"
**Expected:** Section 2 contains a table with at least: Difficulty, Prerequisites, Time-to-grasp. Difficulty marked "Advanced." Prerequisites should include calculus, special relativity (or similar real prerequisites — not vague filler).

### Test 4 — Plain English rule
**Prompt:** "Explain Byzantine fault tolerance"
**Expected:** Section 3 introduces the concept in 2–3 plain sentences before any technical detail. Jargon ("consensus," "fault model") is defined at first use, not assumed.

### Test 5 — Practical adaptation specific
**Prompt:** "Compound interest explained"
**Expected:** Section 4 contains a concrete heuristic (e.g., Rule of 72) and a specific real-world action the reader can take, NOT generic advice like "save more money."

### Test 6 — Glossary completeness
**Prompt:** "What is a Merkle tree?"
**Expected:** Glossary contains entries for at least: hash function, leaf node, root hash. All technical terms used in the explanation appear in the glossary.

### Test 7 — Honest sourcing
**Prompt:** "Explain something obscure that has thin sources" (e.g., a niche CS theory result)
**Expected:** If only 1–2 real sources exist, skill says so rather than fabricating 6 sources. No hallucinated paper titles or DOIs.

### Test 8 — Skip non-conceptual asks
**Prompt:** "How do I configure nginx for HTTPS?"
**Expected:** Skill does NOT trigger. This is a tutorial, not a concept explanation.

### Test 9 — User-context adaptation
**Prompt:** "I'm a doctor. Explain Bitcoin to me."
**Expected:** Section 3 uses analogies/framing relevant to medicine (e.g., distributed ledger compared to medical records, trust without central authority). Prerequisites adjust to skip basic CS assumptions where reasonable.

### Test 10 — No flattery
**Prompt:** "What's the difference between TCP and UDP?"
**Expected:** Output does NOT start with "Great question!" or similar pleasantry. Goes straight to Section 1.

## Quantitative Assertions (for future automation)

- Output contains all 5 section heading keywords: "Why", "Prerequisites", "Explanation"/"Plain English", "Takeaways", "Glossary"
- Section order: "Why" appears before "Prerequisites" appears before "Glossary"
- Section 2 contains a markdown table
- Section 5 "Further Reading" lists ≥3 entries (or explicit honest statement of fewer)
- Glossary contains ≥1 entry
- Output does not start with "Great question", "Sure!", "Of course", or "Happy to"
- Output for tutorial-style prompts ("how do I install...") does not contain "Why This Matters" heading
