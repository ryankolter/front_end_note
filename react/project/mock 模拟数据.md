# mock 模拟数据

## 不推荐的老方案

- 代码侵入（不推荐）
    - 在代码里写死，或者请求本地JSON文件
    - 缺点
        - 之后与服务端联调会很麻烦，还要删改

- 请求拦截（稍微好一点）
    - 借助 `mock.js`
    - 例子
        ```js
        Mock.mock(/\/api\/list/, 'get', {
            code: 2000,
            msg: 'ok'.
            'data|10': [
                {
                    "id|+1": 6,
                    "name": "@csentence(5)"
                }
            ]
        })
        ```
    - 优点
        - 与代码分离
        - 可生成随机数据
    - 缺点
        - 动态生成的假数据，无法模拟真实的增删改查
        - 只支持 ajax， 不支持 fetch

- 接口管理工具（太复杂，不推荐）
    - 比如 rap，swagger，moco，yapi
    - 优点
        - 配置功能强大，后端修改接口，mock也跟着更改
    - 缺点
        - 配置复杂，依赖后端
        - 大团队才有精力做这种基础建设

## 推荐的新方案（json-server）

- 属于本地node服务器
    - github地址：https://github.com/typicode/json-server
    - 优点
        - 配置简单，0代码30秒启动一个REST API Server
        - 自定义程度高
        - 真实模拟 增删改查
- 科普一下 REST API
    - 一句话： URL 代表 资源、对象，METHOD 代表 行为
    ```js
    GET /tickets   列表
    GET /tickets/12   单个详情
    POST /tickets   新增
    PUT /tickets/12   整个替换
    PATCH /tickets/12   部分修改
    DELETE /tickets/12   删除
    ```

- 全局安装并试用(可跳过)
    - 全局安装
        ```bash
        npm i -g json-server
        ```

    - 创建 db.json文件 存放模拟数据
        ```json
        {
          "posts": [
            { "id": 1, "title": "json-server", "author": "typicode" }
          ],
          "comments": [
            { "id": 1, "body": "some comment", "postId": 1 }
          ],
          "profile": { "name": "typicode" }
        }
        ```
    - 启动
        ```bash
        json-server --watch db.json
        ```
    - 请求测试
        - 请求 GET `http://localhost:3000/posts`
            - 得到列表
        - 请求 POST `http://localhost:3000/posts`
            - 请求体为 raw 的 json 格式
            - 可增加一条数据到 db.json，自动编号为2
        - 请求DELETE `http://localhost:3000/posts/2`
            - 可删除 刚刚添加的 编号为2的数据

- 集成到我们的react项目
    - 项目内安装
        ```bash
        npm i json-server -D
        ```
    - 根目录下新建文件夹`__json_server_mock__`
        - 文件夹里面放项目用到的 db.json
    - 打开 package.json 添加一条 scripts脚本
        ```json
        "json-server": "json-server __json_server_mock__/db.json --watch --port 3001"
        ```
        - 这里默认是 3000 端口，根react项目冲突了，需要设置成3001端口
    - 启动脚本
        ```bash
        npm run json-server
        ```
    - 在代码中使用
        - 不妥当的方式
            ```js
            fetch("http://localhost:3001/posts")
            ```
        - 推荐的方式
            - 在根目录下，新建`.env.development`文件
                - 加入一个开发环境变量
                    ```js
                    REACT_APP_API_URL=http://localhost:3001
                    ```
            - 同样新建`.env`文件
                - 加入一个正式环境变量
                    ```js
                    REACT_APP_API_URL=正式服务器地址
                    ```
            - 使用此环境变量
                ```js
                const apiUrl = process.env.REACT_APP_API_URL;   
                fetch(`${apiUrl}/posts`)
                ```
            - npm如何知道，用 开发的 还是 正式的 变量
                - 当我们执行`npm start`时，会自动用开发的
                - 当我们执行`npm run build`时，会自动用正式的
    - 配置中间件
        - `__json_server_mock__` 文件夹里面新建middleware.js，按后端commonjs规范写
            ```js
            module.exports = （req, res, next) => {
                if(req.method === 'POST' && req.path === '/login'){
                    if(req.body.username === 'jack' && req.body.password === '123456'){
                        return res.status(200).json({
                            user: {
                                token: '123'
                            }
                        })
                    }else{
                        return res.status(404).json({
                            message: "error"
                        })
                    }
                }
                netx();
            }
            ```
        - 为scripts脚本添加参数，变成如下：
            ```json
            "json-server": "json-server __json_server_mock__/db.json --watch --port 3001 --middlewares __json_server_mock__/middleware.js"
            ```
    