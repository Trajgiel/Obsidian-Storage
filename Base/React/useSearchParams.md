2022-10-06 02:07
Tags: #hook 
__
# useSearchParams
 
 ---
Взять данные из URL
```tsx
// ...URL/profile?page=2&pageCount=25&name=Vova

const [searchParams, setSearchParams] = useSearchParams()

const pageURL = searchParams.get('page')  
const pageCountURL = searchParams.get('pageCount')  
const nameURL = searchParams.get('name')
```
---
Добавить данные в URL
```tsx
const [searchParams, setSearchParams] = useSearchParams()

setSearchParams({name: 'Vova', age: '29'})

// ...URL/profile?name=Vova&age=29
```
__
### Links
[[hook (Хуки)]]