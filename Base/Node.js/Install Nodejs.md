2022-12-29 20:31
Tags: #nodejs 
__
## Install

---
`npm init -y` - проинициализировать сервер 
`npm i -D typescript ` - установить TypeScript локально
`npm i @types/node -D ` - типизация для Node.js
`npx tsc --init` - проинициализировать TypeScript, создать tsconfig.json

---

`yarn add -D nodemon` - автоматическое обновление сервера
```json
"scripts": {
	"dev": "nodemon index.js",
	"inspect": "nodemon --inspect index.js"
},
```
---

- `yarn add express` - библиотека express
- `yarn add cors` - библиотека cors  
- `yarn add body-parser` - библиотека для работы с боди запроса

---
#### TypeScript:
- `yarn add typescript ts-node @types/node @types/express --dev` - добавить ts пакет
- `yarn tsc --init` - создаём файл для подключения ts в проекте 
в `tsconfig.json` поставить эти параметры `"rootDir": "./src"` `"outDir": "./dist"`
```JSON
"scripts": {
	"dev": "nodemon dist/index.js",  
	"inspect": "nodemon --inspect dist/index.js",
	"watch": "tsc -w",
	"build": "tsc",
	"start": "node dist/index.js"  
},
```
---
#### Подключение и работа с mongoDB базой данных:
- `npm i mongodb mongoose`

---
#### Работа с почтой: 
- Nodemailer - `yarn add nodemailer`

__
### Links
[[Node.js]]