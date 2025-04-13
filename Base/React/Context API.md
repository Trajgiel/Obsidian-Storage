2022-07-10 13:21
Tags: #React 
__
# Context API

storeContext.ts
```tsx
import React from "react";  
  
export const StoreContext = React.createContext(null)
```
Создаём Context в отдельном файле

index.ts
```tsx
<StoreContext.Provider value={store}>  
    <App/>  
</StoreContext.Provider>
```
Всем внутри App будет доступен нашь store. Обрамляем все наши компоненты и доём им доступ к Context

Любая Контейнерная компонента
```tsx
<StoreContext.Consumer>  
    {(store) => {
    ...
        return (
	        <ПрезентационнаяКомпонента/>
        ) 
         
    }}   
</StoreContext.Consumer>
```
С помощью Consumer мы обращаемся к Context и берём из него store и прокидываем в Презентационная компонента


__
### Links
[[Base/React/React]]