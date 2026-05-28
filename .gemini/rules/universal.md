# Universal Rules

These rules apply to every file in the project regardless of language or type.

## File Size

- **Hard limit: 50 lines of code per file.** Blank lines and comments don't count.
- When a file approaches 40 lines, plan how it will be split before adding more.
- Splitting strategies: extract reusable behavior to a new script under `res://systems/`, extract data into a new `Resource`, or split a glue script by phase (e.g. `player_input.gd` + `player_motion.gd`).

## Modularity

- **One responsibility per file.** If you can't describe what a file does in one sentence without "and", split it.
- **Keep the spaghetti on the plate.** Internal complexity inside a module is fine. Complexity that crosses module boundaries is not.
- **Write every system as if you will reuse it in another project**, even when you won't. This forces clean boundaries.
- **Independent systems never reference each other directly.** Two systems that need each other are either one system, or they need a glue script.

## Comments

- No inline comments inside function or method bodies.
- Docstrings or header comments go strictly above the function, method, or class they describe.
- All comments in English.
- No emojis anywhere — comments, docstrings, code, strings, file names, commit messages.

## Security

- Never hardcode API keys, tokens, passwords, or external service URLs.
- Load secrets from environment variables at startup. Document required env vars in `README.md`.
- Validate every value entering the simulation from outside: save files, network responses, environment variables, user input, scraped data.
- Treat save data as untrusted input. Players will edit it.

## When in Doubt

If a piece of code does not clearly fit one category (reusable system, glue, data resource, view component), stop and decide which it is before writing more. Most architecture problems start with code that was never assigned a category.
