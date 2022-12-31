2022-12-31 01:32
Tags: #MongoDB

---

`show databases` - список имеющихся баз данных (`show dbs`)
`use nameBD` - использоать БД или изменять колекции, если БД нет то она будет создана
`db.dropDatabase` - удалить БД

---

`db.createCollection("users")` - создать колекцию в БД
`show collections` - посмотреть колекции в БД

---
#### Добавление данных

`db.users.insert({name: "Vladimir", age: 29})` - добавить документ в колекцию
`db.users.insertMany([
{name: "Vladimir", age: 29},
{name: "Alex", age: 24}
])` - добавить несколько документов

---
#### Получение данных

`db.users.find()` - запрос на получение документа

`db.users.find({ _id: ObjectId("63af708193a78cedab23ba46")})` - получение по id

`db.users.find({age: 29, name: "Vova"})` - получение документа по критериям
`db.users.find({ $or: [{age: 29}, {name: "Vova"}]})` - получить документы с критериям или

`db.users.find({age: {$lt: 29}})` - меньше чем указанное число
`db.users.find({age: {$lte: 29}})` - меньше чем или равно указанного числа
`db.users.find({age: {$gt: 29}})` - больше чем указанное число
`db.users.find({age: {$ne: 29}})` - неравен задонному значению

`db.users.find().sort({age: 1})` - сортировать в прямом порядке
`db.users.find().sort({age: -1})` - сортировать в обратном порядке

`db.users.find().limit(3)` - ограничиваем количество возвращаемых документов

__
### Links
[[Базы данных]]
