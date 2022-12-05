# useImperativeHandle

- 在父组件中定义ref并传入子组件（要配合forwardRef使用）时，自定义子组件能暴露给父组件的内容，而不是暴露子组件内的整个DOM

- 【场景】父组件想要调用子组件的某个函数
    ```js
    // 子组件，只暴露focus方法给传入的ref
    const TextInput = forwardRef((props, ref) => {
        const inputRef = useRef()
        
        useImperativeHandle(ref, () => ({
            focus: () => {
                inputRef.current.focus()
            },
        }))
        
        return <input type="text" ref={inputRef} />
    })
    ```
    ```js
    // 父组件，调用此方法
    export default function Parent() {
        const inputRef = useRef()
        
        return (
            <div>
                <button onClick={() => inputRef.current.focus()}>聚焦</button>
                <TextInput ref={inputRef} />
            </div>
        )
    }
    ```
    
    