# 🏷️ Naming conventions

### TS / JS

- Identifiers should be self-explanatory and describe value.
- Identifiers (variables, functions, methods): **camelCase**.
- Booleans: `is` or `has` prefix (For ReactJS Projects).
- Functions: nouns and verbs prefixes (Flexible) i.e. `loadArticles()`.
- Global constants: **UPPER_SNAKE_CASE**
- Classes: **PascalCase**
- Types and interfaces: **PascalCase**
- Components: **PascalCase**
- Filenames: **kebab-case**
  - Except for when there is a default export, then use the default export's name and casing.
- Private functions: **prefix with \_**
- **No** abbreviations unless they are widely understood.
  - If an abbreviation is used, use normal casing i.e., `ArticleDto`.
- **No** single-letter variables (only for loops and events, i.e., `e`, `i`).

### (S)CSS

**General**

- Use Stylelint
- Use comments when very specific selectors are needed

**No nesting preferred**

- Don't:

```
.card {
  .title {
    .link {
      // Properties
    }
  }
}
```

- Do:

```
.card {
  // Properties
}
.title {
  // Properties
}
.link {
  // Properties
}
```

**Selectors using kebab-case**

- Don't: `class="mostReadPost"`
- Do: `class="most-read-post"`

**Don't use an abbrevation in the classnames (as everyone can interpret it differently)**

- Don't: `class="crsl"`
- Do: `class="carousel"`

**Avoid styling by id**

- Don't: `id="button"`
- Do: `class="button"`

**Use meaningful names**

- Don't: `class="section"`
- Do: `class="article-list"`

**Chain modifier classes**

- Don't: `class="button button-red"`
- Do: `class="button red"`

**Prefix state classes with 'is'**

- Don't: `class="button button-disable"`
- Do: `class="button is-disabled"`

**Keep it short but do sacrifice it for the sake of meaningful names**

- Don't: `class="most-read-blog-post-list-item"`
- Do: `class="most-read-post"`

**Avoid the use of !important**

- Don't: `color: var(--c-red) !important`
- Do: `color: var(--c-red)`

**Preferably style by classname**

- Don't:

```
li {
  a {
    // properties
  }
}
```

- Do:

```
.link {
  // properties
}
```

### Best practices

- Use meaningful and descriptive names for variables, functions, types, and classes.
- Use consistent naming throughout your code.
- If the name of an interface or type is already used for something else, append `Entity` to it.
