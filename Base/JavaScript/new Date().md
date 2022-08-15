2022-07-24 11:20
Tags: #JavaScript
__
# new Date()
new Date() - cоздаёт объект `Date` с текущей датой и временем:

```tsx
const now = new Date();
```

Для доступа к компонентам даты-времени объекта `Date` используются следующие методы:

- getFullYear() - получить год (из 4 цифр)
- getMonth() - получить месяц, от 0 до 11
- getDate() - получить число месяца, от 1 до 31
- getHours() - получить часы
- getMinutes() - получить минуты
- getSeconds() - получить секунды
- getMilliseconds() - получить милисекунды
- getDay() - получить номер дня в неделе, 0(воскресенье) - 6(суббота)

```tsx
const date = new Date();  // текущая дата

date.getHours();          // час в текущей временной зоне
date.getMinutes();        // минуты
date.getSeconds()         // секунды
```


__
### Links
[[Конструкторы]]