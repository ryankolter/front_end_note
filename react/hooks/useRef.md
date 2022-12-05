# useRef

- 用来记录一个值，可用current属性取出

- 【场景】自定义 对DOM元素的引用
    ```ts
    const inputEl = useRef(null);
    
    const onButtonClick = () => {
        inputEl.current.focus();
    };
    return (
        <div>
            <input ref={inputEl} type="text" />
            <button onClick={onButtonClick}>Focus the input</button>
        </div>
    );
    ```
    - 这里 inputEl 的 current 属性，会被初始化为下面 指定ref 的 input元素
