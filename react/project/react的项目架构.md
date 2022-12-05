# react的项目架构

均在src目录下

- `index.tsx` 入口文件
    ```ts
    import React from 'react';
    import ReactDOM from 'react-dom';
    import './index.css';
    import App from './App';

    ReactDOM.render(
        <React.StrictMode>
            <App />
        </React.StrictMode>,
        document.getElementById('root')
    );
    ```
    - 引入`React`和`ReactDOM`做渲染
        - `ReactDOM.render`函数，接受两个参数
            - 组件树
            - 要挂载到的节点
                - 一般是`root`
                - 在 `public目录` 下的 `index.html` 中有定义 
    - 引入同级的 `index.css`文件，指定`全局样式`
        ```css
        html {
            font-size: 62.5%
        }
        
        html body #root .App {
            min-height: 100vh;
        }
        ```
        - 把html根元素的字体大小设置为`62.5%`
            - 就可以让 `1rem = 10px`，用`rem`做单位书写
        - 把App组件的最小高度设置为`100%`的`视口高度`(viewport height)
    - 引入同级的 `App` 主组件，默认是`App.tsx`

- `App.tsx` 主组件
    ```ts
    //v17版本后，不再需要引入import React from 'react';
    import './App.css';
    import { Button } from 'antd';
    import 'antd/dist/antd.css'
    
    const clickBtn = () => {
        console.log("clickBtn")
    }
    
    const App = () => {
        return (
            <div className="App">
                <header className="App-header">
                    <Button type="primary" onClick={clickBtn}>主按钮</Button>
                </header>
            </div>
        );
    }

    export default App;
    ```
    - 引入同级的 `App.css`文件，指定组件的局部样式
    - 这里用 `const App = `定义了一个函数，并 `export default` 导出
        - 函数会 `return` 一棵组件树，实现组件化
            - 组件树内可以 不断嵌套使用 其他 import引入的组件
            - 比如这里引入来自 `antd库` 的 `Button组件`
    - 这里可以同级用`const clickBtn =`定义响应函数

