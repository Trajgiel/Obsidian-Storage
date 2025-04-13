2025-02-23 16:21
Tags: #WebWorker

Это механизм, позволяющий выполнять [[Base/JavaScript/JavaScript]] в фоновом потоке, отделенном от основного потока веб-приложения. Это важно, поскольку позволяет выполнять ресурсоемкие вычисления без блокировки пользовательского интерфейса (UI), что улучшает отзывчивость приложения

---

index.js
```js index
if (window.Worker) {
	const myWorker = new Worker("./worker.js", {type: "module"})
	myWorker.postMessage(e) // предаём данные в Worker
	myWorker.onmessage = (e) => {
		console.log(e.data) // получаем данные из Worker
	}
} else {
	// При отсутствии воркера выполняется логита тут
}
```

worker.js
```js worker
self.onmessage = (e) => {
	const data = e.data // Данные которые принимает Worker
	...
	const result = ...
	self.postMessage(result) // Данные которые возвращает Worker
}
```

---

### Ограничения Web Workers

- **Нет доступа к DOM:** Worker не может напрямую взаимодействовать с элементами страницы.
- **Копирование данных:** Когда данные передаются между основным потоком и Worker, они копируются, а не передаются по ссылке. Это может быть затратно для больших объемов данных.
- **Использование Transferable Objects:** Для улучшения производительности можно использовать `Transferable Objects` (например, массивы `ArrayBuffer`), которые передаются без копирования.

---
### Links
[[Base/JavaScript/JavaScript]]
