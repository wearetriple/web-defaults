# Dumb components

## What is dumb component?

It's purpose is to render the UI, it contain display logic and optionally emits events.
A dumb component ony needs it's props:

- It doesn't make any api calls
- It doesn't mutate global state
- It doesn't require any context

Generally the datatypes of the props are primitive/scalar types (strings, numbers, booleans)
If a prop is an object, especially if that object is coming from an api call, that is a signal you're dealing with a smart component.

## Why limit a component to be dumb?

Making dump components has many benefits:

- Easy to reason about: As a developer you only need to think about this single component (and the nested dumb components)
- Easy to test/preview: You can write a story that renders the component without having to configure any context or mock any api calls.

## How to keep a component dumb?

When developing a component, keep pushing complexity upwards until you reach a smart component.

Example 1

```svelte
<ProductRow productId={product.id} title={product.title} on:delete={onProductDelete} />;

<!-- ProductRow.svelte -->
<script lang="ts">
  export let productId: string;
  export let title: string;

  const dispatch = createEventDispatcher();
</script>

<button on:click={dispatch('delete', productId)}>Delete</button>
```

<details>
  <summary>React</summary>

```tsx
<ProductRow
  productId={product.id}
  title={product.title}
  onDelete={onProductDelete}
/>;

type Props = {
  productId: string;
  title: string;
  onDelete: (id: string) => void;
};
const ProductRow = ({ productId, title, onDelete }: Props) => (
  <button onClick={() => onDelete(productId)}>Delete</button>
);
```

</details>

ProductRow is not very smart but it receives a `productId` which is never displayed, the reason it was passed is was for the onDelete event.
That is a little business logic, we can push that logic up:

```svelte
<ProductRow title={product.title} on:delete={() => onProductDelete(product.id)} />;

<!-- ProductRow.svelte -->
<script lang="ts">
  export let productId: string;
  export let title: string;

  const dispatch = createEventDispatcher();
</script>

<button on:click={dispatch('delete', productId)}>Delete</button>
```

<details>
  <summary>React</summary>

```tsx
<ProductRow
  title={product.title}
  onDelete={() => onProductDelete(product.id)}
/>;

type Props = {
  title: string;
  onDelete: () => void;
};
const ProductRow = ({ title, onDelete }: Props) => (
  <button onClick={onDelete}>Delete</button>
);
```

</details>

Example 2:

```svelte
<ProductRow discount={product.discount} discountVisible={!inventory.hasBought(product.id)} />

<!-- ProductRow.svelte -->
<script lang="ts">
export let discount: number;
export let discountVisible: boolean;
</script>

{#if discountVisible}
  <div class="discount">{discount}</div>
{/if}
```

The business logic is now shared, you could argue that discountVisible is display logic and it is, but why pass a discount as a prop if it's not visible?

```svelte
<ProductRow discount={inventory.hasBought(product.id) ? undefined : product.discount} />

<!-- ProductRow.svelte -->
<script lang="ts">
export let discount: number | undefined;
</script>

{#if discount}
  <div class="discount">{discount}</div>
{/if}
```

## Conclusion

Dumb components, data in, event out. They are easier to write, read, test and maintain and are something to strife for. But don't feel bad for writing smart components, they do the work and are essential too.
