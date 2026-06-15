---
description: 'Run tests and a Foundry evaluation of the agent; report pass/fail with evidence.'
agent: implementer
---

Verify the agent works.

1. Run the test suite in `app/tests/` (including `app/tests/test_eval.py`). Show the output.
2. If a Foundry project is configured, run a batch evaluation using the **microsoft-foundry** skill
   (quality/groundedness/relevance graders) against a small dataset curated from `app/tests/`.
3. Report results as **pass/fail with evidence** (test output, eval scores). Do not claim success
   without showing the run. If anything fails, diagnose the root cause and fix it, then re-run.
