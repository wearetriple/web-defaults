# 📡 Data
The application you are building will transform data to a user interface using a framework like React or Svelte. Meaning, you will retrieve data from one or more sources like an API, state management library, or query params. It forms a layer over your application where your code knows how to form that layer into a workable UI.

Examples where a layer of data can exist:
- In a component, also known as component state and accessed using hooks in React or a variable in Svelte.
- On a server, also known as server state and accessed using an API.
- In route parameters, also known as URL state and accessed using the Location Browser API.

Two keywords that are important in a data layer:
- __Store__: Where data is stored, for example, a Firebase Database, indexedDB, localStore, React Query, Apollo Client Cache, Redux Store, etc.
- __State__: A snapshot of the store at a point in time representing the current state of the store.

## Index
- [What is a global store?](#what-is-a-global-store)
- [What is a state?](#what-is-a-state)
  - [Component state](#component-state)
  - [Application state](#application-state)
  - [Server (cache) state](#server-cache-state)
  - [Route state](#route-state)
- [From state to component](#from-state-to-component)
  - [Connecting or displaying data](#connecting-or-displaying-data)
  - [State management](#state-management)
  - [Transform/formatting data](#transformformatting-data)
  - [When to use a connector?](#when-to-use-a-connector)
  - [When to use a transformer?](#when-to-use-a-transformer)

## Useful links
- [💬 Response Typing](response-typing.md)
- [🗄️ Project structure](project-structure.md)
- [🧱 Components](components.md)

## What is a global store?
In state management terms, a (global) store is an object that holds the state of an application. It is a centralized place where you can store, update, and retrieve data that is used throughout your application.

In a typical state management system, the store is responsible for maintaining the application state, which consists of all the data and values that your application needs to function. This includes things like user data, application settings, and other important data.

## What is a state?
Within an application, whether it be built with React (Native) or Svelte, there are different types of state. So there is not a single centralized state where all your data lives:
<a id='component-state'></a>

- __Component state__: A component is a self-contained, reusable piece of code that can be used to create a UI element, such as a button, form, or menu. The state of a component represents the values that are specific to that component, which can change over time and affect how the component is rendered.

<a id='application-state'></a>

- __Application state__: If you want to keep state on a more global level that doesn't live server-side, you want to consider Application state. State that can represent stuff like:
  - Theming
  - Settings
  - Notifications
  - Open modals
  - etc.
  
  You need to consider if your state needs to live on app level or can be nested deeper down your app tree. Sometimes a state only is relevant to specific subset of pages. In that case define it on a lower level to prevent dropping performance for the whole app.

<a id='server-cache-state'></a>

- __Server (cache) state__: When fetching data from an external API, we can store that data in a client-side cache:
  - Pros:
    - Reduces the number of API calls to the server.
    - Allows data to be available while new data is being fetched.
    - Enables easy reuse of the same API query multiple times without multiple fetches.
  - Cons:
    - Need to consider cache invalidation.
    - Need to resolve conflicts between existing and incoming data in the cache.

<a id='route-state'></a>

- __Route state__: State that is stored in the route. For web applications, it can be found in the address bar of the browser. Within React Native, it refers to route parameters for each screen (stack/tab). Elements you will usually find in a route state include:
  - Path
  - Query parameters
  - Hash

## From state to component
When examining how applications work, it can be stated that a user always starts with a route state:
- The user navigates to a page.
- The user reloads a page.
- The user comes from an external source (like a deep link).

Consider this flow for your application, starting from a route and ending in component(s):

```mermaid
flowchart TD
    api -->|fetch & store| cache -->|set in page props| layout
    connector-.->|optional: transform data| transformer -->|connect data to component| component
    connector -->|connect data to component| component
    entities -->|configure entities| store -->|connect data and dispatches| layout
    params --> loader
    routeState --> serverState
    subgraph layout
    connector
    transformer
    component
    end
    subgraph routeState
    loader
    params
    end
    subgraph applicationState
    entities
    store
    end
    subgraph serverState
    api
    cache
    end
    style connector stroke:lime,stroke-width:2px
    style loader stroke:lime,stroke-width:2px
    style component stroke:lime,stroke-width:2px
    style layout stroke:lime,stroke-width:2px
    style routeState stroke:orange,stroke-width:2px
    style serverState stroke:orange,stroke-width:2px
    style applicationState stroke:orange,stroke-width:2px
    style transformer stroke:yellow,stroke-width:2px
```

> Looking for how to structure this flow in your application, see [project structure](project-structure.md) documentation.

### ![#lime](https://placehold.co/15x15/lime/lime.png) Connecting or displaying data

| Element      | Description                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| Loader    | Based on the route and its params, it can load data. When looking at Next.js, Svelte, or React Router v6, they expose a loader function based on each route. |
| Layout    | Structures components and connectors to display a page/screen to the user. It is always included through a route.                                          |
| Connector | Connects data from the server or application state to components and optionally transforms/formats it. It also handles the propagated actions from components. It keeps components 'dumb' and functional. Read more: [When to use a connector](#when-to-use-a-connector).                      |
| Component | A 'dumb' component only responsible for displaying data and propagating actions to its connector or layout. Read more: [What is a dumb component?](components.md#what-is-dumb-component)                                          |

To make it easier, refer to this overview to see the scope for each element:

|           | Route State | Server State | Application State | Component State | Transformer |
|-----------|-------------|--------------|-------------------|-----------------|-------------|
| Loader    | ✅           | ✅            | ⛔️                | ⛔️              | ⛔️          |
| Layout    | ⛔️          | ✅            | ✅                 | ⛔️              | ⛔️          |
| Connector | ⛔️          | ✅            | ✅                 | ✅               | ✅           |
| Component | ⛔️          | ⛔️           | ⛔️                | ✅               | ⛔️          |


### ![#orange](https://placehold.co/15x15/orange/orange.png) State management

| Element              | Description                                                                           |
|-------------------|---------------------------------------------------------------------------------------|
| Route State       | Handled by your solution of choice: Next.js, Svelte, or React Router.                  |
| Server State      | Handled by your solution of choice: Vanilla fetch, React Query, Apollo, etc.          |
| Application State | Handled by your solution of choice: React Context, Svelte stores, Redux Toolkit, etc. |


### ![#yellow](https://placehold.co/15x15/yellow/yellow.png) Transform/formatting data

| Element    | Description                                                                                                                                                           |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Transformer | A utility function for transforming/formatting data to display prices, dates, or transforming arrays to flatten them or calculate a totalPrice for multiple order lines. Read more: [When to use a transformer](#when-to-use-a-transformer). |


### Examples

<details open>
<summary>React with React Router DOM v6</summary>

First, start with the entry point of your app: the Route State:
- It has an initial fetch in the loader.
- It fetches todos based on the slug of the current page.
- It connects the server state to the route state.
- It connects a layout to the route.
```ts
// Element: Loader
export function todosLoader({ params }: TodosRoute) {
  // Route state -> Connect route params to fetch from server state
  // Server state -> API service will fetch the server (cache) state
  return api.get(`/api/todos/${params.slug}`);
}
```
Now set up your router to use the loader, the navigation path, and layout:
```tsx
// State manager: Route
const router = createBrowserRouter([
  {
    path: "/todos/:slug",
    // imported from loaders
    loader: todosLoader,
    // using id to connect route state to hooks
    id: "TodosBySlug",
    // imported from layouts
    element: <TodosLayout />,
  },
]);

ReactDOM.createRoot(el).render(<RouterProvider router={router} />);
```
Within the layout, the components are structured into a page/screen:
- It uses the server state from the route.
- It imports `TodoHeader` as a dumb component and passes it the page header image.
- It fetches `rightsAndRoles` from the server (cache) state to show/hide the creation option on the screen.
- It imports `TodoListConnector` to display the list of Todos.
```tsx
// Element: Layout
const TodosLayout = () => {
  // Server state -> Similar to route state,
  // but the return of loader data is from the server (cache) state.
  const todosBySlug = useRouteLoaderData("TodosBySlug");
  // Server state -> Get rights and roles from server or cache.
  const { data: rightsAndRoles } = useQuery(QueryRightsAndRoles);

  return (
    // Structures components in a layout
    <section className={$.container}>
      <div className={$.flex}>
        <TodoHeader image={todosBySlug.header.image.url} />
        <TodoListConnector />
      </div>
      {/* Hide/show todo creation based on rights of the current user */}
      {rightsAndRoles.includes("todo-creation") && (
        <div className={$.sticky}>
          <TodoCreate />
        </div>
      )}
    </section>
  );
};
```
The connector is set up to load a list of TodoItem components:
- It loads the todos from the server state (the route loader).
- It connects extra data relevant to this list of components: the Todo Assignee.
- It handles the toggle action.
- It selects the `showTodoTimeStamp` setting from the application state.
- It formats the timestamp to a readable date string.
```tsx
// Element: Connector
const TodoListConnector = () => {
  // Server state -> Similar to route state,
  // but the return of loader data is from the server (cache) state.
  const todosBySlug = useRouteLoaderData("TodosBySlug");
  // Server state -> Connect extra data to TodoItem
  const { data: todoAssignees } = useQuery(QueryTodoAssignees, {
    variables: {
      slug: todosBySlug.slug,
    },
  });
  // Application state -> Connect app settings to TodoItem
  const dispatch = useDispatch();
  const showTodoTimeStamp = useSelector(
    (state) => state.appSettings.showTodoTimeStamp
  );

  // Handle action of TodoItem, update application state
  const onToggle = (id: string, checked: boolean) => {
    dispatch(setTodoChecked(id, !checked));
  };

  return (
    <>
      {todosBySlug.todos.map((todo) => (
        <TodoItem
          title={todo.title}
          onToggle={() => onToggle(todo.id, todo.checked)}
          checked={todo.checked}
          assignedTo={todoAssignees[todo.id].fullName}
          assignedProfilePic={todoAssignees[todo.id].image}
          // Here we transform data if needed.
          // In this case, we want to format time to a readable format.
          time={showTodoTimeStamp ? formatTime(todo.time) : null}
        />
      ))}
    </>
  );
};
```
Finally, a TodoItem component is created:
- It displays props that are passed to the component.
- It imports another 'dumb' component to display the Avatar of the assignee.
- It propagates the `onToggle` event.
```tsx
// Element: Component
const TodoItem = ({
  title,
  checked,
  onToggle,
  time,
  assignedTo,
  assignedProfilePic,
}) => {
  return (
    <section className={$.container}>
      <h2 className={$.heading}>{title}</h2>
      <Avatar name={assignedTo} image={assignedProfilePic} />
      <input
        type="checkbox"
        checked={checked}
        onChange={onToggle}
        className={$.checkbox}
      />
      {time && <p className={$.time}>{time}</p>}
    </section>
  );
};
```
</details>

> More examples can be added/suggested by developers.

### When to use a connector?
It is not obligatory to use a connector in your application, but it can be helpful in the following cases:
1. **Combining multiple states**: You need to combine server and application state into component props. For example, you have a collection of books, but the selection state is only locally available.

2. **Reusability**: You want to use a certain component with a piece of application state in multiple locations of your app. For example, the total price of your shopping cart.

3. **Direct coupling**: Have your data close to the component. Within React, you will benefit from this: prevent unnecessary rerenders of components that do not use a specific slice of server/application state.

### When to use a transformer?
Transformers can be used to transform API data in your application if the data received from the API is in a raw or unstructured format and needs to be processed and transformed into a format that can be easily consumed by your application. Examples include:

1. **Data Cleaning**: If the data received from the API is in a messy or unstructured format.

2. **Data Normalization**: If the API data is in different formats, transformers can be used to normalize the data into a consistent format that can be easily processed by your application.

3. **Data Augmentation**: If the API data is limited, transformers can be used to augment the data by generating new data based on the existing data.

4. **Data Integration**: If the API data needs to be combined with other data sources, transformers can be used to integrate the data by mapping it to a common schema or ontology.

Downsides to using transformers:
1. **Impact on performance**: It may require more computation power.

2. **Extra complexity**: Data from the API is not the same as used in the application.

3. **Taking responsibility**: The backend should deliver clean and structured data. Please discuss with the backend first before adding transformers. The frontend is not supposed to take ownership of the backend data.
