# evolution

A note on the evolution of important versions of popular front-end libraries/frameworks.

## Node.js

- [package.json："type" field](https://nodejs.org/api/packages.html#type)（v12.17.0） 
- [ESM: Top-Level Await](https://nodejs.org/api/esm.html#top-level-await)（v14.8.0）
- [package.json："exports" & "imports" patterns](https://nodejs.org/api/packages.html#exports) - replace `"main"` field（v12.20.0, v14.13.0）
- [`node:` protocol imports](https://2ality.com/2021/12/node-protocol-imports.html)（v14.18.0, v16.0.0）
- [fs/promises](https://nodejs.org/api/fs.html#promises-api) support（v14.0.0, via `require('fs').promises` from v10.1.0）

## React

### [v18](https://react.dev/blog/2022/03/29/react-v18)

- `ReactDOM.render` is no longer supported in React 18.

```jsx
// Before
import { render } from 'react-dom';
render(<App tab="home" />, document.getElementById('app'));

// After
import { createRoot } from 'react-dom/client';
const root = createRoot(document.getElementById('app')); // createRoot(document.getElementById('app')!) if you use TypeScript
root.render(<App tab="home" />);
```
- changed `unmountComponentAtNode` to `root.unmount`.

```jsx
// Before
unmountComponentAtNode(container);

// After
root.unmount();
```

- removed the `callback` from render.

```jsx
// Before
const container = document.getElementById('app');
render(<App tab="home" />, container, () => {
  console.log('rendered');
});

// After
function AppWithCallbackAfterRender() {
  useEffect(() => {
    console.log('rendered');
  });

  return <App tab="home" />
}

const root = createRoot(document.getElementById('app'));
root.render(<AppWithCallbackAfterRender />);
```

- Finally, if your app uses server-side rendering with hydration, upgrade `hydrate` to `hydrateRoot`.

```jsx
// Before
import { hydrate } from 'react-dom';
hydrate(<App tab="home" />, document.getElementById('app'));

// After
import { hydrateRoot } from 'react-dom/client';
const container = ;
const root = hydrateRoot(
  document.getElementById('app'),
  <App tab="home" />
);
// Unlike with `createRoot`, you don't need a separate root.render() call here.
```

### [v16.8](https://legacy.reactjs.org/blog/2019/02/06/react-v16.8.0.html)

- [React Hooks](https://legacy.reactjs.org/docs/hooks-reference.html)
  - Basic Hooks: `useState`, `useEffect`, `useContext`
  - Additional Hooks: `useReducer`, `useCallback`, `useMemo`, `useRef`, `useImperativeHandler`, `useLayoutEffect`, `useDebugValue`, `useDeferredValue`, `useTransition`, `useId` 
  - Library Hooks: `useSyncExternalStore`, `useInsertionEffect`

## Express

### [5.0.0-alpha.1](https://github.com/expressjs/express/releases/tag/5.0.0-alpha.1)

> WARNING:This version was released in November 2014, but is [still in beta as of today](https://github.com/expressjs/express/tree/v5.0.0-beta.1).

remove:

- `app.del - use `app.delete`
- `req.acceptsCharset` - use `req.acceptsCharsets`
- `req.acceptsEncoding` - use `req.acceptsEncodings`
- `req.acceptsLanguage` - use `req.acceptsLanguages`
- `res.json(obj, status)` signature - use `res.json(status, obj)`
- `res.jsonp(obj, status)` signature - use `res.jsonp(status, obj)`
- `res.send(body, status)` signature - use `res.send(status, body)`
- `res.send(status)` signature - use `res.sendStatus(status)`
- `res.sendfile` - use `res.sendFile` instead
- `express.query` middleware

change:

- `req.host` now returns host (`hostname:port`) - use `req.hostname` for only hostname
- `req.query` is now a getter instead of a plain property

add:

- `app.router` is a reference to the base router

### [v4.17.0](https://github.com/expressjs/express/releases/tag/4.17.0)

- Add `express.raw` to parse bodies into `Buffer`
- Add `express.text` to parse bodies into string

### [v4.16.0](https://github.com/expressjs/express/releases/tag/4.16.0)

- Add `express.json` and `express.urlencoded` to parse bodies

### [v4.15.0](https://github.com/expressjs/express/releases/tag/4.15.0)

- Add `next("router")` to exit from router

