<p align="center">
  <img src="assets/logo.png" alt="agent-plugin logo" width="180" />
</p>

<h1 align="center">agent-plugin</h1>

<p align="center">Opinionated Claude skills for sharper agents.</p>

## Install

[Open Plugins](https://open-plugins.com)-compatible. Skills live in `skills/`. Manifest at `.plugin/plugin.json`.

## Skills

### 🧱 [`typescript-principles`](skills/typescript-principles)

Naming, parameter, boolean, and error logging principles for TypeScript.

- Named parameters over positional
- Action-verb function names
- Structured error logging through one helper

### 🧹 [`deslop`](skills/deslop)

Skeptical implementation review.

- Flags silent `??` fallbacks
- Questions hand-rolled regex when libraries exist
- Calls out custom code that duplicates popular packages

### 🦴 [`caveman`](skills/caveman)

Ultra-compressed communication mode.

- Drops articles, pleasantries, hedging
- Keeps technical terms, code blocks, errors exact
- ~75% fewer tokens, same signal
