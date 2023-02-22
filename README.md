# you-might-not-need-an-effect

In this read, I learnt:

- **2 common cases you DON'T need an effect for:**
  - [x] `you don't need useEffect to transform data for rendering`
  - [x] `you don't need useEffect to handle user events`. Let the logic for activating an event be done in the event handler itself. If you put it inside useEffect, the Effect will not know what happened because the event handler component will already have been rerendered due to the prior user event activation which could change the state
- if a calculation is slow or involves a large ammount of data, it's a good idea to `memoize` (cache) it using `useMemo` hook to save on resources and improve your app's speed.

```
const displayedTodos = useMemo(() => {
    getFilteredTodos(todos, filter)
}, [todos, filter]);
```

- the above code tells React not to rerun the useMemo inner function, unless **_todos_** or **_filter_** changes. useMemo will return the previous result of **_getFilteredTodos_** (stored inside it) if the 2 dependencies have not changed. If any of the dependency changes, useMemo's inner function will rerun & the new result stored in useMemo for react to use for rendering
- useMemo's inner function runs during rendering therefore it needs to be a **pure function**
- useMemo helps you skip unnecessary rendering on updates
- **key concepts:**
  - [x] If you can calculate something during render, you don’t need an Effect
  - [x] To cache expensive calculations, add **useMemo** instead of **useEffect**
  - [x] To reset the state of an entire component tree, pass a different key to it
  - [x] To reset a particular bit of state in response to a prop change, set it during rendering
  - [x] **Code that needs to run because a component was displayed should be in Effects, the rest should be in events**
  - [x] If you need to update the state of several components, it’s better to do it during a single event
  - [x] Whenever you try to synchronize state variables in different components, consider lifting state up
  - [x] You can fetch data with Effects, but you need to implement cleanup to avoid race conditions
