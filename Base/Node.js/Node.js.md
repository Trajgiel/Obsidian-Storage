2022-09-29 13:37
Tags: #nodejs
__

Переключение версий с помощью nvm
```bash
nvm install node //установить самую новую версию ноды
nvm install 18.0.0   //установить нужную версию Node.js
nvm list   //список уже установленных версий Node.js
nvm use 5.1.0   //переключиться на Node.js нужной версии
```

---
[[Install Nodejs]] - установки и дополнительные библиотеки...

chrome://inspect - это средство дебага

---

[[HTTP]] протокол...

[[Stream (поток)]]

[[Auth]] - IAM (Identity and Access Management) процессы, связанные с **аутентификацией**, **авторизацией**, а также управлением доступом и идентификацией...

---

[[Nest.js]] - это фреймворк для создания эффективных и масштабируемых се￼￼Содержание:рверных приложений [Node.js](https://nodejs.org/).


---
Создание endPoint на сервере выглядит примерно так:
```js
function getUsers() {
	const users = database.fildUsers()
	return users;
}

app.get('/api/users', getUsers)
```

__
### Links

