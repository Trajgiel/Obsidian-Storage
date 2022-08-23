2022-07-31 21:08
Tags: #JavaScript #promise
__
# Promise
**Промис - это объект, у которого есть 3 состояния и методы then, catch, finally**

Промис (обещание) - это объект, который может находится в одном из 3 состояний (PromiseStatus ):  
1. `pending` (в процессе выполнения обещания)
2. `rejected` (обещание не выполнил)
3. `resolved` (обещание выполнил) 

Свойства PromiseStatus и PromiseValue – внутренние свойства объекта Promise и мы не имеем к ним прямого доступа.  
Для обработки результата следует использовать методы .then, .catch, .finally.

Когда обещание выполнится мы можем узнать об этом, подписавшись (отдав колбек)
с помощью метода промиса - then

Как и любой объект промис создаётся с помощью функции конструктора.

---
Создаётся промис с помощью конструктора `new Promise` и передаёт туда `executor`
```ts
const promise = new Promise(executor: (resolve, reject) => {...})
```
- executor - это функция которая принимае два оргумента `resolve`, `reject`.
```js
const promise = new Promise((resolve, reject) => {  
    setTimeout(() => {  
        resolve({name: 'Vladimir'})    // успешное выполнение  
        //reject('Some error')         //не выполнено    
    }, 2000)  
})
```
 - resolve - результат успешного выполнение.
 - reject - результат ошибки, не выполнено.

---
У экземпляра промиса есть методы для работы (`then`, `catch`, `finally`)
```js
promise.then(  
    (data) => { console.log(data) }, //при успешном выполнении - resolve  
    (err) => { console.log(err) }    //при ошибке - reject  
)

promise.then(    //при передачи одного callBack выполняется результат resolve  
    (data) => {console.log(data)}  
)  
promise.catch(   // используется только для получения отрицательного реультата  
    (err) => { console.log(err) }  
)  
promise.finally(        // выполняется влюбом случае не зависимо от результата  
    ()=> { console.log('Inside finally')} //нечего не передоётся в колбек  
)

promise                 // чаще всего исмпользуется этот вариант  
    .then((data) => {})  
    .catch((err) => {})
```

### Цепочка промисов
Все методы возвращают промисы и мы можем выстраивать их в цепочки
```js
promise  
    .then((date) => {  
        console.log(date)  
        return 2   // res(2) // new Promise((res) => {return res}
    })  
    .then((date) => {  
        console.log(date)  
        return 3   // res(3) // new Promise((res) => {return res}
    })  
    .then(date => {  
        console.log(date)  
    })
```

### Обработка ошибок
```js
promise3  
    .then((date) => {  
        console.log(date)  
    })  
    .catch(err => {  
        console.log(err)  
    })
```

## async, await
- `async` - делаю функцию осинхронной (промисом). Ставится только перед вызовом той функции что возвращает промис.
- `await` - пока не выполнится это действие, код ниже не выполняется
```js
const getUsersAsync = async() => {  //означает что функция осинхронная - async  
    try {  
        const users = await axios.get('https://vk.com/users')  
        const user = await axios.get('https://vk.com/user')  
        const books = await axios.get('https://vk.com/books')  
    }  
    catch (e) {console.log(e)}
    finally { ... }
}

getUsersAsync()  
    .then( data => console.log(data))

```

### Статические методы
Статические методы не доступны экземплярам этого класса или этой функции конструктора. Возвращают новый промис.
- `Promise.all()` - ждёт пока все промисы буду выполнены, если ошибка нечего не вернёт
- `Promise.race()` - при выполнении первого промиса не выполняет остольные
- `Promise.allSettled()` - выполняет все промисы, независимо от их выполнения или нет
- `Promise.resolve()` - вернёт сразу промис в котором есть resolve()
- `Promise.reject()` - вернёт сразу промис в котором есть reject()
- т.д.
```js
const p1 = new Promise(res => {setTimeout(()=> {res(3)}, 3000)})  
const p2 = new Promise(res => {setTimeout(()=> {res(2)}, 2000)})  
const p3 = new Promise((res, rej) => {setTimeout(()=> {rej(1)}, 1000)})  
  
Promise  
    .all([p1, p2, p3]) 
    .then(console.log)  

Promise  
    .race([p1, p2, p3])  
    .then(console.log)  

Promise  
    .allSettled([p1, p2, p3])
    .then(console.log)
    
const p4 = Promise.resolve()
const p5 = Promise.reject()
```

### Промисификация
Промисификация - из кода котрый не работае с промисами деаем код который возвращает нам промис
```js
function get(url, callBack) {  
    if (url) callBack(null, 'Some Data')  
    else callBack({message: 'Invalid url'}, null)  
}  
  
//Пишим обёртку для обычного кода что бы он начал роботать с промисами  
function promisifyGet(url) {  
    return new Promise((res, rej) => {  
        get(url, (err, data) => {  
            if (err) rej(err)  
            else res(data)  
        })  
    })  
}
```
__
### Links
[[JavaScript]]
