---
name: typescript-principles
description: Use when writing, reviewing, or refactoring TypeScript code to apply naming, parameter, error logging, and file-context principles.
---

# TypeScript Principles

Apply these principles when creating, reviewing, or refactoring TypeScript.

## Function Calls

- Prefer named parameters over positional parameters.
- Use an object argument when a function takes multiple values, optional values, or values whose meaning is not obvious from type alone.

```ts
getUsers({ pageSize, pageIndex });
```

Avoid:

```ts
getUsers(pageSize, pageIndex);
```

## Error Logging

Every real error path must use the project's structured error helper. This includes thrown errors, returned HTTP/OAuth/JSON errors, and error logs.

Structured errors must include:

- `status`
- `message`
- `why`
- `fix`

The fields must be specific enough for an operator or developer to understand what happened, why it happened, and what action resolves it.

Avoid:

```ts
throw new Error(`Auth0 metadata request failed with ${response.status}`);
```

Prefer:

```ts
throw createError({
  status: 502,
  message: "Auth0 metadata request failed",
  why: `Auth0 returned status ${response.status} while loading OAuth metadata`,
  fix: "Verify Auth0 is reachable and the issuer configuration is correct",
});
```

## Boolean Names

Boolean-returning functions must be prefixed with a boolean-style verb.

Use prefixes like:

- `is`
- `has`
- `can`
- `should`
- `was`
- `will`

```ts
function isAllowed({ userId }: { userId: string }): boolean {
  return userId.length > 0;
}
```

Avoid ambiguous boolean names:

```ts
function allowed(userId: string): boolean {
  return userId.length > 0;
}
```

## Local File Name Context

Use the file name as naming context. Do not repeat the domain already supplied by the file path or file name unless it removes ambiguity at the call site.

Example: in `data-analysis.ts`, prefer:

```ts
export function getSandbox() {
  // ...
}
```

Over:

```ts
export function getDataAnalysisSandbox() {
  // ...
}
```

Prefer shorter local names when the module boundary already supplies the noun. Use longer names only when exported APIs are commonly imported into contexts where the shorter name would be unclear.
