2022-07-23 17:18
Tags: #JavaScript #class 
__
# class
Для чего нужны классы:
1. Создание однотипных объектов на базе этих классовю.
2. ООП принципы:
	- инкапсуляция (сокрытие деталей)
	- наследование (extends)
	- полиморфизм
---
- super - вызов родительского сонструктора у наследуемого класса.
- this - объект созданный с помощью класса.
- constructor() - (конструирование объекта) - это метод который вызывается во время `new`. 
- render() - метод, возвращает нужные данные
---
Методы жизненого цикла (React):
- componentDidMount() - запускается однин раз при первой отрисовке
- componentDidUpdate() - изменение компоненты
---
```js
class Man {
	constructor(name, age) {       //constructor принимает параметры
		this.name = name;
		this.age = age;
	}
	hello() {                      //метод класса
		console.log(`I am ${this.name}`) 
	}
	render() {                     //метод render
		return (
			{this.name} {this.age}
		)
	}
}
const man1 = new Man('Vova', 28); //создаёт новый объект из заданного ранее класса
const renMam1 = man1.render(); //метод render возвращает нужные данные
```
---
### extends (наследование)
Ключевое слово `extends` работает, используя прототипы. Оно устанавливает `Rabbit.prototype.[[Prototype]]` в `Animal.prototype`. Так что если метод не найден в `Rabbit.prototype`, JavaScript берёт его из `Animal.prototype`.
```js
class Man {
	constructor(name, age) {
		this.name = name;
		this.age = age;
		this.speed = 0;
	}
	run(speed) {
		this.speed = speed;
	}
}

// Наследуем от Man указывая "extends User"
class User extends Man {
	stop() {
		this.speed = 0
		alert(`${this.name} стой!`);
	}
}

let vova = new User("Vova", 28);

vova.run(5); // Вова бежит со скоростью 5.
vova.stop(); // Вова стой!
```
---
## super()
super - вызов родительского сонструктора у наследуемого класса.
```js
class User extends Man {
	constructor(name, age, tech) {
		super(name, age)
		this.tech = tech
	}
	run(speed) {             //меняем наследуемый метод
		super.run(speed)
		console.log('Go')
	}
}
```
Наследуемый класс наследует и constructor, но если мы его пропишим то сонструктор будет свой. Но блягодоря super мы обратимся родительскому классу и заберем параметры которые есть у него.

---
## Приватные свойства и методы
`#` - приватные свойства и методы должны начинаться с `#`. (`private`)
Они доступны только внутри класса.
```js
class Man {
	name = 'Vladimir';
	#age = 28;
}

const user = new Man()
user.name // 'Vladimir'
user.#age // Error
```
---
## GET/SET          (инкапсуляция)
```js
class User {
	#name = 'Vladimir'
    #age = 23  
    get name() {          // ролучение данных через метод
        return this.#name  
    }  
    set age(value) {      //позволяет изменять значение метода
        this.#age = value  
    }  
}

const man = new User()
console.log(man.name) // get
man.age = 28; // set
```
---
`private` - защищено от всех
`protected` - защита он всех но доступен у наследующих классах
`public` - публичный
`readonly` - только для чтения, нельзя редактировать

---


__
### Links
[[JavaScript]]