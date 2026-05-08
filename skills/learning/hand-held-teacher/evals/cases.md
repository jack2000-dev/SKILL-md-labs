# Evals — hand-held-teacher

Manual eval cases. Run by pasting prompts into a Claude session that has this skill installed.

This skill is interactive and qualitative — there are no objective assertions. Grade by behavior.

---

## Trigger tests (skill SHOULD fire)

### T1 — Direct "teach me"
**Prompt:** "Teach me how SQL JOINs work. I'm new to databases."
**Expected:** Skill triggers. First reply assesses learner (what they know, tech stack — e.g., which DB they use), does NOT start teaching.

### T2 — Paraphrased, no "teach"
**Prompt:** "I'm a beginner with React and I'd like to be guided through hooks step by step."
**Expected:** Skill triggers. First reply assesses prior React knowledge and asks about their setup. Does NOT dump a hooks tutorial in one turn.

### T3 — Non-technical learning request
**Prompt:** "Walk me through the basics of stoicism — I want to actually study it, not just read a wiki page."
**Expected:** Skill triggers. First reply assesses prior exposure (read any of the texts? heard the term? etc.) and asks goal. No tech stack question (topic is not technical). Plans 3–6 chunks before teaching.

### T4 — "Tutor me"
**Prompt:** "Can you tutor me on linear algebra? I haven't done math in years."
**Expected:** Skill triggers. Assessment turn first — gauges what they remember, asks about goal (course, ML, just curiosity).

---

## Negative trigger tests (skill should NOT fire)

### N1 — One-shot explanation
**Prompt:** "What is a Merkle tree?"
**Expected:** Skill does NOT trigger. This is a one-shot explanation request — `super-explainer` is the right skill, or Claude answers directly.

### N2 — Tutorial / how-to
**Prompt:** "How do I install Postgres on macOS?"
**Expected:** Skill does NOT trigger. Step-by-step install guide, not learning.

### N3 — Debugging
**Prompt:** "My promise chain is throwing 'undefined is not a function' on line 42 — help me fix it."
**Expected:** Skill does NOT trigger. Debugging task, not teaching.

### N4 — Ambiguous keyword overlap
**Prompt:** "Explain compound interest to me."
**Expected:** Skill does NOT trigger (use `super-explainer`). The verb is "explain", not "teach me", and there is no learner framing.

---

## Behavior tests (assume skill triggered)

### B1 — Starts with assessment, not teaching
**Prompt:** "Teach me how Git branches work."
**Expected behavior:**
- First reply asks what learner already knows about Git (commits? other VCS?)
- Asks tech stack relevance (CLI, GUI client, hosted on GitHub/GitLab)
- Optionally asks goal
- Does NOT start explaining branches in turn 1

### B2 — Chunks the topic, ends each chunk with a check-in
**Prompt:** "Teach me how HTTPS works. I know basic HTTP."
**Expected behavior (after assessment turn):**
- Lays out a short plan (3–6 chunks)
- Teaches chunk 1 only (e.g., "why HTTPS exists")
- Ends turn with a check-in question, not a wall of follow-on content

### B3 — Hints, does not give away answer
**Prompt sequence:**
1. "Teach me recursion in Python."
2. (After lesson, during quiz) "I'm not sure how to write the base case for the factorial function."
**Expected behavior:** On step 2, Claude offers a hint or a leading question (e.g., "What's the smallest input where you already know the answer without doing any math?"), NOT the finished `if n == 0: return 1` line.

### B4 — Gives answer when explicitly asked
**Prompt sequence (continuing B3):**
3. "Just tell me the answer."
**Expected behavior:** Claude reveals the base case AND adds a one-line "why" so the reasoning is visible. No lecture about how the learner should have figured it out.

### B5 — Suggests a tech stack when learner has none
**Prompt:** "I want to learn web development but I've never written code before. Teach me."
**Expected behavior:** Assessment turn includes a suggestion of a starter stack (e.g., "I'd suggest plain HTML/CSS/JS in the browser before any framework — sound OK?") rather than asking "what's your stack" when the learner has none.

### B6 — Provides further reading and a quiz before declaring done
**Prompt:** Run a full lesson on a small topic (e.g., "Teach me what a hash function is and where they're used") to completion.
**Expected behavior:**
- Lesson chunked across turns
- Before wrap-up: 2–4 real-looking further reading sources (no obviously fake links)
- A short quiz (3–5 questions) presented WITHOUT the answers
- After learner answers: kind grading, hints rather than answers for misses (unless asked), one-line summary at the end

### B7 — Stays concise
**Prompt:** Any teaching prompt.
**Expected behavior:** Each individual turn is short — assessment turn is mostly questions, chunk turns are 1–4 short paragraphs, hint turns are 1–3 lines. No massive monolithic replies.

---

## Notes for the human grader

- This skill is judged by **flow across turns**, not single-message correctness. Run the full conversation, not one prompt.
- Two failure modes to watch for: (1) skill skips assessment and starts teaching immediately; (2) skill dumps the whole topic in one turn instead of chunking.
- Tone should feel like a patient peer tutor. Flag anything that sounds condescending or like flattery filler.
