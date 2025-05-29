2025-05-29 20:32
Tags: #



---

```js
function Count() {
  let counter = 0
  return () => {
    console.log(counter++)
  }
}

const c = new Count()
c()
c()
c.counter = 0
c()

const b = new Count()
b() 
```
Что выведет в консоль?

---

```js
for (var i = []; i.length < 3; i.push(2)) {
  setTimeout(() => {
    console.log(i);
  }, i.length * 1000);
} 
```
Что выведет в консол? Как исправить? два решения:
- создание переменной (замыкание)
- параметры setTimeout((arg) => {}, time, arg, ...)

---



---
### Links
[[Interview]]