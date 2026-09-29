# AGENTS.md

This repository is a C++ coding style guide for AI-assisted development.

When working in this repository, follow the rules in `cpp_coding_style.md` and apply them to any generated or modified C++ code.

## Core rules

- Use 2-space indentation. Never use tabs.
- Use `snake_case` for variables and `snake_case_` for member variables.
- Use `PascalCase` for class names, structs, and function names.
- Use `kPascalCase` for constants and enum values.
- Prefer `enum class` over plain `enum`.
- Use `nullptr` instead of `NULL` or `0` for null pointers.
- Do not use `using namespace std;` in headers or generally in project code.
- Prefer RAII and smart pointers (`std::unique_ptr`, `std::shared_ptr`, `std::weak_ptr`) over raw ownership models.
- Prefer explicit C++ casts (`static_cast`, `dynamic_cast`, etc.) instead of C-style casts.
- Keep functions single-purpose and use early returns for error conditions.
- Prefer `std::vector`, `std::array`, `std::string`, and `std::chrono` over raw arrays and ambiguous integer time values.
- Avoid magic numbers; use named `constexpr` values.
- Do not rely on undefined behavior, dangling pointers, or uninitialized values.
- Prefer `std::make_unique()` and `std::make_shared()` over `new`/`delete` in normal business logic.
- Use `override` for overridden virtual functions.
- Keep include ordering consistent: local headers, C headers, C++ headers, third-party, project headers.
- Use `#pragma once` or a consistent project include guard pattern, but avoid mixing both styles.
- Do not add debug artifacts, compiled outputs, or temporary files to the repository.

## Project intent

The goal is to keep code readable, maintainable, and consistent. Favor clarity over cleverness, and prefer explicit, well-named structures over clever shortcuts.

## Reference

- `cpp_coding_style.md` — complete coding standard

## When generating code

- Keep names descriptive, not abbreviated unless the abbreviation is standard and widely understood.
- Use early returns and guard clauses where they improve clarity.
- Favor simple logic over deep nesting.
- Add comments only when clarifying intent, constraints, or non-obvious design choices.
- Keep public API documentation clear and precise.
- Prefer tests that are independent, reproducible, and informative on failure.

## Default behavior for AI assistance

If a coding task is ambiguous, prefer the most explicit, conventional, and maintainable C++ implementation that matches this repository's style guide rather than a more clever or terse solution.
