2022-08-07 01:34
Tags: #JavaScript #Array 
__
# some()
Метод `some()` проверяет, удовлетворяет ли какой-либо элемент массива условию, заданному в передаваемой функции.
**Обратите внимание**: метод возвращает `false` при любом условии для пустого массива.

```ts
[2, 5, 8, 1, 4].some(el => el > 10);  // false

[12, 5, 8, 1, 4].some(el => el > 10); // true
```
Метод `some()` не изменяет массив, для которого он был вызван.
```js
const fruits = ['apple', 'banana', 'mango', 'guava'];

fruits.some(val => val === 'kela')    // false
fruits.some(val => val === 'banana')  // true
```

`true`, если функция проверки возвращает [truthy](https://developer.mozilla.org/ru/docs/Glossary/Truthy) значение хотя бы для одного элемента массива. Иначе, `false`.
__
### Links
[[Методы массива]]