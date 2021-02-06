# React

**Problem** => When should useMemo(), useCallback(), and memo() be used.

**Solution** =>

Basically there are two main cases to use these hooks. When referential equality is needed, and when there are computationally expensive tasks.

- Referential equality is needed.
- Execution of computationally expensive tasks.

1. #### Referential equality

Suppose there are two components, A & B.

```javascript
const A = (props) => {
  const handleClick = () => doSomething();
  const data = getData();
  return (
    <>
      <B data={data} onClick={handleClick} />
      <div>{props.text}</div>
    </>
  );
};

const B = React.memo((props) => <div onClick={props.onClick}>{props.data}</div>);
```

B is a component that renders a big amount of data, therefore it is desired to re-render it only when this data changes. For this, it can be wrapped with React.memo, which memoizes the component, so it won't be re-rendered given it receives the same props. It would work fine if it wasn't for the `onClick` prop. Due to the way JavaScript manages equality (by reference, not by value), `{} !== {}` and `()=>{} !== ()=>{}`. So if for any reason, A get's re-rendered, the new `handleClick` function that is passed to **B** won't be the same as the old one, triggering the re-rendering.

In this case, useCallback becomes useful.

```javascript
const handleClick = useCallback(() => doSomething(), []);
```

Now, the handleClick function won't change with every re-render. The second parameter is just like in useEffect, an array of dependencies (when should handleClick be re-defined).

2. #### Computationally expensive tasks

Suppose there is a component A.

```javascript
const A = (props) => {
  const complexResults = calculateComplexData(props.param1, props.param2);
  return <div>{complexResults}</div>;
};
```

This component is doing some complex (and demanding) calculations and then rendering the results. Imagine this component is re-render by a parent component every time there's a change within it (the parent component). Then `calculateComplexData()` will be executed every time. In order to avoid this not so efficient behavior, useMemo becomes quite useful.

```javascript
const { param1, param2 } = props;
const complexResults = React.useMemo(() => calculateComplexData(param1, param2), [
  param1,
  param2,
]);
```

With this, the complexResults will be the same, given that the dependencies(param1, param2) do not change.

---

**Problem** => Imports might become somehow cumbersome sometimes.. **eg.**

````javascript
import Something from '../../../../components/Something'```
````

**solution** => Use absolute imports.

It is possible to add absolute paths to React within the jsconfig.json/tsconfig.json files.

```json
{
  "compilerOptions": {
    "baseUrl": "src"
  },
  "include": ["src"]
}
```

Now, the import would be something like:

````javascript
import Something from 'components/Something'```
````
