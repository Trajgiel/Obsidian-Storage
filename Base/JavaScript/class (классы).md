2022-07-23 17:18
Tags: #JavaScript #class 
__
# class
Нужны для того что-бы создовать однотипные объекты на базе этих классов

- super -
- this - объект созданный с помощью класса

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

- [[new Date()]] - создаёт объект `Date` с текущей датой и временем...
- new Set() -
- new Map() -

__
### Links
[[JavaScript]]