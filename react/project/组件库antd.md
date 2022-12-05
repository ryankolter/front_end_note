# 组件库antd

## 安装并引用

- 安装

    ```bash
    npm i -S antd
    ```

- 必须引入样式
    ```ts
    import 'antd/dist/antd.css'
    ```

- 【例子】引入想用的组件

    ```ts  
    import { Button } from 'antd';
    ```
    - 使用
        ```ts
        <Button type="primary" onClick={clickBtn}>主按钮</Button>
        ```
        ```ts
        function clickBtn() {
            console.log("clickBtn");
        }
        ```

## 自定义主题色

## 组件

[所有组件示例 - Ant Design](https://012x.ant.design/docs/react/getting-started)

- 基础
    - `Button` 
        ```ts
        <Button type="primary" onClick={clickBtn}>主按钮</Button>
        ```
    - `Icon`
        ```ts
        <Icon type="link" />
        ```

- 表单
    - `Form`
        - `Form.Item`
        - `Input`

- 选项
    - 单选 `Radio`
    - 多选 `Checkbox`
    - 下拉选 `Select`
        - `Option` 
    - 级联选择 `Cascader`
    - 日期选择 `DatePicker`
    - 时间选择 `TimePicker`

- 实用块
    - 折叠面板`Collapse`  

- 导航
    - 菜单 `Menu`
    - 标签 `Tabs`
    - 面包屑 `Breadcrumb`
    - 分页 `Pagination`