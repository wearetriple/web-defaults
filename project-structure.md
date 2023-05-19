```
src
  assets                                 # Contains all the static files such as images, fonts, etc.
    images/
  components                             # Shared components used across the entire application
    Button
      Button.tsx
      Button.module.scss
    Card/
    Icon/
    Header/
    TodoListItem
      TodoListItem.tsx
      TodoListItem.module.scss
  connectors                             # The only component type where it's allowed to use apis and/or stores
    TodosFilters/
    TodosList
      TodosList.module.scss
      TodosList.tsx
  hooks                                  # Hooks used across the entire application
    useUser.tsx
  layouts                                # Initial component used within a route to render the layout (React specific)
    TodoLayout.module.scss
    TodoLayout.tsx
  routes/                                # Routing configuration with loader function to trigger initial api loads
  api                                    # API related code
    dto.ts
    api.ts
  store/                                 # global state stores (appStore/userStore/etc.)
  styles
    global.scss
    utils.scss
    variables
    mixins
    typography
  utils                                  # shared utility functions
    date.ts
    array.ts
    object.ts
    formatMoney.ts
App.tsx                                  # Initial app component, always cluttered with initialization scripts
index.ts
```
