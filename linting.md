# 🤖 Linting

## Linting JS

Linting is the best way to keep your code clean and consistent. Within Triple, we have a default setup for ESLint combined with Prettier. This will make sure that your code is consistent, and you don't have to worry about formatting your code.

The config and instructions can be found here:
[https://www.npmjs.com/package/eslint-config-triple](https://www.npmjs.com/package/eslint-config-triple)

## Linting CSS

### Introduction

Linting CSS is possible with a library called Stylelint. By itself, it doesn't lint Sass files, but this can be included with an extra parser and by telling your editor to use Stylelint. It is also recommended to add this to your package.json tasks for CI.

### Installation

1. Install these packages _(in the future we will create a separate config package)_.

   ```sh
   npm install -D \
     stylelint \
     stylelint-config-clean-order \
     stylelint-config-standard-scss \
     stylelint-prettier
   ```

2. Add the Stylelint config file to the project _(in the future we will create a separate config package)_.

   .stylelintrc

   ```json
   {
     "extends": [
         "stylelint-config-standard-scss",
         "stylelint-config-clean-order",
         "stylelint-prettier/recommended"
     ],
     "customSyntax": "postcss-scss",
     "overrides": [
       {
         "files": ["**/*.scss"],
         "customSyntax": "postcss-scss"
       }
     ]
   }
   ```

3. _(optional for VS Code users)_ Add or append Visual Studio Code options to recognize Stylelint as its formatter for both CSS and SCSS files.

   `.vscode/settings.json`

   ```json
   {
     "stylelint.validate": ["css", "scss"],
     "[css]": {
       "editor.defaultFormatter": "stylelint.vscode-stylelint"
     },
     "[scss]": {
       "editor.defaultFormatter": "stylelint.vscode-stylelint"
     },
     "css.validate": false,
     "less.validate": false,
     "scss.validate": false,
     "editor.codeActionsOnSave": {
       "source.fixAll.stylelint": true
     }
   }
   ```

4. Append the script commands to your package.json so they can be used by your CI or developer (when they aren't using VS Code, they can still apply fixes and checks). It is also recommended to include it in your `npm test` command.

   `package.json`

   ```json
   ...
   "scripts": {
       "lint": "stylelint \"src/**/*.{css,scss}\"",
       "format": "npm run lint -- --fix"
   }
   ...
   ```

5. _(optional for VS Code users)_ Add the extension [Stylelint][stylelint] to Visual Studio Code.

### Usage

With all this set, you should have everything lintable. You can check if there are errors with `npm run lint` or even apply an autofix with `npm run lint:fix`. This will still throw an error if there are errors that can't be autofixed.

[stylelint]: https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint
