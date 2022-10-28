2022-10-24 18:12
Tags: #ReduxToolkit #Redux 
__
# Redux Toolkit

Создаём store нашего приложения
```ts
//store.ts
import thunk from 'redux-thunk'
import {configureStore} from "@reduxjs/toolkit";

const rootReducer = combineReducers({  
    auth: authReducer,  
    app: appReducer,  
    todoList: todoListReducer,  
    tasks: tasksReducer  
})  
  
export const store = configureStore({  
    reducer: rootReducer,  
    middleware: getDefaultMiddleware => getDefaultMiddleware().prepend(thunk)  
})
```
---
Санки пишут сверху, принимают данные и возвращают данные через return
```ts
// Thunks
export const loginTC = createAsyncThunk<
    {isLoggedIn: boolean}, //тип возвращаемого объьекта
    LoginParamsType, // тип того что принимает санка
    {rejectValue: {errors: string[], fieldsErrors: string[]}} // тип ошибки
>('auth/login', async (date, thunkAPI) => {  
    thunkAPI.dispatch(setAppStatusAC({status: "loading"}))  
    try {  
        const res = await authAPI.login(date)  
        if (res.data.resultCode === RESULT_CODES.succeeded) {  
            thunkAPI.dispatch(setAppStatusAC({status: "succeeded"}))  
            return {isLoggedIn: true}  
        } else {  
            handleServerAppError(res.data, thunkAPI.dispatch)  
            return thunkAPI.rejectWithValue({errors: res.data.messages, fieldsErrors: res.data.fieldsErrors})  
        }    } catch (error) {  
        if (axios.isAxiosError(error)) {  
            handleServerNetworkError(error.message, thunkAPI.dispatch)  
            return thunkAPI.rejectWithValue({errors: error.message, fieldsErrors: undefined})  
        }  
        return thunkAPI.rejectWithValue({errors: undefined, fieldsErrors: 'someError'})  
    }  
})
```

```ts
const slice = createSlice({  
    name: 'tasks',  
    initialState,  
    reducers: {  
        getTasks(state, action: PayloadAction<{
            todolistId: string, tasks: TasksType[] 
        }>) {  
            state[action.payload.todolistId] = action.payload.tasks.map(el => 
                ({...el, entityStatus: 'idle'})
            )  
        },  
        ...
    },  
    extraReducers: (builder) => {  
        builder.addCase(addTodoListAC, (state, action) => {  
            state[action.payload.toDoList.id] = []  
        });  
        ...  
    }  
})
```

```ts
export const tasksReducer = slice.reducer  
export const getTasksAC = slice.actions.getTasks  
export const addTitleTaskAC = slice.actions.addTitleTask
...
```

---
### Test-ы
```ts
test('add title task', () => {  
    const action = createTaskTC.fulfilled(
	    newTask, // то что приходит из запроса
	    'requestId',
	    {todolistId: toDoListID_1, title: "Hello"} // то что принимает санка
	)  
    const tasksReducer1 = tasksReducer(tasks, action)  
    expect(tasksReducer1[toDoListID_1].length).toBe(3)  
    expect(tasksReducer1[toDoListID_1][0].title).toBe("Hello")  
})
```

__
### Links
[[Redux]]