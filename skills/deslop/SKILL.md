---
name: deslop
description: Question fallbacks, regex matching, and custom code when a popular library could be used.
---

# Deslop

Question these patterns when creating, reviewing, or refactoring code.

## Fallbacks

- Question your usage of fallbacks (e.g. environment variables overrides).

Avoid:

```ts
const EVAL_USER_EMAIL =
  process.env.EVAL_USER_EMAIL ??
  process.env.BIGQUERY_EVAL_USER_EMAIL ??
  "first.lastname@gmail.com";
```

Prefer:

```ts
const EVAL_USER_EMAIL = process.env.EVAL_USER_EMAIL;

if (!EVAL_USER_EMAIL) {
  throw new Error("EVAL_USER_EMAIL is required");
}
```

Avoid:

```ts
const total =
  order.grandTotal ??
  order.articles.reduce(
    (sum, article) => sum + Number(parseFloat(String(article?.amount)) || 0),
    0,
  );
```

Prefer:

```ts
const total = order.grandTotal;

if (total == null) {
  throw new Error("order.grandTotal is required");
}
```

Only use a fallback when the compatibility case is real and known:

```ts
const total = order.grandTotal ?? order.total;
```

## Regex Pattern Matching

- Question your usage of pattern matching via regex.

Avoid:

```ts
function readOnlyQuery(query) {
  const sql = String(query).trim().replace(/;+\s*$/, "");
  if (!/^(select|with|explain)\b/i.test(sql)) throw new Error("read only only");
  if (/\b(insert|update|delete|drop|alter|create)\b/i.test(sql)) throw new Error("mutating sql");
  return sql;
}
```

Prefer:

```ts
async function readOnlyQuery({ bigquery, query }) {
  const [job] = await bigquery.createQueryJob({ query, dryRun: true, useLegacySql: false });
  if (job.metadata.statistics?.query?.statementType !== "SELECT") throw new Error("read only only");
  return query;
}
```

## Popular Libraries

- Question if a very popular library for your specific case could be used rather than adding all the code yourself (e.g. oauth).

## Type Overwrites

- Question your usage of type overwrites/assertions when the inferred type should be used.
