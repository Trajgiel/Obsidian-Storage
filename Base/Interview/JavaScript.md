2025-04-13 19:48
Tags: #Interview #JavaScript 

- [V8](#V8)
- [Garbage Collector](#Garbage%20Collector)
- [Event Loop](#Event%20Loop)
- [Web Workers / Service Workers](#Web%20Workers%20/%20Service%20Workers)
- [Object.freeze](#Object.freeze)
- [Object.seal](#Object.seal)
- [Object.preventExtensions](#Object.preventExtensions)
- [Object.defineProperty](#Object.defineProperty)
- [Context (Arrow Functions, bind / call / apply)](#Context%20(Arrow%20Functions,%20bind%20/%20call%20/%20apply))
- [Promises and async/await](#Promises%20and%20async/await)
- [Function Generator](#Function%20Generator)
- [Meta Programming (Symbols, Reflect, Proxy)](#Meta%20Programming%20(Symbols,%20Reflect,%20Proxy))
- [void](#void)

---
### V8

Это движок JavaScript. Он используется в браузере Chrome и Node.js.
Основные этапы работы V8:
1. **Парсинг:** Код преобразуется в абстрактное синтаксическое дерево (AST).
2. **Компиляция:** AST компилируется в машинный код с помощью JIT-компилятора (Just-In-Time).
3. **Оптимизация:** V8 использует оптимизации, такие как Inline Caching и Hidden Classes, для улучшения производительности.

---

### Garbage Collector

JavaScript автоматически управляет памятью через механизм Garbage Collector:
- **Выделение памяти:** Когда создаются переменные, объекты или функции, память выделяется автоматически.
- **Сборка мусора:** GC освобождает память, которая больше не используется (например, когда ссылки на объекты теряются).

**Утечки памяти** возникают, когда память не освобождается, несмотря на то что она больше не нужна. Примеры:
- Забытые таймеры (`setInterval`).
- Неправильное использование замыканий.
- Ссылки на DOM-элементы, которые были удалены из документа.

---

### Event Loop

Это механизм, который позволяет JavaScript обрабатывать асинхронные операции, оставаясь однопоточным. Его работа:

1. **Call Stack:** Выполняет синхронный код.
2. **Web APIs:** Браузер предоставляет API для асинхронных операций (таймеры, запросы).
3. **Callback Queue:** Асинхронные операции помещаются в очередь после завершения.
4. **Event Loop:** Проверяет, пуст ли Call Stack, и передает задачи из очереди в стек.

---

### Web Workers / Service Workers

**Web Workers:** Позволяют выполнять JavaScript в фоновом потоке, не блокируя основной поток UI. Используются для тяжелых вычислений.

**Service Workers:** Это скрипты, которые работают в фоновом режиме и управляют сетевыми запросами, кэшированием и офлайн-функциональностью. Часто используются для реализации PWA (Progressive Web Apps).

---

### Object.freeze

Делает объект полностью неизменяемым:

- Нельзя добавлять новые свойства.
- Нельзя удалять существующие свойства.
- Нельзя изменять значения существующих свойств.

---

### Object.seal

- Нельзя добавлять новые свойства.
- Нельзя удалять существующие свойства.
- Можно изменять значения существующих свойств.

---

### Object.preventExtensions

- Нельзя добавлять новые свойства.
- Можно изменять значения существующих свойств.
- Можно удалять существующие свойства.

---

### Object.defineProperty

Позволяет точно определить или изменить одно свойство объекта, задавая его дескриптор

---

### Context (Arrow Functions, bind / call / apply)

- **Обычные функции:** `this` определяется в момент вызова (зависит от контекста вызова).
- **Стрелочные функции:** `this` берется из лексического окружения (где функция была объявлена).

Методы для изменения контекста:

- `bind`: Создает новую функцию с привязанным контекстом.
- `call` и `apply`: Вызывают функцию с указанным контекстом.

---

### Promises and async/await

**Promises:** Это объекты, представляющие результат асинхронной операции, который может быть выполнен успешно (`resolved`) или завершиться ошибкой (`rejected`).
```js
const fetchData = () =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve("Data"), 1000);
  });

fetchData()
  .then((data) => console.log(data)) // Data
  .catch((err) => console.error(err));
```

- **async/await:** Синтаксический сахар над Promises, упрощающий работу с асинхронным кодом.
```js
async function getData() {
  try {
    const data = await fetchData();
    console.log(data); // Data
  } catch (err) {
    console.error(err);
  }
}
getData();
```

---

### Function Generator

Это функции, которые могут приостанавливать свое выполнение и возобновлять его позже. Они используют ключевое слово `function*` и `yield`.

```js
function* generator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = generator();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

---

### Meta Programming (Symbols, Reflect, Proxy)

**Symbols:** Уникальные идентификаторы, используемые как ключи объектов.
```js
const id = Symbol("id");
const obj = { [id]: 123 };
console.log(obj[id]); // 123
```

**Reflect:** API для работы с объектами, предоставляющее методы для выполнения операций
```js
const obj = { a: 1 };
console.log(Reflect.get(obj, "a")); // 1
```

**Proxy:** Позволяет перехватывать и переопределять операции над объектами.
```js
const handler = {
  get(target, prop) {
    return prop in target ? target[prop] : "Default";
  },
};
const proxy = new Proxy({ a: 1 }, handler);
console.log(proxy.a); // 1
console.log(proxy.b); // Default
```

---

### void

Используется для указания, что выражение или функция не возвращает никакого значения (то есть возвращает `undefined`).

---
### Links
[[Interview]]