# AGENTS.md

Guidance for AI coding agents (and humans) working in this repository.

## Repo context

- **Purpose**: Centralized repository for **OPA (Open Policy Agent) policies** (Rego).
- **Primary languages/formats**: `rego`, `yaml/yml`, `json`, `md`.

## Where to make changes

- Add new policies under a clearly named folder (e.g. `policies/<domain>/...`) if/when such a folder exists.
- Keep policy modules small and focused; prefer multiple modules over one large file.
- Include tests for new/changed policy behavior (Rego test files typically end with `_test.rego`).

## Local dev / validation commands

This repo may be used in environments that already have OPA tooling installed. Prefer these commands when available:

- **Format Rego**:

  ```bash
  opa fmt -w .
  ```

- **Run Rego tests**:

  ```bash
  opa test -v .
  ```

- **Lint YAML (optional, if `yamllint` is available)**:

  ```bash
  yamllint .
  ```

If these tools are not installed in the environment, do not add heavy tooling just to run checks unless the task explicitly requires it.

## Policy conventions (Rego)

- **Use explicit package names**: `package <org>.<product>.<domain>` (avoid `package main`).
- **Prefer `default` decisions**:
  - `default allow := false` (or equivalent) in decision modules.
- **Keep inputs/outputs stable**:
  - When changing decision shapes, update all relevant callers/docs/tests.
- **Add tests for behavior changes**:
  - Cover both allow/deny (or pass/fail) paths.
  - Use descriptive test names and minimal fixtures.

## Documentation

- Update `README.md` when adding new policy areas, entrypoints, or expected inputs.
- If adding a new policy “API” (new decision), document:
  - expected `input` shape
  - decision name(s)
  - examples

## Security / safety

- Do not commit secrets, tokens, or private endpoints.
- Avoid writing policies that log or expose sensitive `input` fields.

## PR/commit hygiene (when applicable)

- Keep changes scoped and easy to review.
- Include a short test plan in PR descriptions (what you ran, what you validated).

