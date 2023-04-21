# Data flow

## Folder structure

```
.
└── src/
    ├── core/
    │   ├── services/
    │   │   ├── api-dto.ts
    │   │   └── api.ts
    │   └── store/
    │       ├── entities/
    │       │   └── [entity].ts
    │       └── configure.ts
    └── ui/
        └── components/
            └── [component]/
                ├── [component].connector.tsx
                └── [component].tsx
```

### Flow

```mermaid
flowchart TD
    dto -->|import types| api -->|fetch endpoint| connector -.->|optional: transform data| transformer -.->|connect data to component| component
    connector -->|connect data to component| component
```

### services/api-dto.ts
```ts
export type ApiGetResponse = {
  "entity/[id]/": EntityDto;
};

type EntityDto = {
  id: string;
  title: string;
  body: string;
};
```
### services/api.ts
```ts
const api = {
  get<T extends keyof ApiGetResponse>(
    path: T,
    config?: Config
  ): Promise<ApiResponse<ApiGetResponse[T]>> {
    return wrapped("GET", endpoint + path, config || {});
  },
};
export default api;
```
### store/entities/[entity].ts
```ts
import { createSlice, PayloadAction } from "@reduxjs/toolkit";

const entitiesSlice = createSlice({
  name: "entities",
  initialState: { selected: undefined },
  reducers: {
    selectEntity: (state, action: PayloadAction<string>) => {
      state.selected = action.payload;
    },
  },
});

export const { selectEntity } = entitiesSlice.actions;

export default entitiesSlice.reducer;

```
### components/[component].connector.tsx
```ts
const EntityConnector = ({ id }) => {
  const { data } = useApi(`entity/${id}`);
  const dispatch = useDispatch();
  const entitySelected = useSelector(state => state.entities.selected === id);

  const onSelectEntity = (id: string) => {
    dispatch(selectEntity(id));
  };

  return (
    <EntityComponent
      id={data.id}
      selected={entitySelected}
      title={data.title}
      body={data.body}
      onSelect={onSelectEntity}
    />
  );
};
```
### components/[component].tsx
```tsx
const EntityComponent = ({ id, selected, title, body, onSelect }) => {
  return (
    <Touchable onPress={() => onSelect(id)}>
      <View style={[selected && $.selected]}>
        <Heading>{title}</Heading>
        <Text>{body}</Text>
      </View>
    </Touchable>
  );
};
```
