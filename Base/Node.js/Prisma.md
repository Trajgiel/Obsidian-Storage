2025-01-05 20:30
Tags: #prisma

Это современное ORM (Object-Relational Mapping) для [Node.js](https://nodejsdev.ru/) и [TypeScript](https://scriptdev.ru/).

Проще говоря, Prisma — это инструмент, позволяющий работать с реляционными (PostgreSQL, MySQL, SQL Server, SQLite) и нереляционной (MongoDB) базами данных с помощью JavaScript или TypeScript без использования SQL (хотя такая возможность имеется).

---

Установка prisma в проект
```
npm i -D @prisma/client
npx prisma init
```

Создание миграции
```
npx prisma migrate dev --name initialization
```

---

```json
model UserModel {
  id                Int                   @id @default(autoincrement())
  email             String                @unique
  firstName         String
  lastName          String
  age               Int
  hashPassword      String                @map("hash_password")
  
  createdAt         DateTome              @default(now())
  updatedAt         DateTome              @uodatedAt

  @@map("users")
}
```

---
### Links
[[Node.js]]