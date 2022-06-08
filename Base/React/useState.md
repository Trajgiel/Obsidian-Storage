2022-06-07 21:36
Tags: #React 
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
__
### Links
[[Хуки]]