2022-06-07 21:36
Tags: #React #hook
__
# useState
Хук состояния
UseState - возвращает значение с состоянием и функцию для его обновления. Работает асинхронно.

```jsx
  const [age, setAge] = useState(42);
  
  const [fruit, setFruit] = useState('банан');
  
  const [todos, setTodos] = useState([{ text: 'Изучить хуки' }]);
```

```jsx
const [count, setCount] = useState(0); // объявляем переменную состояния

const [значение, функция] = useState(первоначальное значение)
```

- count - это переменная
- setCount - функция для изменения переменной
- 0 - первоночальное значение

```jsx
setCount(5) // count будет изменен на 5, и перерисован ДОМ
```

Если в первоночальное значение передать функцию то она будет выполнена только один раз, при отрисовке.
```tsx
function generateDate() {   
    return 1  
}

const [count, setCount] = useState(generateDate)

setCount(state => state + 1)
```
Если в функции изменению (setCount) поместить колбек, то он будет принимать state.
__
### Links
[[hook (Хуки)]]