# 🗄️ Project structure

```
.
├── src/
│   ├── assets/                           # assets folder can contain all the static files such as images, fonts, etc.
│   │   └── images
│   ├── components/                       # shared components used across the entire application
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   └── Button.module.scss
│   │   └── Icon/
│   │       ├── assets
│   │       ├── Icon.tsx
│   │       └── Icon.module.scss
│   ├── config                            # all the global configuration, env variables etc. get exported from here and used in the app
│   ├── connectors/
│   │   └── Posts/
│   │       ├── Posts.connector.tsx
│   │       └── Posts.utils.tsx
│   ├── hooks/                            # shared hooks used across the entire application
│   │   └── useUser.ts
│   ├── routes/                           # routes configuration
│   │   ├── routes.tsx
│   │   └── loaders/                      # route loaders for (pre)loading data based on route navigation
│   │       └── postsLoader.ts
│   ├── services/                         # services needed for communication with APIs
│   │   ├── api.ts
│   │   └── apiDtos.ts
│   ├── store/                            # global app state stores
│   │   └── user/
│   │       ├── userReducer.ts
│   │       └── userActions.ts
│   ├── styles/                           # global app styling / initial theming setup / mixins
│   │   ├── global.scss
│   │   ├── variables
│   │   ├── mixins
│   │   └── typography
│   └── utils/                            # shared utility functions
│       ├── date.ts
│       ├── array.ts
│       └── object.ts
├── App.tsx
└── index.ts
```
