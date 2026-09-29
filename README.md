# C++ Coding Style

This repository contains a C++ coding standard and AI guidance files intended to help coding agents follow a consistent style when generating or modifying C++ code.

## Contents

- `cpp_coding_style.md` — full coding standard
- `AGENTS.md` — repository instructions for coding agents such as Codex
- `.github/copilot-instructions.md` — GitHub Copilot instructions

## Purpose

The goal is to keep C++ code in this project:

- readable
- consistent
- maintainable
- explicit
- safe and predictable

The style is based on common C++ engineering practice and the Google C++ Style Guide direction, adapted for project use.

## How AI tools use this repository

The repository includes agent instruction files so that Codex, Copilot, and similar coding assistants can follow these rules automatically when working in this repo.

These rules cover:

- naming conventions
- indentation and formatting
- class and function design
- smart pointers and RAII
- pointer/null handling
- error handling and early returns
- constants and enums
- resource ownership and lifetime
- code review expectations

## Suggested usage

When making changes in this repository:

1. Read `cpp_coding_style.md` for full rules.
2. Follow the repository agent guidance in `AGENTS.md`.
3. Keep code simple, explicit, and consistent with the existing style.
4. Avoid build artifacts, temporary files, and debug logs.

## Example rules enforced by the repo instructions

- 2-space indentation, no tabs
- `snake_case` for variables
- `snake_case_` for member variables
- `PascalCase` for classes and functions
- `kPascalCase` for constants
- `enum class` preferred
- `nullptr` preferred over `NULL`
- no `using namespace std;`
- prefer RAII and smart pointers
- avoid C-style casts
- prefer early returns and clear function responsibilities

## Reference

- `cpp_coding_style.md`
- `AGENTS.md`
- `.github/copilot-instructions.md`

## Notes

This repository is intentionally lightweight and documentation-first. It is suitable as a source of truth for AI-assisted C++ development and can later be extended with linting, CI validation, or a structured automated skill layer.
