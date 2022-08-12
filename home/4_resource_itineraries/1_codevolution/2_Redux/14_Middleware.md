# 14. Middleware
Created Friday 12 August 2022

### Why and What
- Middlewares are the suggested way to extend Redux with custom functionality.
- Middlewares provide an extension point between dispatching an action, and the moment it reaches a reducer.
- Middlewares are commonly used for logging, crash reporting, performing async tasks etc.

- Basically, middleware let us hook into Redux's action-reducer lifecycle.

### How
Simply specify the list of middleware(s) when creating the store. Example:
```js
const { createStore, applyMiddleware } = require('redux');
const { logger } = require('redux-logger');

function reducer() {...}

const store = createStore(reducer, applyMiddleware(logger, ...));
```

See [full code](https://github.com/exemplar-codes/redux-demo-codevolution/blob/3c7cce025d40a11b59191ab356add910655235d2/middleware.js).