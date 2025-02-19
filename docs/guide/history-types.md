---
title: History Types
---

> NOTE: If you don't need **hash or memory routing, then you can skip this section**.

While it's not required to know the `history` API itself to use TanStack Router, it's a good idea to understand how it works. Under the hood, TanStack Router requires and uses a `history` instance to manage the browser history.

- If you don't create a history instance, a default `createBrowserHistory` instance is created for you automatically when you call `new ReactRouter()`
- If you **need a special history instance type**, You can use the history package to create your own history instance:

- `createBrowserHistory`: The default history type.
- `createHashHistory`: A history type that uses a hash to track history.
- `createMemoryHistory`: A history type that keeps the history in memory.

Each of these APIs behaves slightly differently and documentation for them can be found in the [`history` package](https://github.com/remix-run/history).

Once you have a history instance, you can pass it to the `ReactRouter` constructor, which can then be passed to the `Router` component:

```tsx
const history = createHashHistory()
const location = new ReactRouter({ history })

function App() {
  return (
    <Router
      location={location}
      routes={
        [
          // ...
        ]
      }
    />
  )
}
```

## Browser Routing

The `createBrowserHistory` is the default history type. It uses the browser's `history` API to manage the browser history.

## Hash Routing

Hash routing can be helpful if your server doesn't support rewrites to `index.html` for HTTP requests (among other environments that don't have a server).

```tsx
import { createHashHistory, ReactRouter } from '@tanstack/react-router'

// Create a hash history
const hashHistory = createHashHistory()

// Set up a ReactRouter instance with the hash history
const location = new ReactRouter({
  history: hashHistory,
})
```

## Memory Routing

Memory routing is useful in environments that are not a browser, like `node.js` or `electron`.

```tsx
import { createMemoryHistory, ReactRouter } from '@tanstack/react-router'

// Create a memory history
const memoryHistory = createMemoryHistory({
  initialEntries: ['/'], // Pass your initial url
})

// Set up a ReactRouter instance with the memory history
const location = new ReactRouter({
  history: memoryHistory,
})
```
