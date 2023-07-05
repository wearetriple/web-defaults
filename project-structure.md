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
│   └── useUser.tsx
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
│   └── formatMoney.ts
├── App.tsx                               # Initial app component, always cluttered with initialization scripts
└── index.ts
```

In order to scale the application in the it's optional to keep most of the code inside the features folder, which should contain different feature-based things. Every feature folder should contain domain specific code for a given feature. This will allow you to keep functionalities scoped to a feature and not mix its declarations with shared things. This is much easier to maintain than a flat folder structure with many files.

```
src/features/chatBot/
├── assets
├── images
├── components/
│   ├── PromptInput/
│   │   ├── PromptInput.tsx
│   │   └── PromptInput.module.scss
│   ├── ChatHistory/
│   │   ├── ChatHistory.tsx
│   │   └── ChatHistory.module.scss
│   └── PromptResonse/
│       ├── PromptResonse.tsx
│       └── PromptResonse.module.scss
├── connectors/
│   └── Chatbot/
│       ├── ChatbotConnector.tsx
│       └── ChatbotUtils.tsx
├── hooks/
│   └── useChatHistory.ts
├── routes/
│   ├── routes.tsx
│   └── loaders/
│       └── postsLoader.ts
├── api/
│   ├── api.ts
│   └── apiDtos.ts
├── store/
│   └── user/
│       ├── chatBotReducer.ts
│       └── chatBotActions.ts
└── utils
```
