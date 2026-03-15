# Contributing to 47 Sunset OS

Thank you for contributing! This document describes the coding guidelines and tooling setup for this project to keep the codebase clean, consistent, and maintainable.

## Table of Contents

- [Getting Started](#getting-started)
- [Coding Guidelines](#coding-guidelines)
- [Tooling](#tooling)
- [Git Workflow](#git-workflow)

---

## Getting Started

```bash
# Install dependencies
npm install

# Run linting
npm run lint

# Run auto-fix for linting issues
npm run lint:fix

# Check formatting
npm run format:check

# Auto-format all files
npm run format

# Type-check the project
npm run build

# Run tests
npm test
```

---

## Coding Guidelines

### General Principles

- **Clean Code**: Write self-documenting code. Prefer descriptive variable and function names over comments.
- **DRY (Don't Repeat Yourself)**: Extract duplicated logic into reusable functions or modules.
- **Single Responsibility**: Each function, class, or module should do one thing well.
- **YAGNI**: Don't add functionality until it's needed.

### TypeScript

- Use **strict TypeScript**. All types must be explicit; avoid `any`.
- Prefer `interface` for public API shapes and `type` for unions/intersections.
- Always use `const` and `let`; never `var`.
- Use `type` imports (`import type { ... }`) for type-only imports.

### Code Complexity

Automated ESLint rules enforce the following limits:

| Metric                  | Limit                         | Rationale                              |
| ----------------------- | ----------------------------- | -------------------------------------- |
| Cyclomatic complexity   | ≤ 10                          | Keeps methods testable and readable    |
| Nesting depth           | ≤ 4 levels                    | Prevents "pyramid of doom"             |
| Lines per file          | ≤ 300 (excl. blanks/comments) | Encourages single-responsibility files |
| Lines per function      | ≤ 50 (excl. blanks/comments)  | Keeps functions focused                |
| Parameters per function | ≤ 5                           | Prefer options objects for more args   |

### Line Length

All lines are limited to **100 characters**, enforced by Prettier.

### Formatting

All formatting is handled automatically by **Prettier**. Run `npm run format` before committing, or configure your editor to format on save.

Key settings (see `.prettierrc`):

- Single quotes
- Semicolons
- Trailing commas
- 2-space indentation
- LF line endings

---

## Tooling

### ESLint

ESLint enforces code quality rules on all `.ts` and `.tsx` files. Configuration is in `.eslintrc.js`.

Run the linter:

```bash
npm run lint          # check only
npm run lint:fix      # auto-fix where possible
```

### Prettier

Prettier enforces consistent formatting. Configuration is in `.prettierrc`.

```bash
npm run format:check  # check only (used in CI)
npm run format        # auto-format
```

### TypeScript

`tsconfig.json` is set to `strict` mode. The `npm run build` command type-checks the project without emitting files.

---

## Git Workflow

1. **Branch naming**: `feature/<short-description>`, `fix/<short-description>`, `chore/<short-description>`
2. **Commit messages**: Use [Conventional Commits](https://www.conventionalcommits.org/) format:
   - `feat: add agent registration API`
   - `fix: handle null credentials in vault`
   - `chore: update ESLint config`
3. **Pull Requests**: All PRs must pass the CI pipeline (lint, format check, type check, tests) before merging.
4. **No direct pushes to `main`**: All changes must go through a PR.
