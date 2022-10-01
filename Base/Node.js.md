2022-09-29 13:37
Tags: #Nodejs
__
# Node.js

---
HTTP протокол имеет 4 основных метода:
- GET - получить данные
- POST - создать данные
- PUT - изменить данные
- DELETE - удалить данные
---
Создание endPoint на сервере выглядит примерно так:
```js
function getUsers() {
	const users = database.fildUsers()
	return users;
}

app.get('/api/users', getUsers)
```
---
`yarn init -y` - y проинициализировать сервер
`yarn add express pg pg-hstore sequelize cors dotenv` - доп библиотеки
`yarn add -D nodemon` - автоматическое обновление сервера

`yarn add express` - библиотека express
`yarn add cors` - библиотека cors
`yarn add body-parser` - библиотека лоя работы с боди запроса

__
### Links

