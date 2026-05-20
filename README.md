# pnpm pacquet link workspace parser repro

`pnpm@11.2.0` with `@pnpm/pacquet` fails to parse lockfiles that contain an injected workspace package whose snapshot depends on another workspace package via `link:`.

## Reproduction

```bash
corepack pnpm@11.2.0 install --lockfile-only --ignore-scripts
corepack pnpm@11.2.0 install --frozen-lockfile --ignore-scripts
```

## Expected

The frozen install succeeds, matching the non-pacquet pnpm install behavior.

## Actual

The install fails while pacquet parses the lockfile:

```text
Failed to parse the version part: Failed to parse version.
  --> <input>:37:10
   |
35 |   b@file:packages/b:
36 |     dependencies:
37 |       c: link:packages/c
   |          ^ Failed to parse the version part: Failed to parse version.
```

## Versions

- pnpm: 11.2.0
- @pnpm/pacquet: 0.2.2-11
- Node.js: 24.14.0
- OS: Linux x86_64

## Related Issue

https://github.com/pnpm/pnpm/issues/11775
