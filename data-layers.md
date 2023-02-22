# Data Layers
> "A data access layer (DAL) in computer software is a layer of a computer program which provides simplified access to data stored in persistent storage of some kind."

Examples where a layer of data can exist:
- In a component also known as component state and accessed using hooks in React.
- On a server also known as server state and accessed using an API.
- In route parameters also known as URL state and accessed using Location Browser API.

Two keywords that are important in a data layer:
- __Store__: Where data is stored, for example a Firebase Database, indexedDB, localStore, React Query, Apollo Client Cache, Redux Store, etc.
- __State__: A snapshot of the store in a point of time representing the current state of the store.

## Store


## State
Within an application, wether it be build with React (Native) or Svelte, there are different types of state. So there is not a single centralized store where all your data lives:

### Component state
(...write short description)

#### Examples

<details>
<summary>React (Native) with useState - (...write usecase)</summary>

```jsx
import React from "react";
import { Switch } from "react-native";

const Toggle: React.FC = () => {
    const [toggled, setToggled] = React.useState(false);

    return <Switch onValueChange={() => setToggled(!toggled)}  />;
};

export default Toggle;
```
</details>

<details>
<summary>React (Native) with useReducer - (...write usecase)</summary>

```tsx
import React from "react";
import { Button, Switch, Text, TextInput } from "react-native";
import { TouchableOpacity } from "react-native-gesture-handler";

type SleepPosition = "belly-first" | "left-side" | "right-side";

type ActionResetForm = {
  type: "RESET_FORM";
};
type ActionSetEmailAddress = {
  type: "SET_EMAIL_ADDRESS";
  payload: string;
};
type ActionSetReceivingAnnoyingMarketingEmails = {
  type: "SET_RECEIVING_ANNOYING_MARKETING_EMAILS";
  payload: boolean;
};
type ActionSetSleepPosition = {
  type: "SET_SLEEP_POSITION";
  payload: SleepPosition;
};

type Action =
  | ActionResetForm
  | ActionSetEmailAddress
  | ActionSetReceivingAnnoyingMarketingEmails
  | ActionSetSleepPosition;

type State = {
  emailAddress: string;
  receiveAnnoyingMarketingEmails: boolean;
  sleepPosition: SleepPosition;
};

const defaultState: State = {
  emailAddress: "",
  receiveAnnoyingMarketingEmails: false,
  sleepPosition: "belly-first",
};

const reducer = (state: State, action: Action) => {
  switch (action.type) {
    case "RESET_FORM": {
      return defaultState;
    }
    case "SET_EMAIL_ADDRESS": {
      return {
        ...state,
        emailAddress: action.payload,
      };
    }
    case "SET_RECEIVING_ANNOYING_MARKETING_EMAILS": {
      return {
        ...state,
        receiveAnnoyingMarketingEmails: action.payload,
      };
    }
    case "SET_SLEEP_POSITION": {
      return {
        ...state,
        sleepPosition: action.payload,
      };
    }
    default: {
      throw new Error(`Action type not supported`);
    }
  }
};

const NewsLetterSubscribe: React.FC = () => {
  const [state, dispatch] = React.useReducer(reducer, defaultState);

  return (
    <>
      <Switch
        onValueChange={(toggled) =>
          dispatch({
            type: "SET_RECEIVING_ANNOYING_MARKETING_EMAILS",
            payload: toggled,
          })
        }
      />
      <TouchableOpacity
        style={state.sleepPosition === "belly-first" && styles.active}
        onPress={() =>
          dispatch({ type: "SET_SLEEP_POSITION", payload: "belly-first" })
        }
      >
        <Text>Belly first</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={state.sleepPosition === "left-side" && styles.active}
        onPress={() =>
          dispatch({ type: "SET_SLEEP_POSITION", payload: "left-side" })
        }
      >
        <Text>Belly first</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={state.sleepPosition === "right-side" && styles.active}
        onPress={() =>
          dispatch({ type: "SET_SLEEP_POSITION", payload: "right-side" })
        }
      >
        <Text>Belly first</Text>
      </TouchableOpacity>
      <TextInput
        placeholder="Email-Address"
        onChangeText={(text) =>
          dispatch({ type: "SET_EMAIL_ADDRESS", payload: text })
        }
      />
      <Button
        onPress={() => dispatch({ type: "RESET_FORM" })}
        title="Reset form"
      />
    </>
  );
};

export default NewsLetterSubscribe;
```
</details>

### Application state
If you want to keep state on a more global level that doesn't live server side you want to consider Application state. State that can represent stuff like: theming, settings, notifications, open modals, etc.

You need to consider if your state needs to live on app level or can be nested deeper down your app tree. Sometimes a state only is relevant to specific subset of pages. In that case define it on a lower level to prevent dropping performance for the whole app.

#### Examples

<details>
<summary>React (Native) with context + hooks - (...write usecase)</summary>
</details>

<details>
<summary>React (Native) with RTK + hooks - (...write usecase)</summary>
</details>


### Server Cache state
When fetching data from an external API we can store that data in a client side cache. This has several benefits:
- Reduce amount of API calls to the server.
- Have data available while new data is being fetched.
- Easy to use the same API query multiple times, without multiple fetches.

There are also a couple of downsides:
- Need to think about invalidating cache.
- Resolve conflicts between existing and incoming data in the cache.

#### Examples

<details>
<summary>React (Native) with React Query (REST) - (...write usecase)</summary>
</details>

<details>
<summary>React (Native) with Apollo Query (GraphQL) - (...write usecase)</summary>
</details>

### Route state
State that is stored in the route. For web that means it can be found in the address bar of the browser. Within React Native it means route params for each screen (stack/tab).

#### Examples

<details>
<summary>NextJS??  - (...write usecase)</summary>
</details>

<details>
<summary>React with React Router + hooks  - (...write usecase)</summary>
</details>

<details>
<summary>React with React Navigation + hooks  - (...write usecase)</summary>
</details>
