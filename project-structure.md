```
.
├── src/
│   ├── assets/                                     # Contains all the static files such as images, fonts, etc.
│   │   └── images
│   ├── components/                                 # Shared components used across the entire application
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   └── Button.module.scss
│   │   ├── Card/
│   │   ├── Icon/
│   │   ├── Pagination/
│   │   └── TodoListItem/
│   ├── config                                      # global app config (global constants/enums/etc.)
│   ├── connectors/                                 # The only component type where it's allowed to use api and/or store hooks
│   │   └── Todos/
│   │       ├── TodosListConnector.tsx
│   │       ├── TodosHeaderConnector.tsx
│   │       └── TodosPaginationConnector.tsx
│   ├── hooks/                                      # Hooks used across the entire application
│   │   ├── useUser.ts
│   ├── layouts/                                     # Initial component used within a route to render the layout
│   │   └── TodoLayout
│   │           ├── TodoLayout.module.scss
│   │           └── TodoLayout.tsx
│   ├── routes/
│   │   └── loaders/
│   │       └── loadTodos.ts
│   ├── services/                                   # API related code
│   │   ├── dto/
│   │   │   ├── types.ts
│   │   │   └── utils/
│   │   │       └── todo.ts
│   │   └── api.ts
│   ├── store/                                      # global state stores (redux/recoil/etc.)
│   │   └── user/
│   ├── styles/                                     # global styling
│   │   ├── global.scss
│   │   ├── helpers.scss
│   │   ├── variables
│   │   ├── mixins
│   │   └── typography
│   └── utils/                                      # shared utility functions
│       ├── date.ts
│       ├── array.ts
│       └── formatMoney.ts
├── App.tsx                                         # Initial app component, always cluttered with initialization scripts
└── index.ts
```
