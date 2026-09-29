# Copilot Instructions

This repository defines a C++ coding standard. When creating or modifying C++ code, follow the rules in `cpp_coding_style.md` and the repo-specific guidance below.

## Required style

- Indent with 2 spaces; no tabs.
- Use `snake_case` for variables, except member variables use `snake_case_`.
- Use `PascalCase` for classes, structs, and function names.
- Use `kPascalCase` for constants and enum values.
- Prefer `enum class`.
- Use `nullptr`, not `NULL` or `0`.
- Do not use `using namespace std;`.
- Prefer RAII and smart pointers.
- Avoid C-style casts.
- Keep code simple, readable, and explicit.
- Prefer early returns and small single-purpose functions.

## Design expectations

- Prefer clear ownership semantics.
- Use standard C++ containers and types first.
- Avoid unnecessary templates, inheritance, or abstraction.
- Keep lifecycle and resource ownership explicit.
- Use comments to explain why, not what.

## Reference

- `cpp_coding_style.md`

## Repository rule

Do not commit build artifacts, temporary files, or debug logs.
