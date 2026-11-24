---
name: review-my-code
description: Mentor-style review of the learner's own NestJS project code: checks it against the course task's contract, explains why each issue matters on the backend, and gives hints rather than rewrites. Use when the learner asks to review, check, or get feedback on their project code.
argument-hint: [task number e.g. 1.1.0] [path or "staged"] (default: all uncommitted changes)
---

# Review the learner's code as a mentor

The learner is a React frontend developer building their **first backend project**: a NestJS app at the repo root, for path A of the course. The point of the review is to help them **learn**, not just to find bugs. Read only. **Never edit their files** unless they explicitly ask for a specific fix afterwards.

## 1. Work out what to review

- **Code:** if `$ARGUMENTS` names a path, review that path. `staged` means `git diff --cached`. Otherwise review all uncommitted work: `git diff HEAD` plus untracked files from `git status`, ignoring `courses-content/` and `my-learning/`. If nothing has changed, ask what to review.
- **Task:** if `$ARGUMENTS` has a task number, read that task in `courses-content/backend/A/1/en/` (match by number prefix). Otherwise infer the task from the code (registration, auth, RBAC, and so on) and say which one you assumed.
- Read the task's `# Practical assignment` section: user stories, contract, errors and constraints, audit/logs, and non-functional requirements. That is the spec you review against.
- Read enough of the surrounding code (modules, entities, config, `main.ts`) to judge the change in context.

## 2. Review across these areas

1. **Meets the contract:** endpoints, methods, request and response shapes, status codes, error cases, and every user story from the task.
2. **Correctness:** logic bugs, missing `await`, unhandled rejections, race conditions (for example two registrations with the same email), and missing transactions where several writes must succeed or fail together.
3. **Security:** password hashing, token and cookie flags (`httpOnly`, `secure`, `sameSite`, expiry), authorization checked on the server for every protected route, ownership checks (IDOR), input validation and whitelisting, injection risks, secrets kept out of code, no internal errors or sensitive fields (password hash) leaked in responses.
4. **NestJS idioms:** the right building block for each job (pipe vs guard vs interceptor vs middleware vs filter), DTOs with validation, dependency injection instead of manual `new`, config through a config service, and module boundaries.
5. **Data:** the schema and constraints match the task (unique indexes, not-null, foreign keys); migrations are used rather than `synchronize`; no N+1 queries; pagination on list endpoints.
6. **Operability:** meaningful logs without secrets, the audit events the task requires, and consistent error responses.
7. **Testability:** what is untested and worth testing.

## 3. Write the feedback

Use this structure:

- **Summary:** 2–3 sentences on the overall state, and which task was reviewed against.
- **What's good:** specific things done well, so the learner knows what to keep doing.
- **Issues**, grouped by severity and most important first:
  - 🔴 **Must fix**: bugs, security holes, or contract violations.
  - 🟡 **Should fix**: wrong idioms, fragile code, missing validation or tests.
  - 🔵 **Nice to have**: style and polish.

  For each issue, give `file:line`, what is wrong, **why it matters on the backend** (one or two sentences, with a frontend comparison where one helps), and a **hint** toward the fix. Don't give a full rewrite. A short snippet is fine when the idea can't be explained without one.
- **Contract checklist:** each requirement from the task marked ✅ done, ⚠️ partial, or ❌ missing.
- **Learn next:** one or two concepts worth reading up on, linking to the matching doc in `my-learning/` if it exists, or suggesting `/learn-topic` if it doesn't.

Be direct and specific; skip generic advice. If something is a judgement call rather than a mistake, say so and explain the trade-off.
