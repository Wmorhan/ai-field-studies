# Design: Lesson 02 — Workflow Patterns

**Date:** 2026-06-04
**Output file:** `lessons/02-prompt-patterns/workflow-patterns.md`
**Audience:** Developers new to AI-assisted coding (solo and team)

---

## Goal

Teach readers that Claude has no implicit knowledge of their development process, and that defining workflows explicitly — in CLAUDE.md — is not optional configuration but a core practice. Git serves as the deep worked example. Other workflow types are mentioned to generalize the pattern.

---

## Structure

### Part 1: The failure (opening hook)
A short scenario — no preamble. Claude fixes a bug, but works on a branch that's two days stale, commits directly to main, and breaks CI. The reader recognizes this immediately or fears it. No moralizing — just the problem, stated plainly.

### Part 2: The meta-pattern
One or two paragraphs. Core argument: Claude starts every session with no memory of how your team works. Without explicit workflow definitions it makes locally reasonable decisions that violate your process. This is a contract to write once and reuse — not a workaround for a limitation.

Acknowledge both audiences:
- Solo devs: still need it, future-you will thank present-you
- Teams: urgent — one undefined step and Claude becomes a liability on shared branches

Tone: direct, no bullet lists. The git section carries the detail.

### Part 3: Git — the worked example
Four workflow rules. Each has one paragraph explaining *why*, followed by a copy-paste CLAUDE.md snippet.

**Rule 1: Pull before work**
Claude must run `git fetch` (or `git pull`) and confirm the current branch before touching any code. Stale code produces stale solutions — often silently.

```markdown
## Git: Before You Start
Always run `git fetch origin` and `git status` before reading or editing any file.
Confirm you are on the correct branch. If in doubt, ask.
```

**Rule 2: Branch discipline**
Never commit to main or master. Branch naming follows a convention (e.g. `feat/`, `fix/`, `chore/`). Define who creates the branch — Claude, or the developer.

```markdown
## Git: Branching
Never commit directly to `main` or `master`.
Always work on a feature branch. Branch names follow the pattern: `type/short-description`
(e.g. `feat/user-auth`, `fix/login-redirect`).
Create the branch before making any changes.
```

**Rule 3: Commit hygiene**
Atomic commits — one logical change per commit. Descriptive messages in imperative mood. No "WIP", "temp", or "fix fix" commits pushed to shared branches.

```markdown
## Git: Commits
Each commit should contain one logical change.
Write commit messages in imperative mood: "Add user validation" not "Added user validation".
Do not push WIP commits to shared branches.
```

**Rule 4: PR targeting**
Which branch to open the PR against. Draft vs ready. When to push vs when to wait for developer review.

```markdown
## Git: Pull Requests
Open PRs against `main` unless otherwise instructed.
Use draft PRs while work is in progress. Mark ready only when the task is complete.
Do not push to remote until explicitly asked to do so.
```

### Part 4: Other workflows worth defining
One paragraph per workflow type — enough to make the reader think "I need to define mine." No deep tutorial.

- **Test-before-commit:** Define whether tests must pass locally before any commit. Specify the test command.
- **Deployment gates:** Define what must be true before Claude can trigger or suggest a deploy.
- **Code review steps:** Define whether Claude should self-review, what checklist to follow, and when to flag for human review.

Close the section with: the pattern is always the same — identify the workflow, write the rule, add it to CLAUDE.md.

### Part 5: Key Takeaways + What's Next + Further Reading
Standard lesson footer matching lesson 01 format.

Key takeaways:
1. Claude has no memory of your process — define it explicitly
2. Git is the highest-risk implicit assumption in most projects
3. The meta-pattern applies to any workflow: test, deploy, review
4. Teams need this urgently; solo devs need it eventually
5. One CLAUDE.md section per workflow — write it once, rely on it always

What's Next: lesson 03 (debugging AI — when Claude gets stuck or confused)
Further Reading: link to Claude Code CLAUDE.md docs, link to conventional commits spec

---

## Out of scope
- Full tutorials on other workflow types (testing, deployment, code review)
- Specific CI/CD tool configuration
- Git branching strategy deep-dives (GitFlow, trunk-based, etc.)
- Non-CLAUDE.md enforcement mechanisms (branch protection rules, CI gates) — mention exists, no tutorial
