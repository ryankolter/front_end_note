# async和等待await

ES7中引入，让ES6的promise可读性更强

### async是什么？

声明`会返回Promise`的函数

三句话
- async就是声明后面定义的函数为异步函数
- 这样才能在函数体里面使用await等待
- 才能在调用此函数时在前面使用await等待
```js
//ES6写法
function s() {
    return Promise.resolve('TEST');
}

function f() {
    return Promise.reject('Error');
}
```
```js
//ES7写法
async function asyncS() {
    return 'TEST';
}

async function asyncF() {
    throw 'Error';
}
```
本质就是Generator函数的语法糖
<br>

### await是什么？

只能在声明了async的函数内使用
让我们能等待一个Promise返回信号，返回后才能继续往下执行

【例子】

- 模拟异步
    - 用 setTimeout 模拟异步，并用 Promise 封装
        ```js
        let func = (val) => {
            return new Promise((resolve, reject) => {
                setTimeout(() => {
                    resolve(val);
                }, 1000);
            });
        }
        ```
- 定义异步函数
    - 下面调用func会返回一个Promise对象，可以加await等待
        ```js
        async function f(){
            const response = await func('http://example.com/');
            //下面就相当于Promise返回后then里面的回调
            console.log(response);
        }
        ```
- 执行  
    - 由于在最外层不能用await，所以需要用下面两种方法
    - 【办法1】用.then写Promise返回后的回调
        ```js
        f().then(() => console.log('Finished'));
        ```
    - 【办法2】用立即执行函数
        ```js
        (async ()=> {
            await f();
            console.log('Finished')
        })()
        ```

### Generator函数是什么？

- 它可以断续执行，并返回一连串的值

- 函数内书写一行行的“yeild 返回值”来定义返回（每一行可返回一次），并停止执行
    ```js
    加上星号来定义
    function* helloWorldGenerator(){
        yield 'hello';
        yield 'world';
        return 'ending';
    }
    ```

- 调用此函数生成对象，再调用对象的`.next方法`来恢复执行，并触发一次yield返回
    - 生成对象
        ```js
        var hw = helloWorldGenerator()
        ```
    - 调用对象中的next方法
        ```js
        console.log(hw.next()) //返回{value:"hello",done：false}
        ```
        - 这里
            - value代表yield返回的值
            - done代表还可以继续调用.next()得到返回值
    - 再次调用
        ```js
        console.log(hw.next()) //返回{value:"world",done：false}
        ```
    - 再次调用
        ```js
        console.log(hw.next()) //返回{value:"ending",done：true}
        ```
        - 发现done为true，即可知道生成器执行到最后的return了




