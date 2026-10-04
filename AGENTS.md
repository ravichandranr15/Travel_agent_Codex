# Repository Guidelines

## Project Structure & Module Organization

This repository is currently an empty scaffold: no application source, tests, or asset directories are present. As the project grows, keep production code in a clearly named source directory (such as `src/`), tests in `tests/` or alongside the code, and static assets in `assets/`. Update this guide when the actual layout is established.

## Build, Test, and Development Commands

There is no build system or runnable application configured yet. Once project tooling is added, document the canonical install, local development, build, and test commands here; keep them aligned with checked-in scripts and configuration (for example, `npm run dev` only if a matching script exists).

## Coding Style & Naming Conventions

Follow the formatter and linter configured for the chosen language, and keep formatting changes consistent with nearby files. Use descriptive names: `PascalCase` for types where idiomatic, `camelCase` for functions and variables in JavaScript or TypeScript, and `snake_case` in Python. Avoid adding a formatter or linter without recording its use in project configuration and this guide.

## Testing Guidelines

No test framework or coverage threshold is configured. Add tests with the project’s chosen framework, use clear names that describe the behavior under test, and include the command to run them in the relevant project scripts and this guide. Run relevant checks before submitting changes.

## Commit & Pull Request Guidelines

Git history is not available in this scaffold, so no repository-specific commit convention can be inferred. Use concise, imperative commit subjects (for example, `Add itinerary parser`). Pull requests should explain the change and its motivation, list validation performed, and include screenshots for user-facing visual changes. Link related issues when applicable.

## Configuration & Secrets

Keep credentials and machine-specific settings out of source control. Use documented environment variables and provide safe examples (such as a `.env.example`) when configuration is introduced; never commit real secrets.
