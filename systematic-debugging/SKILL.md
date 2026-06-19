---
name: systematic-debugging
description: "4-phase root cause debugging: understand bugs before fixing."
---

# Systematic Debugging

## When to use
For ANY technical issue: test failures, bugs, unexpected behavior, performance problems, build failures.

## How

### The Iron Law
**NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST**

### Phase 1: Root Cause Investigation
1. **Read error messages carefully** — don't skip warnings, read full stack traces
2. **Reproduce consistently** — exact steps, every time?
3. **Check recent changes** — git diff, recent commits, new dependencies
4. **Gather evidence** — log data in/out at each component boundary
5. **Trace data flow** — where does the bad value originate?

**Completion checklist:**
- [ ] Errors fully read and understood
- [ ] Issue reproduced consistently
- [ ] Recent changes identified
- [ ] Evidence gathered
- [ ] Problem isolated to specific component
- [ ] Root cause hypothesis formed

### Phase 2: Pattern Analysis
1. Find working examples in the same codebase
2. Compare against references
3. Identify every difference
4. Understand dependencies

### Phase 3: Hypothesis and Testing
1. Form single hypothesis: "I think X is root cause because Y"
2. Test minimally — smallest possible change, one variable
3. Verify before continuing
4. If doesn't work → form NEW hypothesis

### Phase 4: Implementation
1. Create failing test case
2. Implement single fix (root cause, not symptom)
3. Verify fix + no regressions
4. **Rule of Three:** If 3+ fixes failed → question architecture, don't try fix #4

### Red Flags — STOP and Follow Process
- "Quick fix for now, investigate later"
- "Just try changing X and see if it works"
- "Skip the test, I'll manually verify"
- "It's probably X, let me fix that"
- "One more fix attempt" (after 2+ failures)
