# 路由库react-router

- 安装
    - 指令
        ```bash
        npm i -S react-router react-router-dom history
        ```
    - 目前推荐安装6.x版本
    - 区别
        - `react-router`负责计算底层路由逻辑
        - `react-router-dom`提供浏览器模块
            - 提供如下封装
                - `BrowserRouter`
                - `Link`
                - `URLSearchParamsInit`
                - `useSearchParams`
                - ...等等
            - 同理还有`react-router-native`用于提供App模块
        - `history`
            - 这个也要一并安装，不然报错
    
- 官网
    - [GitHub - remix-run/react-router](https://github.com/remix-run/react-router)

- 配置路由
    - 就是 某路径 与 渲染组件 的对应关系
    - 引入
        ```tsx
        import { Navigate, Route, Routes } from "react-router";
        ```
    - 组装一级路由
        ```tsx
        <Routes>
            <Route path={"/projects"} element={<ProjectList />} />
            <Route path={"/projects/:projectId/*"} element={<ProjectScreen />} />
            <Navigate to={"/projects"} />
        </Routes>
        ```
    - 组装二级路由
        ```tsx
        <Routes>
            {/*projects/:projectId/kanban*/}
            <Route path={"/kanban"} element={<KanbanScreen />} />
            {/*projects/:projectId/epic*/}
            <Route path={"/epic"} element={<EpicScreen />} />
            <Navigate to={window.location.pathname + "/kanban"} replace={true} />
        </Routes>
        ```
    - 写法解释
        - 整体用`<Routes>`和`</Routes>`包裹
        - 单个项用`<Route />`，里面填写
            - 要匹配的路径
            - 对应的自定义模块，
                - 路径匹配上后就渲染此模块
        - 最后有一个`<Navigate />`，里面填写
            - 如果路由是`/`啥都没有跟时，默认前往的路径

- 配置超链接
    - 就是点击后，跳到某路径
    - 引入
        ```tsx
        import { Link } from "react-router-dom";
        ```
    - 组装
        ```tsx
        <Link to={"kanban"}>看板</Link>
        ```