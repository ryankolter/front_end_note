# Number的方法

下面的写法：
数字变量.方法名 是原型方法
Number.方法名 是静态方法

## 原型方法

- #### `.toFixed()`
    - 将数字四舍五入，保留n位小数，不传参默认n为0
        ```js
        数字变量.toFixed(n)
        //Number.prototype.toFixed.call(数字变量);
        ```

- #### `.toPrecision()`
    - 将数字舍弃或补全到指定长度n，会考虑科学计数法
        ```js
        数字变量.toPrecision(n);
        //Number.prototype.toPrecision.call(数字变量);
        ```

## 静态方法

- #### `.isInteger()`
    - 判断是否为Number类型，且是整数
        ```js
        Number.isInteger(数字)
        ```
        - 【例子】
            ```js
            Number.isInteger(25) // true
            Number.isInteger(25.0) // true
            Number.isInteger(25.1) // false
            ```

- #### `isNaN()`
    - 判断是否是数字，直接调用，是window下的全局函数
        ```js
        isNaN(数字)
        ```
        - 对于ES6，Number对象补充了这个函数，更可靠
            ```js
            Number.isNaN(数字)
            ```

- #### `parseInt()`
    - 把字符串转换成数字，直接调用，是window下的全局函数
        ```
        parseInt(字符串)
        ```
        - 对于ES6，Number对象补充了这个函数
            ```js
            Number.parseInt(字符串)
            ```

- #### `parseFloat()`

    - 把字符串转换成浮点数，直接调用，是window下的全局函数
        ```js
        parseFloat(字符串)
        ```
        - 对于ES6，Number对象补充了这个函数
            ```js
            Number.parseFloat(字符串)
            ```

## Number的属性

- #### `Number.EPSILON`
    - 两个可表示(representable)数之间的最小间隔

- #### `Number.MAX_VALUE`
    - 能表示的最大正数。最小的负数是 -MAX_VALUE

- #### `Number.MIN_VALUE`
    - 能表示的最小正数即最接近 0 的正数 (实际上不会变成 0)。最大的负数是 -MIN_VALUE

- #### `Number.MAX_SAFE_INTEGER`
    - JavaScript 中最大的安全整数 2^53^ - 1

- #### `Number.MIN_SAFE_INTEGER`
    - JavaScript 中最小的安全整数 -(2^53^ - 1)
