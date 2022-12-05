# useContext

- 在函数子组件内引入 上下文对象，并取出其中的变量或函数，供子组件使用

- 【场景】引入全局上下文`GlobalContext` 
    ```js
    //任意一个底层子组件
    import { useContext } from 'react';
    import { GlobalContext } from '../../GlobalProvider';

    const { currentId, setCurrentId } = useContext(GlobalContext);

    return (
        <div>{currentId}</div>
    );
    ```

    - 这里依赖于一个文件`GlobalProvider.tsx`，里面提供了GlobalContext（用于底层子组件，进行取出） 以及 GlobalProvider（用于顶层父组件，进行注入）
        ```js
        import { useState } from 'react';
        export const GlobalContext = createContext(initContext);

        export const GlobalProvider = ({ children }: { children: React.ReactNode }) => {
            const [currentId, setCurrentId] = useState();

            return (
                <GlobalContext.Provider
                    value={{
                        currentId,
                        setCurrentId
                    }}
                >
                    {children}
                </GlobalContext.Provider>
            )
        }
        ```
        - 选择要注入的顶层父组件，这里可指定为App，在`index.tsx`文件中配置
            ```js
            import { createRoot } from 'react-dom/client';
            import { GlobalProvider } from './GlobalProvider';
            import App from './App';

            const container = document.getElementById('root');
            const root = createRoot(container!);
            root.render(
                <GlobalProvider>
                    <App />
                </GlobalProvider>
            );
            ```
    - 如果要用以前的类去写，会很麻烦，需要自己在组件树中书写 GlobalContext.Consumer，使用value，导致层级加深
        ```js
        import { GlobalContext } from '../../GlobalProvider';

        return (
            <GlobalContext.Consumer>
                { value => 
                   <div>{value.currentId}</div>
                }
            </GlobalContext.Consumer>
        );
        ```
        
            
        
        