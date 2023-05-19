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
│   │   │   ├── Card.tsx
│   │   │   └── Card.module.scss
│   │   ├── Icon/
│   │   │   ├── assets/
│   │   │   │   ├── chevron.svg
│   │   │   │   ├── check.svg
│   │   │   │   └── ...
│   │   │   ├── Icon.tsx
│   │   │   └── Icon.module.scss
│   │   ├── Header/
│   │   │   ├── Header.tsx
│   │   │   └── Header.module.scss
│   │   ├── Pagination/
│   │   │   ├── Pagination.tsx
│   │   │   └── Pagination.module.scss
│   │   ├── ListItem/
│   │   │   ├── ListItem.tsx
│   │   │   └── ListItem.module.scss
│   │   └── Todo/                                   # Todo specific components
│   │       ├── TodoListItem.tsx
│   │       └── TodoListItem.module.scss
│   ├── config                                      # global config (types/enums/etc.)
│   ├── connectors/                                 # The only component type where it's allowed to use api and/or store hooks
│   │   └── Todos/
│   │       ├── TodosListConnector.tsx
│   │       ├── TodosHeaderConnector.tsx
│   │       └── TodosPaginationConnector.tsx
│   ├── hooks/                                      # Hooks used across the entire application
│   │   └── useUser.ts
│   ├── layout/                                     # Initial component used within a route to render the layout
│   │   └── TodoLayout.tsx
│   ├── routes/                                     # Routes configuration
│   │   ├── Routes.tsx
│   │   └── loaders/                                # (async) data loading hook within routes
│   │       └── todoLoader.ts
│   ├── services/                                   # API related code
│   │   ├── dto/
│   │   │   ├── types.ts
│   │   │   └── utils/                              # shared utility functions from DTO to render
│   │   │       └── todo.ts
│   │   └── api.ts
│   ├── store/                                      # global state stores (redux/recoil/etc.)
│   │   └── user/
│   │       ├── userReducer.ts
│   │       └── userActions.ts
│   ├── styles/                                     # global styling
│   │   ├── global.scss
│   │   ├── variables
│   │   ├── mixins
│   │   └── typography
│   └── utils/                                      # shared utility functions
│       ├── date.ts
│       ├── array.ts
│       └── object.ts
├── App.tsx
└── index.ts
```
