# css-in-js库emotion

- (不推荐)安装`@emotion/react`
    - 指令

        ```bash
        npm i -S @emotion/react
        ```

    - 利用css属性内嵌
        ```ts
        import { css, tsx } from '@emotion/react'
        ```
        - 定义的同时，使用
            - 字符串
                ```ts
                render(
                    <div css={css`
                        padding: 32px;
                        font-size: 24px;
                    `}> my btn </div>
                )
                ```
            - 或者 对象
                ```ts
                render(
                    <div css={{
                        padding: 32px;
                        font-size: 24px;
                    }}> my btn </div>
                )
                ```

- (推荐)安装`@emotion/styled`
    - 指令
        ```bash
        npm i -S @emotion/styled
        ```
    - 利用styled组件定义
    ```ts
    import styled from '@emotion/styled'
    ```
    - 先定义
        - 字符串类型
            ```ts
            const myButton = styled.div`
                padding: 32px;
                font-size: 24px;
            `
            ```
        - 或者 函数类型
            ```ts
            const myButton = styled.div(props => ({
                padding: '32px',
                fontSize: '24px'
            }))
            ```
            - 可以与字符串类型结合，只要加入到第2、第3..个参数即可
    - 再使用
        ```ts
        render(
            <myButton> my btn </myButton>
        )
        ```
        
- 样式复用
    ```ts
    const base = css`
        padding: 32px;
        font-size: 24px;
    `
    ```
    ```ts
    render(
        <div css={css`
            ${base};
            background-color: #eee;
        `}> my btn </div>
    )
    ```
