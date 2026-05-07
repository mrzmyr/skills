---
name: deslop
description: Use when reviewing, refactoring, or implementing code to challenge unnecessary fallbacks, brittle regex pattern matching, and custom code where a mature popular library would be safer.
---

# Deslop

Use this skill as a skeptical pass before accepting an implementation. Look for code that feels expedient but increases long-term ambiguity, brittleness, or maintenance cost.

## Fallbacks

Question fallbacks before keeping them.

Ask:

- Is this fallback a real product requirement or a convenience added during implementation?
- Does it hide misconfiguration that should fail loudly?
- Does an environment variable override create behavior that is hard to discover or reproduce?
- Should this be a typed configuration value, feature flag, explicit parameter, or documented operational setting instead?

Keep fallbacks only when the failure mode is intentional and observable.

## Regex Pattern Matching

Question regex usage before adding or preserving it.

Ask:

- Is the input format simple, stable, and bounded enough for regex?
- Would a parser, URL API, schema validator, tokenizer, or SDK method be more correct?
- Are edge cases and escaping rules obvious from tests?
- Is this regex doing business logic that deserves named code instead?

Prefer structured APIs over pattern matching when the data has a real format.

## Popular Libraries

Before writing custom protocol, security, parsing, or integration code, check whether a mature popular library exists for the exact case.

Examples:

- Use established OAuth libraries for OAuth flows.
- Use schema validators for structured input validation.
- Use official SDKs for vendor APIs when available.
- Use proven parsers for real languages, URLs, dates, and document formats.

Custom code is acceptable when the library would add more risk than it removes, but make that tradeoff explicit.

## Review Output

When reporting findings, be concrete:

- Name the questionable fallback, regex, or custom implementation.
- Explain the risk.
- Suggest the simpler or more established alternative.
- Call out when the current approach is acceptable and why.
