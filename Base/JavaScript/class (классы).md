2022-07-23 17:18
Tags: #JavaScript #class 
__
# class
Нужны для того что-бы создовать однотипные объекты на базе этих классов
- super - вызов родительского сонструктора у наследуемого класса
- this - объект созданный с помощью класса
---
- constructor() - (конструирование объекта) - это метод который вызывается во время `new`. 
- componentDidMount() - запускается однин раз при первой отрисовке
- render() - метод, возвращает нужные данные

```js
class Man {
	constructor(name, age) {       //constructor принимает параметры
		this.name = name;
		this.age = age;
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
`#` - приватные свойства и методы должны начинаться с `#`. Они доступны только внутри класса.
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
### GET/SET
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
`protected` - защита он инстансов
`public` - публичный
`readonly` - только для чтения, нельзя редактировать

---
### extends
Ключевое слово `extends` работает, используя прототипы. Оно устанавливает `Rabbit.prototype.[[Prototype]]` в `Animal.prototype`. Так что если метод не найден в `Rabbit.prototype`, JavaScript берёт его из `Animal.prototype`.
```js
class Animal {
	constructor(name) {
		this.speed = 0;
		this.name = name;
	}
	
	run(speed) {
	this.speed = speed;
	alert(`${this.name} бежит со скоростью ${this.speed}.`);
	}
	
	stop() {
		this.speed = 0;
		alert(`${this.name} стоит.`);
	}
}

// Наследуем от Animal указывая "extends Animal"
class Rabbit extends Animal {
	hide() {
		alert(`${this.name} прячется!`);
	}
}

let rabbit = new Rabbit("Белый кролик");

rabbit.run(5); // Белый кролик бежит со скоростью 5.
rabbit.hide(); // Белый кролик прячется!
```


__
### Links
[[JavaScript]]