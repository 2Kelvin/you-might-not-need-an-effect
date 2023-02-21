# you-might-not-need-an-effect

In this read, I learnt:

- **2 common cases you DON'T need an effect:**
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
