2022-06-04 23:45
Tags: #typeScript
__

TypeScript — язык программирования, представленный Microsoft в 2012 году и позиционируемый как средство разработки веб-приложений, расширяющее возможности [[JavaScript]]. Разработчиком языка TypeScript является Андерс Хейлсберг, создавший ранее Turbo Pascal, Delphi и C#.

TypeScript — является строго типизированным языком, и каждая переменная и константа в нём имеет определённый тип.  
Мы не можем динамически изменить ранее указанный тип переменных.

## Содержание:
- [Type](#type)
- [Interface](#Interface)
- [Enum](#enum)
- [Generic](#Generic)
- [Утилиты типов](#утилиты_типов)
- [Декораторы](#декораторы)
- [tsconfig.json](#tsconfig.json)

---

## Type
```ts
const a: number = 10;
const b: string = 'Hello';
const c: boolean = true;

type UserType = {
	age: number,
	name: string
}

const arr:number[] = [1, 2, 3, 4, 5]
```

Создания массива который нельзя изменить (только для чтения)
```ts
const arr:ReadonlyArray<number> number[] = [1, 2, 3, 4, 5]
```

**Типизация функции**, типизируются параметры и то что возвращает функция
```ts
const gerString = (name: string): string => {  
  return name  
}
// или
type FunctionType = (name: string) => string
const gerString: FunctionType = (name) => {  
  return name  
}
```

**Типизация класса**
```ts
class User {  
  name: string  
  age: number  
  
  constructor(name: string, age:number) {  
    this.name = name  
    this.age = age  
  }  
  
  getInfo(): string {  
    return `${this.name} - ${this.age}`  
  }  
}
```
`private` - защищено от всех  
`protected` - защита он всех но доступен у наследующих классах  
`public` - публичный  
`readonly` - только для чтения, нельзя редактировать

```ts
type TypeBrand = 'bmw' | 'mclaren' | 'mercedes'  
type TypePrice = '$100000' | '$400000' | '$50000'  
  
type TypeCar = `${TypeBrand} ${TypePrice}`
```

---

## Interface
```ts
interface UserInterface {  
  age: number,  
  name: string  
}
```

Может наследоваться от другого интерфейса
```ts
interface PersonInterface extends UserInterface {  
  age: number  
}
```

---
## enum
Тип `enum` или перечисление позволяет определить набор именованных констант, которые описывают определенные состояния.
Для определения перечисления применяется ключевое слово enum.
```ts
const enum TaskStatuses {  
    New,  
    InPProgress,  
    Completed,  
    Draft3  
}
// TaskStatuses.New -> 0

enum Season {  
    Winter = 'Зима',  
    Spring = 'Весна',  
    Summer = 'Лето',  
    Autumn = 'Осень'  
}
// Season.Autumn -> 'Осень'
```

---

## Generic
С помощью дженерика можно прокладывать типы и интерфейсы
```ts
interface Interface<K, V> {  
  key: K  
  value: V  
}

type Type<K, V> = {  
  key: K  
  value: V  
}

const props: Type<number, string> = {  
  key: 1,  
  value: 'qwe'  
}
```

Их можно использовать как в **функциях** так и в **классах**

```ts
function entity<T>(args: T): T {  
  return args  
}  

const entity2 = <T>(args: T):T => {  
  return args  
}

entity<number>(1)  
entity<string>('name')
```
 
```ts
class Entity<T> {  
  private name: T  
  constructor(name: T) {  
    this.name = name  
  }  
  getName():T {  
    return this.name  
  }  
}  
  
new Entity<number>(1)  
new Entity<string>('name')
```

```ts
type TypeIsNumber<T> = T extends number ? 'yes' : 'no'  
  
type Type1 = TypeIsNumber<number>  // -> 'yes'
type Type2 = TypeIsNumber<string>  // -> 'no'
```

---

## Утилиты_типов
Omit - в новом типе не добавлять указанные поля
Pick - в новом типе будут поля которые указал
Partial - делает все свойства не обязательными
Required - делает все поля обязательными
Readonly - делает все поля доступными только для чтения

```ts
interface User {  
  id: number  
  name: string  
  age: number  
}  
  
interface Element1 extends Omit<User, 'id'> {}
interface Element2 extends Pick<User, 'id'> {}
interface Element3 extends Partial<User> {}
interface Element4 extends Required<User>  {}
interface Element5 extends Readonly<User> {}
```


---

## Декораторы
```ts
function LogClass(constructor: Function) {  
  console.log(constructor.name)  
}  
  
function LogMethod(target: Object, key: string, descriptor: PropertyDescriptor) {  
  console.log(key)  
}  
  
@LogClass  
class Plane {  
  private id: number  
  
  constructor(id: number) {  
    this.id = id  
  }  
  
  @LogMethod  
  getId() {  
    return this.id  
  }  
}
```


---

## tsconfig.json
Файл в котором заложены настройки типизации
```json
{  
  "compilerOptions": {  
    "target": "es5",  // Версия экмаскрипт
    "lib": ["dom", "dom.iterable", "esnext"],  
    "allowJs": true,  
    "skipLibCheck": true,  
    "strict": true,  // Режим усилиной проверки на типы
    "forceConsistentCasingInFileNames": true,  
    "noEmit": true,  
    "esModuleInterop": true,  
    "module": "esnext",  // Виды импортов
    "moduleResolution": "bundler",  
    "resolveJsonModule": true,  
    "isolatedModules": true,  
    "jsx": "preserve",  
    "incremental": true,  
    "paths": {  
      "@/*": ["./src/*"]  
    }  },  
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],  
  "exclude": ["node_modules"]  
}
```

__
### Links
