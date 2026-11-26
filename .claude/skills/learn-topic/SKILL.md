---
name: learn-topic
description: Write (or update) a comprehensive, beginner-friendly Markdown learning doc in my-learning/ for one path A course topic, e.g. "/learn-topic 0.3" or "/learn-topic idempotency". Use whenever the learner asks for a doc, notes, or explanation file for a course topic.
argument-hint: <course number or topic name, e.g. 0.1 | 1.1.0 | middleware>
---

# Write a learning doc for a course topic

The reader is a React frontend developer learning backend for the first time, in Node.js/TypeScript (Express and NestJS). Their project uses **NestJS**. The doc must be easy to learn from the first time and easy to look things up in later.

## 1. Find the source

- Match `$ARGUMENTS` to a file in `courses-content/backend/A/1/en/`. Match by number prefix first (`0.3` → `0.3 Архитектуры Back End.md`), then by topic name against the English headings (filenames are in Russian). Use `config.json` in that folder for the module order and titles.
- If the argument is ambiguous or matches nothing, list the closest candidates and ask which one.
- Read the whole source file. If something in the English text reads oddly, compare it with the Russian original in `../ru/`.
- Ignore all .NET and Python content.

## 2. Check what already exists

- If `my-learning/` already has a doc for this topic, update and extend it. Don't create a duplicate. Keep any notes the learner added themselves.
- Skim the docs already in `my-learning/`. Link to them instead of re-explaining concepts they cover, and reuse their terms so the series stays consistent.

## 3. Plan the learning order (do this before writing)

The learner finds the course hard to follow. Our docs must be systematic and must build up in strict dependency order.

1. List every concept the topic needs, including ones the course takes for granted.
2. Order them so that **each concept depends only on concepts before it**: in this doc or in an earlier `my-learning/` doc.
3. Any prerequisite not covered by an earlier doc goes into a **"Before we start"** primer at the top. Teach it there briefly but properly.
4. Note where the course is ambiguous, vague, or out of order. The doc resolves each of those plainly (state the most reasonable reading where the course is unclear) and never repeats them.
5. Plan the progression from simple to complete: the intuition first, then the simplest working version, then each added layer, until the topic is fully covered for Node.js/TS + NestJS.

Never use a term before it is explained. Never defer something needed now with "we'll cover this later".

## 4. Verify before stating facts

Library APIs, package names, versions, and defaults change. Anything you're not certain is current (NestJS APIs, a library's options, security recommendations such as hashing parameters) needs checking against the official docs before it goes in the doc.

## 5. Write the doc

File: `my-learning/<course-number>-<english-kebab-topic>.md`, for example `my-learning/0.3-backend-architectures.md`. Follow any different layout the learner has already set up.

**Style**
- Use plain, simple English with short sentences and paragraphs. Define each term the first time it appears, and **bold** it.
- Write for an absolute beginner in backend. Assume no backend knowledge, but do assume solid JS/TS, React, and browser knowledge. Easy to read must not mean incomplete: by the end, the learner should know everything they need on the topic for Node.js/TS + NestJS.
- Bridge from the frontend where the analogy is accurate: React component tree ↔ module/DI tree, fetch ↔ the request the server receives, browser cookies, form validation ↔ server validation, npm. Say where an analogy breaks down.
- Teach the topic; don't translate the course text section by section. Cover everything the course file covers, then go deeper wherever a beginner would get stuck. Skip extras that neither the course nor the project needs.

**Structure** (adapt the headings to the topic, but keep this order)
1. Title, a one-line summary, a link to the course source file, and the total study time.
2. **What you'll learn**: a numbered roadmap of the sections, so the learner sees the build-up before starting.
2b. **How to learn this guide**: how to approach studying this specific doc.
   - Plan **one session per day**. Give a table with the day, what to read, the course-file topic it covers, and a **realistic time**: careful reading, running every example, the exercise, and that day's self-check questions, usually 1.5–2.5 hours. Size the sessions to fit one day: follow the course file's topics, merging topics while the day still fits about 2.5 hours and splitting ones that are too big. Use as few days as that allows, because there are many topics to get through.
   - For each day, give a time breakdown, a hands-on exercise (runnable in the local playground where the topic allows, using only what the docs have taught), and the numbers of the self-check questions that belong to it. A few days after the last session, the learner answers all of them without scrolling up.
   - If the doc's order differs from the course file's, say where and why.
   - Give a per-section routine: skim, run or try, explain it back, move on only when it's clear.
   - Say how to use the doc after the first pass: the cheat sheet as a reference, self-check questions again later, and which project tasks to revisit it for.
3. **Before we start** (only if needed): primers on prerequisites not covered by earlier docs, plus links to the earlier docs this one builds on.
4. **Why this matters**: the problem this solves and where it shows up in the course project.
5. **Concepts**: built up in the dependency order planned in step 3, one idea per section. Add Mermaid diagrams for flows, sequences, relationships, and lifecycles.
6. **In code**: TypeScript only. Lead with NestJS, since that is the learner's project framework. Add the Express equivalent when seeing the raw version shows what Nest does under the hood. Keep snippets small and commented.
7. **Common mistakes**: especially frontend habits that are wrong on the backend.
8. **Cheat sheet**: a condensed quick reference (tables or bullets) to scan later.
9. **Self-check questions**: answers go in `<details><summary>Answer</summary>…</details>`. Include the course's own review questions plus your own.
10. **Further reading**: official docs first, using the course's Node.js links where they are good.

**For practical-task files (`X.Y.Z`)**, also add a **"Building it in the project"** section:
- the contract restated in plain English: endpoints, request and response shapes, status codes, error cases;
- the data model it needs;
- the request flow through the Nest pieces (controller → pipe/guard → service → repository), with a diagram;
- recommended libraries, each with the reason and one alternative;
- an ordered implementation checklist and the edge cases to test.

Do **not** write the implementation. The learner builds it. Small illustrative snippets are fine; complete working solutions are not.

## 6. Report back

Reply with the file path, a 3–5 bullet summary of what the doc covers, and anything you verified or were unsure about.
