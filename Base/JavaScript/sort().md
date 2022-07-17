2022-06-06 11:55
Tags: #JavaScript #Array
__
# sort()
Вызов `arr.sort()` сортирует массив  на месте, меняя в нём порядок элементов.

`!!! Не возвращает новый массив`
```js
arr.sort(fn) // Функция определяет порядок сортировки

arr.sort((a,b) => a - b) //сортировка по возврастанию / number
arr.sort((a,b) => b - a) //сортировка по убыванию / number

arr.sort(a,b) => a.name > b.name ? 1 : -1) // сортировка по алфавиту / string

arr.sort(a,b) => a.name.localeCompare(b.name)) // сортировка по алфавиту / string
```

__
### Links
[[Методы массива]]