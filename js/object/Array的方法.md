# Array的方法

下面的写法：
数组.开头的是原型方法
Array.开头的是静态方法

## ES5之前的方法

### 会影响数组内部元素

- 添加与删除
    - 尾部添加多个元素，返回操作后数组的length
        ```js
        length = 数组.push(elem1,elem2...)
        ```
    - 删除尾部最后一个元素，并返回此元素
        ```js
        last = 数组.pop()
        ```
    - 头部添加多个元素，返回操作后数组的length
        ```js
        length = 数组.unshift(elem1,elem2...)
        ```
    - 删除头部第一个元素，并返回此元素
        ```js
        first = 数组.shift()
        ```
    
- 整个操作
    - 删除某位置开始的n个元素，且可添加新元素补充进去，返回被删除的元素
        ```js
        数组.splice(开始删除处的索引，要删除的元素数目，elem1，elem2...)
        ```
    - 把数组元素颠倒，返回颠倒后的结果
        ```js
        rev = 数组.reverse()
        ```
    - 排序，如果不加参数，将按照字符编码顺序
        ```js
        数组.sort(比较函数);
        //比较函数有两个参数a和b
        //若返回大于0，代表a应该在b的前面
        ```
        - 例子：中文按拼音排序
            ```js
            userArray.sort(function(a,b){
                return a['display_name'].localeCompare(b['display_name']);
            })
            ```

### 不影响内部数组元素（仅访问）

- `concat`
    - 链接多个数组，返回链接后的一个新数组
        ```js
        result = 数组.concat(array1, array2...）
        ```

- `slice`
    - 返回选定位置的数组元素，包括begin但不包括end
        ```js
        sli = 数组.slice(begin[, end])
        ```

- `join`
    - 给定分隔符，拼接数组中的元素，返回拼接后的字符串
        ```js
        string = 数组.join(分隔符)
        ```

## ES5加入的新方法

### 不影响内部数组元素（仅访问）

- 查找
    - 从头部的 fromIndex处 开始向后找，返回第一个找到的索引
        ```js
        数组.indexOf(要查的元素[, fromIndex])
        ```
    - 从尾部的 fromIndex处 向前开始找，返回第一个找到的索引
        ```js
        数组.lastIndexOf(要查的元素[, fromIndex])
        ```
    - 注意，对NaN会有强对比误判，谨慎使用

- 迭代
    - `forEach` 遍历数组，在callback函数中做处理，函数有三个参数：velue，index，array
        ```js
        数组.forEach(callback，指定callback的作用域)
        //注意，forEach无法通过break来中断遍历，只能用try方法抛出异常来中断跳出
        ```
    - `map` 遍历数组，在callback函数中做运算，并以数组返回所有运算后结果（一个新数组）
        ```js
        newArray = 数组.map(callback，指定callback的作用域)
        ```

    - `filter` 遍历数组，在callback函数中做筛选，函数如果返回true，就留下此元素，最终以数组返回所有留下的元素(一个新数组)
        ```js
        newArray = 数组.filter(callback，指定callback的作用域)
        ```

    - `every` 遍历数组，在callback函数中做判断，每个元素都返回true，最终结果才为true
        ```js
        bool = 数组.every(callback，指定callback的作用域)
        ```
    - `some` 遍历数组，在callback函数中做判断，每个元素都返回false，最终结果才为false
        ```js
        bool = 数组.some(callback，指定callback的作用域)
        ```
    - `reduce` 遍历数组，在累加器函数中做处理，total是总值，currentValue是每次迭代的元素值，currentIndex是每次迭代的索引值，initialValue是第一次迭代开始的初始值（可不写，默认0），最终返回总值
        ```js
        result = 数组.reduce(累加器函数(total, currentValue, currentIndex, arr){ }, initialValue)
    
        //还有反向遍历数组，在累加器函数中做处理
        数组.reduceRight( )
        ```

## ES6加入的新方法

### 会影响数组内部元素

- 整个操作
    - 从外部填充数据 到某段位置
        ```js
        数组.fill(替换数据源，开始替换的位置，结束替换的位置)
        ```
        - 比如`[1, 2, 3, 4, 5, 6].fill('a', 2, 4)`
            - 表示把a填到2号位和3号位，不包括4号
            - 结果是`[1, 2, 'a', 'a', 5, 6]`
    
    - 用自身填充数据 到某段位置
        ```
        数组.copyWithin(开始替换的位置，替换数据源的开始位置，替换数据源的结束位置)
        ```
        - 参数
            - 参数2可选，默认为0，可用负值表示从最后一个（-1）开始数
            - 参数3可选，默认为数组长度，直到无法读为止
        - 比如`[1, 2, 3, 4, 5].copyWithin(0, 3)`
            - 表示把3号位开始的4,5替换到0号位,1号位去
            - 结果是`[4, 5, 3, 4, 5]`

### 不影响内部数组元素（仅访问）

- 查找
    - 从头部开始向后找，条件语句返回true则代表符合，直接返回值
        ```js
        数组.find(function(value,index,arr){
            return 条件语句
        })
        ```
    - 从头部开始向后找，条件语句返回true则代表符合，直接返回索引
        ```js
        数组.findIndex(function(value,index,arr
            return 条件语句
        })
        ```
    - 从头部的fromIndex处开始向后找，返回布尔值，表示是否找到
        ```js
        数组.includes(要查的元素[, fromIndex])
        ```
        - 修复了indefOf中对NaN的强对比误判
            - 比如`[1, 2, NaN].indexOf(NaN);`会返回-1，是有问题的
            - 而`[1, 2, NaN].includes(NaN);`会返回true，没问题

- 遍历方法
    - 遍历值
        ```js
        for(let item of arr)
        //等价于
        for(let item of arr.values())
        ```
    - 遍历键
        ```js
        for(let index of arr.keys())
        ```
    - 遍历键值对 
        ```js
        for(let [index,value] of arr.entries())
        ```

- 转化方法(属于静态方法)
    - 把json对象转换成数组
        ```js
        Array.from(json对象)
        ```
        - 参数要满足：key必须是0，1，2（数字或字符串均可），还有length
    - 把一堆独立的数字，字符串或变量，合成数组
        ```js
        Array.of(数字1，字符串1，数字2，变量1....)
        ```

