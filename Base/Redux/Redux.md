2022-07-10 21:02
Tags: #Redux
__
# Redux
Redux — библиотека для JavaScript с открытым исходным кодом, предназначенная для управления состоянием приложения. Чаще всего используется в связке с React или Angular для разработки клиентской части. Содержит ряд инструментов, позволяющих значительно упростить передачу данных хранилища через контекст.

Весь код нужно обернуть в тег `Provider`:
```tsx
ReactDOM.render(  
    <Provider store={store}>  
        <App/>  
    </Provider>  
    ,  document.getElementById('root')
);
```

Код в отдельном файле `store.ts`
```ts
const rootReducer = combineReducers({  
    todoList: todolistsReducer,  
    tasks: tasksReducer  
})  
  
export type AppRootStoreType = ReturnType<typeof rootReducer>  
  
export const store = createStore(rootReducer)
```

- `combineReducers` - формирует один [[reducer]] из готовых маленьких редьюсеров
- `createStore` - создаёт `store` который хронит состояние приложения
---
- [[reducer]] - это чистая функция которая принимает state, принимает action...
- [[action (Action Creators)|action]] - это объект у которого обязательно есть свойство `type`...
---
- [[useDispatch]]
- [[useSelector]]

__
### Links
