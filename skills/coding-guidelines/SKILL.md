---
name: coding-guidelines
description: Use when writing, reviewing, or refactoring code to avoid overcomplication, make surgical changes, surface assumptions, and define verifiable success criteria.
---

# Coding Guidelines

## 1. Planning

### Think Before Coding

Before implementing:

- State your assumptions and relevant tradeoffs explicitly.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

### Goal-Driven Execution

Define success criteria. Loop until verified.

For refactoring, ensure tests pass before and after.

For multi-step tasks, state a brief plan with a verification check for each step.
Finish and verify each small unit before starting the next.
A break in the middle is allowed when you planned it and can undo it.

### Foundational Thinking

- Get the data shape right before you write the logic.
- Do first whatever helps every later phase.

### Redesign From First Principles

- Prefer extending the existing design when it can satisfy the request correctly.
- Redesign only when explicitly requested or necessary for correctness. In that case, consider what you would have built with the requirement present from the start, and deliver only the necessary changes in pieces.

## 2. Implementation

### Simplicity First

Write the minimum code that solves the problem.

- No features, flexibility, or configurability beyond what was asked.
- No abstractions for single-use code.
- No error handling for impossible scenarios.

### Surgical Changes

When editing existing code:

- Don't "improve" adjacent code, comments, or formatting.
- Refactor only when explicitly requested or necessary to satisfy the current requirements.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.
- Remove imports/variables/functions that YOUR changes made unused.

The test: Every changed line should trace directly to the user's request.

### Laziness Protocol

- One decision lives in one place.

### TDD

- Write the failing test before you change the code.
- See it fail for the reason you expect.
- Make the smallest change that makes it pass.
- If an honest test is impractical, do not write a bad one.
- Never remove, skip, or weaken tests just to make them pass.
- Passing tests do not guarantee correctness.

### Subtract Before You Add

- Simplify affected code before extending it only when simplification is requested or needed for the change. Do not make unrelated cleanup a prerequisite.

### Build the Lever

- Build a helper only when requested or when repetitive or error-prone work in the current task justifies its cost; prefer existing tools when suitable.
- When building a helper, verify one representative unit manually first, then check that the tool reproduces the result.

### Security & Configuration

Do not add `.env` files, API keys, webhook secrets, or new service-account credentials. Keep secrets
in local environment configuration.

### Architecture

#### Model the Domain

- Use domain structures and types that make illegal states and values impossible.
- Maintain a glossary only when requested or when ambiguous domain terms affect the current task; reuse existing documentation when possible.

#### Boundary Discipline

- Parse and validate external data once, where it enters.
- Inside, trust it.
- Keep the business logic in a pure function.

#### Type System Discipline

- Do not silence the compiler.

#### Make Operations Idempotent

- Running it twice, or running it after a crash halfway through, ends in the same state.

#### Separate Before Serializing Shared State

- If they do not need the same mutable thing, give each its own.
- If they do, allow one writer, and enforce that in the structure.

## 3. Verification and Debugging

### Fix Root Causes

- Reproduce it.
- Fix the cause.
- A guard that only hides the crash is not a fix.

### Attack the Premise

- When two attempted fixes based on the same assumption fail the same verification check, state that assumption explicitly.
- Before attempting another fix, check the assumption against a minimal reproduction, test results, or an execution trace.
- If the evidence disproves the assumption, revise it. If it supports the assumption, investigate another cause. Base the next fix on the evidence collected.

### Test Behavior, Not Implementation

- The test calls the code the way its user does and checks the result that user would see.
- If the test would still pass when every function returned nothing, throw it out.

## 4. Pull Requests

- Write pull request titles and descriptions in English.
- Structure PR descriptions into the following sections, in this order; omit User Stories,
  Cosmetic Changes, or Technical Changes when there are no changes in that category:
  1. **User Stories:** Describe behavioral changes from the user's perspective, focusing on what the
     feature should accomplish rather than how it was implemented.
  2. **Cosmetic Changes:** Describe purely aesthetic, visual, and layout changes.
  3. **Technical Changes:** Describe independent internal changes with no user-facing behavioral
     or visual impact, such as refactoring or build tooling changes. Technical work supporting a
     User Story or Cosmetic Change belongs in that item's Technical Implementation entry.
  4. **Before and After:** Compare the previous and resulting behavior, appearance, or internal
     technical state for each change. Use a Markdown table with
     **Before** and **After** columns to present each comparison side by side.
  5. **Technical Implementation:** Explain how the changes were implemented, highlighting key
     technical decisions and relevant changes.
- Assign a unique identifier to each User Story (`US-1`, `US-2`, etc.), Cosmetic Change
  (`CC-1`, `CC-2`, etc.), and Technical Change (`TC-1`, `TC-2`, etc.). Reuse these exact identifiers
  in an **ID** column in the Before and After
  table and in every Technical Implementation entry to identify the changes they support.
  Every User Story, Cosmetic Change, and Technical Change must have corresponding Before and
  After and Technical Implementation entries.
- Do not include a Validation section.
- Only push commits or create/update a pull request after the user explicitly confirms that the
  commit is finished.
- Keep subsequent changes local until the user gives that instruction again.
- Don't start a new pull request until the user explicitly confirms that the previous one is finished.
