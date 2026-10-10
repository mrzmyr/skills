---
name: increase-readibility
description: Use when writing or rewriting prose for a reader who skims, such as reports, plans, PR descriptions, status summaries, specs, and instructions. Applies bullets, nesting, bold key points, Simplified Technical English, and MoSCoW priorities.
---

# Increase Readability

These are guidelines, not hard rules. Apply a technique only when it makes the text faster to skim. Skip it when it adds noise.

## Structure

- **Bullets over long paragraphs.** One idea per bullet.
  - ❌ A 6-line paragraph that mixes cause, impact, and next step.
  - ✅ Three bullets: `Cause`, `Impact`, `Next`.
- **Nest for hierarchy.** Put detail under the point it supports. Keep nesting to 2-3 levels.
  - ✅ `Migration blocked` → `Needs API key` → `Owner: Sam, due Friday`
- **Keep prose for reasoning.** Use a short paragraph when ideas depend on each other and bullets would break the logic.

## Emphasis

- **Bold key aspects only.** Bold the decision, number, owner, or risk a skimmer must not miss.
  - ❌ Bold on every second phrase.
  - ✅ "Deploy is **blocked** until the **API key** arrives."
- **Front-load.** Put the conclusion first, then detail.

## Language (ASD-STE100 Simplified Technical English)

- **One meaning per word.** Use the same word for the same thing. Do not vary terms for style.
- **Short sentences.** One idea, about 20 words maximum.
- **Active voice, simple tenses.**
  - ❌ "The cache should be cleared by the job before the build is started."
  - ✅ "The job clears the cache. Then the build starts."
- **Plain verbs.** Use `use`, not `utilize`. Use `start`, not `initiate`.
- **Commands for steps.** Write `Run the tests.`, not `The tests should be run.`
- **Keep technical names exact.** Do not rename APIs, commands, or error text for simplicity.
- **Apply only where it fits.** Skip for casual messages, creative writing, or text that must keep a personal voice.

## Priority (MoSCoW)

- Label items by priority when the reader must choose or act.
  - **MUST** — required. Work fails or is blocked without it.
  - **SHOULD** — important. Do it unless there is a good reason not to.
  - **COULD** — optional. Do it if time allows.
- Use these three labels only. Drop `Won't` unless the reader needs an explicit out-of-scope list.
- Group by priority, `MUST` first.
  - ✅
    - **MUST** — fix the failing migration
    - **SHOULD** — add a rollback test
    - **COULD** — rename the helper
- Skip labels when every item has the same priority.

## Check before sending

- Can the reader get the main point from the first line?
- Can the reader find their action in under 10 seconds?
- Did each technique remove effort for the reader? If not, undo it.
