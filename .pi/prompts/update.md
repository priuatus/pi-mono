---
description: Fetch upstream and rebase main to sync changes
---

Fetch from upstream and rebase main to sync changes.

Steps:
1. `git fetch upstream`
2. `git rebase upstream/main`
3. If conflicts occur:
   - For `packages/ai/src/models.generated.ts`: take upstream's version (it's auto-generated)
   - For `package-lock.json`: delete and regenerate with `npm install --package-lock-only --ignore-scripts`
4. Continue rebase with `git rebase --continue`
5. After successful rebase, force push: `git push --force-with-lease origin main`

Final step:
- Summarize the changes since last update (changelog). Note any interactions with the patches we are hosting in our fork (the commits you rebased).
