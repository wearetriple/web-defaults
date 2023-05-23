# 🏷️ Naming conventions

### TS / JS

- Identifiers should be self-explanatory and describe value.
- Identifiers (variables, functions, methods): **camelCase**.
- Booleans: `is` or `has` prefix (For ReactJS Projects).
- Functions: nouns and verbs prefixes (Flexible) i.e. `loadArticles()`.
- Global constants: **UPPER_SNAKE_CASE**.
- Classes: **PascalCase**.
- Types and interfaces: **PascalCase**.
- Components: **PascalCase**.
- Filenames: **kebab-case**.
  - Except for when there is a default export, then use the default export's name and casing.
- Private functions: **prefix with \_**.
- **No** abbreviations unless they are widely understood.
  - If an abbreviation is used, use normal casing i.e., `ArticleDto`.
- **No** single-letter variables (only for loops and events, i.e., `e`, `i`).

### (S)CSS

- No nesting preferred.
- Selectors using **kebab-case**.
- Use Stylelint.

### Best practices

- Use meaningful and descriptive names for variables, functions, types, and classes.
- Use consistent naming throughout your code.
- If the name of an interface or type is already used for something else, append `Entity` to it.
