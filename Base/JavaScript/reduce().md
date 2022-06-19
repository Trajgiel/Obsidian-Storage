2022-06-17 00:00
Tags: #JavaScript 
__
# reduce()
Вычисление единого значения на основе всего массива

```js
const nums = [10, 20, 30] //sum

nums.reduce((acc, cur) => acc + cur, 0) // 60
//acc - общий результат
//cur - элемент (следующий)
//0 - первоночальное значение
```


```js
let students = [  
    {  
        id: 1,  
        name: "Bob",  
        age: 22,  
        isMarried: true,  
        scores: 85  
    },  
    {  
        id: 2,  
        name: "Alex",  
        age: 21,  
        isMarried: true,  
        scores: 89  
    },  
    {  
        id: 3,  
        name: "Nick",  
        age: 20,  
        isMarried: false,  
        scores: 120  
    }
];

students.reduce((acc, cur) => acc.scores > cur.scores ? acc : cur)//ищем максимум
students.reduce((acc, cur) => acc + cur.scores, 0)//сумма значений

students.reduce((acc, cur) => acc.push({...cur, scores: cur.scores + 10}), [])
//создаём новый массив, пушим элементы, внутри изменяем значение
```
[].push()
```js
const NewStudents = students.reduce((acc, cur) => {  
    acc[cur.id] = {...cur};  //создаём ключ и даём ему значение (новый массив)
    delete acc[cur.id].id;  // удаляем id из значения
    return acc; 
}, {})

NewStudents = {   // создали новый объект
    1: {  
        name: "Bob",  
        age: 22,  
        isMarried: true,  
        scores: 85  
    },
	...    
}

```
__
### Links
[[Методы массива]]