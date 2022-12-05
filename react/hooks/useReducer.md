# useReducer

- 可替代`useState`的高级方案，管理复杂的状态变量，在涉及多个键值的对象情况下，更好用(可借鉴redux的state)

- 【场景】对aciton行为进行封装和触发
    ```ts
    const [state, dispatch] = useReducer(reducer, {count: 0});
    
    const reducer = (state, action) => {
        switch (action.type) {
            case 'increment':
                return {count: state.count + 1};
            case 'decrement':
                return {count: state.count - 1};
            default:
                return state;
        }
    }
    
    return (
        <div>
            <p>you clicked {state.count} times</p>
            <button onClick = {() => dispatch({type: 'increment'})}>
                +
            </button>
            <button onClick = {() => dispatch({type: 'decrement'})}>
                -
            </button>
        </div>
    )
    ```
