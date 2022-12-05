# useCallback

- 用来记忆并缓存`函数`，当指定的依赖发生更改时，才会更新这个函数，可用于优化性能

- 【场景1】自定义 回调函数
    ```ts
    const memoizedCallback = useCallback(
        () => {
            doSomething(a, b);
        },
        [a, b],
    );
    ```
    - `useCallback(fn, inputs)` 等价于 `useMemo(() => fn, inputs)`

- 【场景2】测量DOM节点
    ```js
    function MeasureExample() {
        const [height, setHeight] = useState(0);
        
        const measuredRef = useCallback(node => {
            if (node !== null) {
                setHeight(node.getBoundingClientRect().height);
            }
        }, []);
        
        return (
            <>
                <h1 ref={measuredRef}>Hello, world</h1>
                <h2>The above header is {Math.round(height)}px tall</h2>
            </>
        );
    }
    ```
    