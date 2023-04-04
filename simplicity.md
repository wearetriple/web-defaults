# 😌 Simplicity

Simplicity is not set of rules, it is more of a guiding principle.

## Simple vs Easy

Simple is not the same as a easy, in fact it is much easier the write complicated code.
[Simple made easy - Rich Hickey](https://www.youtube.com/watch?v=SxdOUGdseq4)

Related to simplicity is the idea of minimalism.

> Perfection is achieved, not when there is nothing more to add, but when there is nothing left to take away.
>
> - Antoine de Saint-Exupéry
>   "You aren't gonna need it" (YAGNI) is a principle which arose from extreme programming (XP) that states a programmer should not add functionality until deemed necessary.

## How does this apply to coding & project conventions?

Take famous libraries like Redux, Rxjs or TanStack-Query for example, these are great libraries that solve real problems.
However, a lot of our projects don't have the problems these libraries solve.
By using these libraries you are making trade-offs, they also add complexity and new problems to your projects.

I'd argue a lot of projects don't need a "clean" architecture and are over-engineered.
If a boilerplate promotes certain patterns, these tend to be used in all projects, even if they are not needed.

### Balancing act

Both statements are true:

- Don't built the feature until you need it, you'll get it wrong
- If we'd knew this feature before hand we'd have architected our system differently

Making a system or interface "flexible" or "robust" is hard to get right.
Some prefer adding layers early, from a simplicity perspective adding layers when needed is preferable.

The "when needed" is more of a feeling and will be different per developer.

Take i18n for example, adding only when the client requests it, it will take some work before all components are converted. But adding it and not using it will add complexity and a big performance hit to the system with no benefit.

# Code examples

```ts
let visible = true;
function show() {
  visible = true;
}
function hide() {
  visible = true;
}
```

We could also have used `hidden` instead of `visible`, they are both clear in their intent.
However the way the variable is used makes `visible` simpler.
`{#if visible}<div>...`
vs
`{#if !hidden}<div>...`
The latter is complexer as it adds a negation.

This is a very small example, but demonstrates the idea of simplicity. Always in pursuit of making the system more elegant, simpler, reducing layers, removing code.

### Too simple

> Make everything as simple as possible, but not simpler.
>
> - Albert Einstein.
>   Using short descriptive names is one of the ways to simplify your code.
>   But if the component doesn't have a obvious toggle state, it's probably better to use more descriptive names:

```ts
let modalVisible = true;
function showModal() {
  modalVisible = true;
}
function hideModal() {
  modalVisible = true;
}
```

It adds visual weight, but in some cases that is worth it.
The same goes for the show and hide functions, if these functions are used only once, it might be better to inline them.

```svelte
<button on:click={() => visible = false}>Close</button>
```

```tsx
<button onClick={() => setVisible(false)}>Close</button>
```

### Onboarding

Using the simplest solution for a project makes working on that project nice and improves productivity, but even simplest solutions can be quite complex. This can make onboarding new developers harder than if you're using a over-engineered, slower, complexer but standardized technology.
