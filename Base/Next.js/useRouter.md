2023-07-18 20:44
Tags: #nextjs #hooks

---

[useRouter](https://nextjs.org/docs/pages/api-reference/functions/use-router) - получение доступа к маршрутизатору внутри любого компонента
```tsx
const router = useRouter()
```

Методы:
- asPath - возвращает url ( `...car/1` )
- pathname - возвращает системный url ( `...car/[id]` )
- query - возвращает динамические параметры (  `query.id = 1` )

push - переход на нужный url (  `push(/hame/page)` )

---
### Links
[[hooks]]
