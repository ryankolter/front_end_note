# useEffect

- 用来定义`副作用`，可以替代以前的生命周期

- 【场景1】无需清理的副作用: 
    - 我们希望 在 React 更新 DOM 之后，运行一些额外的代码，这种属于 副作用，比如 网络请求、手工 DOM 修改和日志记录

        ```ts
        useEffect(() => {
            document.title = `You clicked ${count} times`;
        });
        ```
    - 这样子，网页的标题就会随着每次渲染(无论是第一次mount还是后面的update)，而触发副作用，进而变更
    - 如果要用以前的类去写，会很麻烦，需要 componentDidMount 和 componentDidUpdate，像下面这样
        ```ts
        componentDidMount() {
            document.title = `You clicked ${this.state.count} times`;
        }

        componentDidUpdate() {
            document.title = `You clicked ${this.state.count} times`;
        }
        ```
- 【场景2】需要清理的副作用: 
    - 我们希望 组件 卸载之后，运行一些额外的代码，也属于副作用
        ```ts
        useEffect(() => {
            ChatAPI.subscribeIt(props.friend.id, handleStatusChange);
            return function cleanup() {
                ChatAPI.unsubscribeIt(props.friend.id, handleStatusChange);
            };
        });
        ```
        - 这样子，会在卸载之后，自动执行里面返回的清理函数
        - 如果要用以前的类去写，会很麻烦，需要 componentDidMount 和 componentWillUnmount，像下面这样
            ```ts
            componentDidMount() {
                ChatAPI.subscribeToFriendStatus(
                    this.props.friend.id,
                    this.handleStatusChange
                );
            }

            componentWillUnmount() {
                ChatAPI.unsubscribeFromFriendStatus(
                    this.props.friend.id,
                    this.handleStatusChange
                );
            }
            ```