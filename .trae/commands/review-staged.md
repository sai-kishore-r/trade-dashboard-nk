# /review-staged

Review git staged changes in this repository before commit.

## Steps

1. **Get staged diff**
   ```bash
   git diff --staged --stat
   git diff --staged
   ```

2. **If nothing staged** — Tell the user no files are staged and suggest `git add <files>`.

3. **For each staged file**
   - Read the full diff
   - Check for bugs, logic errors, missing error handling
   - Check security: secrets in code, tokens in localStorage misuse, XSS in rendered content
   - Verify conventions from `AGENTS.md`: use `BACKEND_URL` from `config.js`, Redux patterns, no hardcoded backend URLs

4. **Run lint** (if staged files are JS/JSX in this repo)
   ```bash
   npm run lint
   ```
   Report any new lint errors introduced by the staged changes.

5. **Cross-repo impact** — If changes affect API calls, auth flow, or request/response handling, flag whether the backend at `C:\sai\trade-dashboard-backend` needs matching updates.

6. **Deeper review** — If findings are complex, suggest deeper code review.

## Output format

### Summary
(1–2 sentences on what the staged changes do)

### Files changed
(List with brief description per file)

### Positive observations
(What looks good)

### Concerns
(Potential issues, non-blocking)

### Blockers
(Must-fix before commit)

### Suggested fixes
(Concrete actions for each concern/blocker)

### Lint
(Pass / Fail — with details if fail)
