# 🗄️ Project structure

```
.
├── src/
│   ├── assets/
│   │   └── images
│   ├── components/
│   │   ├── Button/
│   │   │   ├── Button.tsx
│   │   │   └── Button.module.scss
│   │   └── Icon/
│   │       ├── assets
│   │       ├── Icon.tsx
│   │       └── Icon.module.scss
│   ├── config
│   ├── connectors/
│   │   └── Posts/
│   │       ├── Posts.connector.tsx
│   │       └── Posts.utils.tsx
│   ├── hooks/
│   │   └── useUser.ts
│   ├── routes/
│   │   ├── routes.tsx
│   │   └── loaders/
│   │       └── postsLoader.ts
│   ├── services/
│   │   ├── api.ts
│   │   └── apiDtos.ts
│   ├── store/
│   │   └── user/
│   │       ├── userReducer.ts
│   │       └── userActions.ts
│   ├── styles/
│   │   ├── global.scss
│   │   ├── variables
│   │   ├── mixins
│   │   └── typography
│   └── utils/
│       ├── date.ts
│       ├── array.ts
│       └── object.ts
├── App.tsx
└── index.ts
```
