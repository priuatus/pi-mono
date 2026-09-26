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
   - For `packages/coding-agent/install-lock/package-lock.json` and `packages/coding-agent/npm-shrinkwrap.json`: delete and regenerate with `node scripts/generate-coding-agent-install-lock.mjs` and `node scripts/generate-coding-agent-shrinkwrap.mjs`
4. Continue rebase with `git rebase --continue`
5. After successful rebase, force push: `git push --force-with-lease origin main`

Final step:
- Summarize the changes since last update (changelog). Note any interactions with the patches we are hosting in our fork (the commits you rebased).
- Sanity-check the result: run `npm run check:shrinkwrap` and `npm run check:install-lock:coding-agent` before pushing, and after pushing run `npm ci --ignore-scripts` locally so `node_modules` matches the updated lockfile.
