2025-04-13 18:19
Tags: #Interview #ProgrammingParadigms

- [Imperative vs Declarative](#Imperative%20vs%20Declarative)
- [Чистая функция](#Чистая%20функция)
- [side-effects](#side-effects)
- [Функции высшего порядка](#Функции%20высшего%20порядка)
- [Композиция](#Композиция)
- [Каррирование](#Каррирование)
- [Point-free стиль](#Point-free%20стиль)
- [Функциональные структуры данных](#Функциональные%20структуры%20данных)
- [OOP vs Functional](#OOP%20vs%20Functional)
- SOLID / YAGNI / DRY / KISS

---

### Imperative vs Declarative

**Императивное программирование** фокусируется на том, _как_ что-то должно быть сделано. Программа описывает последовательность шагов или инструкций, которые компьютер должен выполнить.

**Декларативное программирование** фокусируется на том, _что_ должно быть сделано. Программа описывает желаемый результат, не указывая, как его достичь.

---

### Чистая функция

Это функция, которая:

1. Детерминизм - всегда возвращает один и тот же результат при одних и тех же входных данных.
2. Не имеет побочных эффектов (например, изменение глобальных переменных, работа с файловой системой, сетевые запросы).

---

### side-effects

Это действия, которые функция выполняет помимо возврата значения:

- Изменение глобальных переменных.
- Выполнение сетевых запросов.
- Логирование в консоль.

---

### Функции высшего порядка

Это функции, которые принимают другие функции как аргументы или возвращают их как результат.

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // map — функция высшего порядка
```

---

### Композиция

Это процесс объединения нескольких функций в одну. Результат одной функции передается как вход для другой.

```js
const compose = (f, g) => x => f(g(x));
const add5 = x => x + 5;
const multiplyBy2 = x => x * 2;
const addAndMultiply = compose(multiplyBy2, add5);
console.log(addAndMultiply(10)); // (10 + 5) * 2 = 30
```

---

### Каррирование

Это преобразование функции с несколькими аргументами в последовательность функций.
```js
const add = a => b => a + b;
const add5 = add(5);
console.log(add5(3)); // 8
```

---

### Point-free стиль

Это стиль программирования, при котором функции создаются без явного упоминания аргументов.

```js
const double = x => x * 2;
const doubleAll = map(double); // Point-free стиль
```

---

### Функциональные структуры данных

Это структуры, которые являются иммутабельными (неизменяемыми).
- **Списки (List):** Неизменяемые коллекции элементов.
- **Стеки (Stack):** Структуры данных, работающие по принципу LIFO.
- **Очереди (Queue):** Структуры данных, работающие по принципу FIFO.
- **Деревья (Tree):** Иерархические структуры данных.
- **Мапы/Хэш-таблицы (Map/Hash Table):** Коллекции пар ключ-значение.

---

### OOP vs Functional

**OOP** :
- Основано на объектах, содержат состояние (данные) и поведение (методы).
- Акцент на мутабельности (изменении состояния).
- Использует принципы инкапсуляции, наследования и полиморфизма.

**Инкапсуляция** - механизм который объединяет данные и методы, работающие с этими данными.

**Наследование** - механиз позволяющий одним модулям обладать функциональностям других модулей.

**Полиморфизм** - это свойство функции одинаково обрабатывать различные типы объектов и классов

**Функциональное программирование** :
- Основано на функциях, которые являются первым классом граждан.
- Акцент на иммутабельности (неизменяемости данных).
- Минимизация побочных эффектов и использование чистых функций.

---
### Links
[[Interview]]
