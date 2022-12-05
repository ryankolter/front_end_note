# useState

- 用来定义`状态变量`，可以替代以前的 构造函数内state 和 setState

- 【场景】自定义`含状态`的组件
    ```ts
    import { useState } from 'react';
    
    const MyBtn = () => {
        const [count, setCount] = useState(0);
        
        return (
            <div>
                <p>you clicked {count} times</p>
                <button onClick = {() => setCount(count + 1)}>
                    click me
                </button>
            </div>
        )
    }
    
    export default MyBtn;
    ```

    - 如果要用以前的类去写，会很麻烦，像下面这样
        ```ts
        class MyBtn extends React.Component {
            constructor(props) {
                super(props);
                this.state = {
                    count: 0
                }
            }
            
            render() {
                return (
                    <div>
                        <p>you clicked {this.state.count} times</p>
                        <button onClick = {
                            () => this.setState({
                                count: this.state.count + 1
                            })
                        }>
                            click me
                        </button>
                    </div>
                )
            }
        }
        ```