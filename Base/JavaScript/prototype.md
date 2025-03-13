2022-08-19 21:34
Tags: #JavaScript 

`__proto__` - это специальное свойство объекта, (есть у всех объектов) и ссылается на `prototype` с помощью которого был создан и от которого текущий объект наследует свойства и методы.

`prototype` - это объект (есть у функций и классов) который будет использоваться в качестве прототипа для всех экземпляров, созданных через эту функцию с помощью оператора `new` 

---

`__proto__` - есть у всех объектов.
Почти всегда это объект. При том разые `__proto__`  разных по 'типу' объектов - они равны, то есть это один и тот же объект.
```js
const man = {};   // new Object(...)
const man2 = {};
man.__proto__ === man2.__proto__   // true

const users = [];   // new Array(...)
const users2 = [];
users.__proto__ === users2.__proto__   // true

const str = "string";   // new String(...)
const str2 = "string2";
str.__proto__ === str2.__proto__   // true

man.__proto__ === users.__proto__   //false
users.__proto__ === str.__proto__   //false
```
`__proto__` любого объекта ссылается на `prototype` класса (функцию-конструктора), с помощью которой этот объект был создан (сконструирован)

`prototype` - есть у class, либо function (у стрелочных функций его нет)
Каждый prototype - это незавичимый объект, сам по себе, с определённым набором свойст и методов.
```js
const promise = new Promise(()=>{});
promise.__proto__ === Promise.prototype   // true

const man = {}; // new Object(...)
man.__proto__ === Object.prototype   //true

const users = []; // new Array(...)
users.__proto__ === Array.prototype   //true

const str = "string"; // new String(...)
str.__proto__ === String.prototype   //true
```
---
## Object.setPrototypeOf
Метод **`Object.setPrototypeOf()`** устанавливает прототип (то есть, внутреннее свойство `[[Prototype]]`) указанного объекта в другой объект или `null`.
```js
Object.setPrototypeOf(obj, prototype);
```
`obj` - объект, которому устанавливается прототип.
`prototype` - новый прототип объекта (объект или `null`.

__
### Links
[[JavaScript]]
[prototype и __proto__ / JavaScript для собеседований](https://www.youtube.com/watch?v=b55hiUlhAzI)