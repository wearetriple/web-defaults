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
│       └── TodoListItem.module.scss
├── connectors/                           # The only component type where it's allowed to use APIs and/or stores
│   ├── TodosFilters/
│   │   ├── utils/
│   │   │   └── useTodoFilters.ts
│   │   ├── TodosFilters.module.scss
│   │   └── TodosFilters.tsx
│   └── TodosList/
│       ├── TodosList.module.scss
│       └── TodosList.tsx
├── hooks/                                # Hooks used across the entire application
│   └── use-user.ts
├── layouts/                              # Initial component used within a route to render the layout (React specific)
│   └── TodosLayout/
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
│   └── format-money.ts
├── App.tsx                               # Initial app component, always cluttered with initialization scripts
└── index.ts
```

### Example: Application scaling by folders per feature

If you want to make your application more scalable it's optional to create a feature-based folder structure. It will allow you to keep functionalities scoped to a feature and not mix its declarations with shared code. This can make it easier to maintain than a flat folder structure with many files.

```
src/features/chat-bot/
├── assets/
│   └── images/
├── components/
│   ├── PromptInput/
│   │   ├── PromptInput.tsx
│   │   └── PromptInput.module.scss
│   ├── ChatHistory/
│   │   ├── ChatHistory.tsx
│   │   └── ChatHistory.module.scss
│   └── PromptResponse/
│       ├── PromptResponse.tsx
│       └── PromptResponse.module.scss
├── connectors/
│   └── Chatbot/
│       └── ChatbotConnector.tsx
├── hooks/
│   └── use-chat-history.ts
├── api/
│   ├── api.ts
│   └── api-dtos.ts
├── store/
└── utils
```

when do I create a separate api folder?

- when the feature is the only part there the api is being used

what should exist in the root folder structure?

- shared components
- shared api
- shared store
