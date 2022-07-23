2022-07-10 20:12
Tags: #React #hook 
__
# useReduser
```tsx
const [state, dispatch] = useReducer(reducer, initialArg, init);
```
- state - наш стейт, переменная в которой хранятся данные
- dispatch - функция которая оправляет в reducer наш action
- reducer - функция которая принимает state и action, возвращает новый state
- initialArg - первоночальное значение state
- init - функция которая создаёт начальное состояние лениво, init(initialArg)

Альтернатива для [[useState]]. Принимает редюсер типа `(state, action) => newState` и возвращает текущее состояние в паре с методом `dispatch`.

Вот пример счётчика, переписанный для использования редюсера:
```tsx
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```
__
### Links
[[hook (Хуки)]]
