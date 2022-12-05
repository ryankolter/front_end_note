# useMemo

- 用来记忆并缓存`值`，在指定依赖没有更改时，直接返回缓存值，无需重新计算，可用于优化性能

- 【场景1】自定义 计算属性
    ```ts
    const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
    ```
    - 当 a或者b 发生更改时，会重新计算 memoizedValue 的值

- 【场景2】实现 shouldComponentUpdate，防止不必要的子组件渲染
    ```js
    const [count, setCount] = useState(0);
    const [time, setTime] = useState(0);
    
    const child1 = useMemo(() => <Counter count={count} />, [count]);
    const child2 = useMemo(() => <Time time={time} />, [time]);

    return (
        <div>
            <button onClick={() => setCount(count + 1)}>count + 1</button>
            <button onClick={() => setTime(time + 1)}>time + 1</button>
            {child1}
            {child2}
        </div>
    );
    ```
    