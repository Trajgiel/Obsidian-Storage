2022-08-25 17:52
Tags: #Redux #Thunk
__
# Thunk
Redux Thunk - это библиотеки промежуточного ПО, позволяющее вызывать создателей действий, которые возвращают функцию вместо объекта действия. Эта функция получает метод обработки приложения, который затем используется для обработки регулярных синхронных действий внутри тела функции после выполнения асинхронных операций.

```
yarn add redux-thunk - установить библиотеку thunk
```
`thunk` - это функция которой разрешено делать side-effect, принимает два праметра: `dispatch` и `getState`. Является частью описания бизнес логики, делает `dispatch actions` 

---
Примените промежуточное ПО при создании приложения, использует команду Redux `applyMiddleware`. Файл `store.ts` будет выглядеть следующим образом:
```ts
import { tasksReducer } from './tasks-reducer';  
import { todolistsReducer } from './todolists-reducer';  
import {applyMiddleware, combineReducers, createStore} from 'redux';  
import thunk from 'redux-thunk'  
  
const rootReducer = combineReducers({  
    tasks: tasksReducer,  
    todolists: todolistsReducer  
})  

export const store = createStore(rootReducer, applyMiddleware(thunk));

export type AppRootStateType = ReturnType<typeof rootReducer>
```
Мы импортировали Redux Thunk и добавили его в наше приложение, с помощью `applyMiddleware(thunk)`

---
```ts
export const getTaskTC = (todoListsID: string) =>  
    (dispatch: Dispatch) => {  
        todolistsAPI.getTasks(todoListsID)  
            .then(res => {  
                dispatch(setTasksAC(todoListsID, res.data.items))  
            })  
    }
```
---
После получения метода `dispatch` от состояния функция, возвращаемая создателем асинхронного действия с Redux Thunk, также получает метод `getState`, что позволяет прочитать текущие значения store:
```ts
export const getTaskTC = (todoListsID: string) =>  
    (dispatch: Dispatch, getState: () => AppRootStateType) => {
		const tasks = getState().tasks[todoListsID]
        ...
    }
```
Получили на прямую нужные данные

---


__
### Links
[[Redux]]