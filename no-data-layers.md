# "Data layer"

Many "webapps" have a "data layer", but why. In many many cases this is not needed.
Developers are taught the S.O.L.I.D. principles such a D.R.Y (don't repeat yourself) and S.R.P. (Single Responsibility principle)

These principles and practices are written in an era of OOP programming model and are compiled to linkable binaries and their usefulness is not universal.

Lets take a todo app.
If we take the following directory structure:

- models/
  - User.ts
  - Project.ts
  - Task.ts
- transformers/
  - userTransformers.ts
  - projectTransformers.ts
  - taskTransformers.ts
- services/
  - userRepository.ts
  - projectRepository.ts
  - taskRepository.ts
  - api.ts
  - dto.ts

We can reduce this to

- services/
  - api.ts
  - dto.ts

And the result has the same level of "maintainable", "scalable" or "readable" as before (better in my opinion, but these are very subjective terms)
The code hasn't moved, the other files are deleted, but the new project gets a lower grade on the "clean" scorecard.

Why did we start these principles in the first place, what was the benefit?

From the book:

- Independent of Frameworks
- Testable
- Independent of UI
- Independent of Database
- Independent of any external agency.

## Independent of Frameworks

They where not listed above but i suspect that this file growth problems continues
A useUser.ts, useTask.ts useProject.ts instead of a single useApi.ts

api.ts & dto.ts weren't framework dependent, so when removing files this is still the case.

## Testable

Just less code that needs tests

## Independent of UI

"A Web UI could be replaced with a console UI"
I don't see how taskRepository.ts is giving us any benefits over direct api usage.
If this was a backend, some access validation logic could be written independently, for frontend, what kind of methods can to call on a Task?

## Independent of Database

Let's interpret this as independent of backend, oké, you got me, because using the api directly throughout the application create much tighter coupling to the backend.
But this is a very theoretical advantage:

1. Most applications are bound to the same backend for their lifetime.

2. When the decision has been made to replace the backend, this is a opportunity to start fresh (and use SvelteKit ;p )

Because yeah, the models _could_ be independent of the backend, but it am willing to bet a couple of Triple coins that the migration to different backed is more work than changing some fields in a transformer.
And if it was only changing some fields, typescript refactor and VSCode's search-and-replace can get you very far.

3. The dreaded whitelabel application, this one sounds so good on paper. When i think of successful whitelabel products, i think of Contentful and Shopify, where it's mostly api's and the customer facing UI is not part of the platform, but the client get a nice UI to manage their stuff.
   If it's possible, then it's extremely hard especially in the multiple backend to multiple frontend setup.
   What you'll probability end up with is that the second and third backend have compatibility layers that makes them look like the first backend.
   and the models be become big with lots of optional properties and logic based on those property combinations.
   Instead of an unified model architecture i'd suggest creating a webapp for each backend. Re-use can be achieved by creating dumb & renderless components.

## Independent of any external agency

So this is the code that is standalone, it's doesn't depend on a backend and doesn't depend on a design or frontend.
Sometimes called "business logic".
This one is a bit tricky, take "Show the edit button for user with edit rights"
This is business logic, but it is also UI logic. the `{user.rights.editor && <button>Edit</button>}`

Most of the time the business logic the frontends are make is fairly straightforward.

# But, but, but

## The ugly backend

The backend is ugly "The user dto is using snake_case and uses both English and Dutch property names."
That is not ideal, and i feel your pain. but faking how the api really works is like putting lipstick on a pig.

PS. If the backend is created in C#, ask your backender for camelCase it's the `JsonSerializerOptions.PropertyNamingPolicy = JsonNamingPolicy.CamelCase;` option.

Sketching out how you prefer to receive the json, and ask your backend (preferably during refinement) a good option.

I find it easier to adjust to reading and using a different naming convention than an application where the data in the network panel doesn't match the data i'm working with. (it not clean, but based on the property name you can see it came from the api)

## Ugly types everywhere

This takes little practice, but try not to import Dto types directly.

Example:

```
const { data, loading, error } = useApi('user/[userId]', { userId })
```

This code fetches the user with the id passed as `userId` the `data` is a typed user object.
the properties of that object be mapped to component props, all without importing the UserDto.
The components don't use user object they thinks in strings, and booleans, See dumb components.

## This is chaos. where is the structure?

The best I can explain this is with a metaphor:
You walk into a room there is stuff on the desk, some stuff on the floor and stuff in two big boxes.
This represents the "messy" or "dirty" codebase.

You can "clean" this room by taking stuff by bringing boxes placing stuff into small boxes with labels (files) and put those small boxes into to bigger boxes (folders). at the end this room has stacks of boxes, some filled, some empty, this represents the clean codebase.

Both rooms have structure, and although the second room has more structure.

But to get anything done in the clean room, you are opening and closing boxes all the time,
If you're not the one that packed and labelled the boxes, you don't know where to find anything.
And once you're done creating the thing might not fit anymore and you need to reshuffle and relabel the boxes.

Some developers love organizing and labeling stuff, and are very happy in the clean room.
And for them the this way of working is effective.

I like the "messy" codebase for it's focus on creating value and having tool ready.

Searching for a compromise where there is less stuff on the floor.

## The backend is changing the responses and production was broken

This is a organizational problem, not a technical problem, If you would could change tables in the database, the backend breaks. The API a backend provides is a contract between frontend and backend.

Backends change, but creating a "generic" model is not the solution. This might make you feel safe, but this is an illusion.
You are trying to predict the future of what is going to change and what stays the same, and most of the time we are wrong.

This also happens when the api has unclear specifications.
A lot can be solved by talking to your backender and asking for clarification or improved documentation types.
In C# for example placing additional `[Required]` annotation from `System.ComponentModel.DataAnnotations` will change the generated openapi type from `string | null | undefined` to `string`

Sometimes you've got to deal with unreliable data sources, where correct data by the backend is not possible.
In that case a verification step is needed, don't create Dto types for that api (as they are incorrect and lying to typescript leads to bugs)

Use zod or a comparable library to verify the data and use the type inferred by zod as Dto.

# Models

No models never?
For the Task in the example, the businesslogic lives on the server.
If the businesslogic really lives in the frontend, maybe, but the models are the lesser idea. The big idea is to decouple it from the api and ui.
`models/ShoppingCart.ts` is not important or that useful.
`utils/calulateTotalPrice.ts` this one is, if you can prevent using a Dto that's preferable.

```ts
// instead of
function calulateTotalPrice(cart: CartDto);
// write
type Line = { quantity: number; amount: number };
function calulateTotalPrice(lines: Line[]): number;
```

If the Line type can be made compatible Cart by changing `amount` into `amountInEuro` and (and only have one cart backend) make that change to make calling the function easier.

Note that the Line type doesn't include a product or description, that is not needed for the calulateTotalPrice to execute and that reduces the setup code needed for a unittest. Would you be using a models/OrderLine.ts you'd probably

# Transformers

Most webapps are big transformer, they transform data into UI.
Without guidance it may be "too flexible and organic" for developers.
So what is the best place to transform.

Wait until you need it.
What PHP's magic quotes has taught me is wait until you need the data and then transform/encode the data into the desired format. Much later I realized this is not only useful for security.
Many codebases do the opposite and data is transformed before anything is done with it. So lets elaborate:

Example:

```ts
function transformTask(task: TaskDto): User {
  return {
    id: data.guid,
    description: data.text_description
    createdAt: transformDate(data.date_created)
  };
}
```

later

```jsx
<div>{task.descripion}</div>
<div>{formatDate(task.createdAt)}</div>
```

This is code I could have written in the past.
Today I'd write:

```jsx
<div>{task.text_descripion}</div>
<div>{formatDate(task.date_created)}</div>
```

The reasoning is that I convert the uglier object into a nicer object once and the rest of the application can use the nice object.
True, but at what cost?

### Scenario 1: A new field is added.

Update the Dto (generate api types) the new properties are ready to use.
But when using transformers you need to update the model and the transformers

Forgot to update one? New bug: Loading and saving a task removes the new property on save.

### Scenario 2: Dates

Oh oh, a bug the SSR date was different than the CSR, because the `transformDate` used Date object and the server was in another timezone.
How to solve?
include a timezones into your js bundle. Or looking at the server string: "2023-04-21T10:30:00+0200" all the correct numbers are in the string.
Strip the timezone and the Date object contains the "wrong" time and invalid unit timestamp. but when displaying it shows the date in dutch timezone.

When converting the data in the beginning your whole app get the wrong date, for-display-purposes-only

##

@todo Overpassing

##

@todo type coassion , optional god object

##

@todo d.ts

## Transformers hidden in plain sight

<div>{title}</div>

<Row title={item.text_title} />

@todo explain

# Examples of how to load data without transformers,

@todo
