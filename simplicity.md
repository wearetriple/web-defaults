# 😌 Simplicity

Simplicity is not a set of rules; it is more of a guiding principle.

## Simple vs Easy

Simple is not the same as easy. In fact, it is much easier to write complicated code. [Simple made easy - Rich Hickey](https://www.youtube.com/watch?v=SxdOUGdseq4)

Related to simplicity is the idea of minimalism.

> Perfection is achieved, not when there is nothing more to add, but when there is nothing left to take away.
>
> - Antoine de Saint-Exupéry

"You aren't gonna need it" (YAGNI) is a principle that arose from extreme programming (XP) which states that a programmer should not add functionality until it is deemed necessary.

## How does this apply to coding & project conventions?

Take famous libraries like Redux, Rxjs, or TanStack-Query, for example. These are great libraries that solve real problems. However, many of our projects don't have the problems these libraries solve. By using these libraries, you are making trade-offs, as they also add complexity and new problems to your projects.

I would argue that many projects don't need a "clean" architecture and are over-engineered. If a boilerplate promotes certain patterns, they tend to be used in all projects, even if they are not needed.

### Balancing act

Both statements are true:

- Don't build the feature until you need it; you'll get it wrong.
- If we had known about this feature beforehand, we would have architected our system differently.

Making a system or interface "flexible" or "robust" is hard to get right. Some prefer adding layers early, but from a simplicity perspective, adding layers when needed is preferable.

The "when needed" is more of a feeling and will be different for each developer.

Take i18n, for example. If we add it only when the client requests it, it will take some work before all components are converted. But adding it and not using it will add complexity and have a big performance hit on the system with no benefit.

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

We could have also used `hidden` instead of `visible`; they are both clear in their intent. However, the way the variable is used makes `visible` simpler.
`{#if visible}<div>...`
vs
`{#if !hidden}<div>...`
The latter is more complex as it adds a negation.

This is a very small example but demonstrates the idea of simplicity: always in pursuit of making the system more elegant, simpler, reducing layers, and removing code.

### Too simple

> Make everything as simple as possible, but not simpler.
>
> - Albert Einstein

Using short descriptive names is one of the ways to simplify your code. However, if the component doesn't have an obvious toggle state, it's probably better to use more descriptive names:

```ts
let modalVisible = true;
function showModal() {
  modalVisible = true;
}
function hideModal() {
  modalVisible = true;
}
```

It adds visual weight, but in some cases, that is worth it. The same goes for the show and hide functions. If these functions are used only once, it might be better to inline them.

```svelte
<button on:click={() => visible = false}>Close</button>
```

```tsx
<button onClick={() => setVisible(false)}>Close</button>
```

### Onboarding

Using the simplest solution for a project makes working on that project nice and improves productivity. However, even the simplest solutions can be quite complex. This can make onboarding new developers harder than if you're using an over-engineered, slower, more complex but standardized technology.
