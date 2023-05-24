```
src/
├── assets/                               # Contains all the static files such as images, fonts, etc.
│   └── images/
├── components/                           # Shared components used across the entire application
│   ├── Button/
│   │   ├── Button.tsx
│   │   └── Button.module.scss
│   ├── Card/
│   ├── Icon/
│   ├── Header/
│   └── TodoListItem/
│       ├── TodoListItem.tsx
├── connectors/                           # The only component type where it's allowed to use apis and/or stores
│   ├── TodoFilters/
│   │   ├── utils/
│   │   │   └── useTodoFilters.ts
│   │   ├── TodoFilters.module.scss
│   │   └── TodoFilters.tsx
│   └── TodoList/
│       ├── TodoList.module.scss
│       └── TodoList.tsx
├── hooks/                                # Hooks used across the entire application
│   └── useUser.tsx
├── layouts/                              # Initial component used within a route to render the layout (React specific)
│   └── TodoLayout/
│       ├── TodoLayout.module.scss
│       └── TodoLayout.tsx
├── routes/                               # Routing configuration with a loader function to trigger initial API loads
├── api/                                  # API related code
│   ├── dto.ts
│   └── api.ts
├── store/                                # Global state stores (appStore/userStore/etc.)
├── styles/
│   ├── global.scss
│   ├── utils.scss
│   ├── variables
│   ├── mixins
│   └── typography
├── utils/                                # Shared utility functions
│   ├── date.ts
│   ├── array.ts
│   ├── object.ts
│   └── formatMoney.ts
├── App.tsx                               # Initial app component, always cluttered with initialization scripts
└── index.ts
```
