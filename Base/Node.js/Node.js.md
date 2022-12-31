2022-09-29 13:37
Tags: #Nodejs
__
# Node.js

---
[[Install Nodejs]] - установки и дополнительные библиотеки...

---

chrome://inspect - это средство дебага

---

[[HTTP]] протокол...

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

