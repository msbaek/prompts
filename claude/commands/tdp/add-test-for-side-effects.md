---
argument-hint: "[method-name]"
description: "Sometimes AI writes utility methods that unexpectedly mutate input. Or it quietly modifies shared state."
---

Add the following prompt

## Prompt

Check if this method has side effects like modifying input arguments or static state.
Write a unit test that will fail if any such side effects occur.
