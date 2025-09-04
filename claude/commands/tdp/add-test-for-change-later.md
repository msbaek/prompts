---
argument-hint: "[method-name]"
description: "This prompt forces AI to think like a maintainer. Not just a builder."
---

Add the following prompt

## Prompt

Based on this code, what would break or behave differently if I changed the underlying implementation later (e.g., switched from List to Set)?
Write tests that assert expected behavior to help catch such regressions.
