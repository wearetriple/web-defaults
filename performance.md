# 🏃 Performance

## Compilers (development performance)

Use Vite and avoid Webpack. Vite uses the native ES modules feature in the browser to handle imports, while webpack and Parcel use a more traditional approach of bundling all the files together. This allows for faster development builds and hot module replacement with Vite.

## Lazy loading

Lazy loading is a design pattern. It allows you to load parts of your application on-demand to reduce the initial load time. For example, you can initially load the components and modules related to your homepage. Then, you can load the rest of the components based on user navigation.

### Advantages

- Reduces initial loading time by reducing the bundle size.
- Reduces browser workload.
- Improves application performance in low bandwidth situations.
- Improves user experience at initial loading.
- Optimizes resource usage.

### Disadvantages

- No performance improvement for small-scale applications.
- Placeholders can slow down quick scrolling.
- Requires additional communication with the server to fetch resources.

## Data fetching

Smart implementations of data fetching can improve your applications performance drastically. Some examples of data fetching implementations:

- Avoid fetching the same data multiple times. Store data that is used on every page rather than fetching the samen data every page render.
- Fetch extra data separate from the initial page load. The page is already shown to the user, giving the user a faster experience. Extra data that is fetched can be indicated by showing loading indicators
- Stale while revalidating. @TODO: more info

## React specific

- useMemo. A React Hook that lets you cache the result of a calculation between re-renders.
- useCallback. A React Hook that lets you cache a function definition between re-renders.

## Vite specific

@TODO

#### Sources

- https://medium.com/trendyol-tech/vite-webpack-killer-or-something-else-87019b4aeca2
- https://www.syncfusion.com/blogs/post/lazy-loading-with-react-an-overview.aspx
- https://react.dev/reference/react/useMemo
- https://react.dev/reference/react/useCallback
