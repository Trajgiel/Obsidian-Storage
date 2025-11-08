2025-03-28 11:32
Tags: #workerThreads

Это встроенный модуль Node.js (`worker_threads`), который позволяет запускать параллельные потоки (потоки воркеры) для выполнения кода в отдельных потоках, но в одном и томже процессе.

Позволяют выполнять задачи в отдельных потоках, не мешая основному потоку.

---

### Основные моменты:

1. Каждый worker запускается в отдельном потоке.
2. У каждого worker свой event loop, свой V8 и свой memory heap.
3. Основной поток и worker общаются через **message passing** (через события и сериализуемые данные).
4. Можно создать сколько угодно worker'ов (ограничено ресурсами системы).

![[workerThreads1.png]]

Минимальный пример использования:

``` js
// main.js
const { Worker } = require('worker_threads');

const worker = new Worker('./worker.js');

worker.postMessage('Привет из main');

worker.on('message', (msg) => {
    console.log('Сообщение от worker:', msg);
});

// worker.js
const { parentPort } = require('worker_threads');

parentPort.on('message', (msg) => {
    console.log('Сообщение от main:', msg);
    parentPort.postMessage('Привет из worker');
});
```

---

### Когда использовать?

- Долгие вычисления
- Парсинг и обработка больших данных
- Генерация PDF, изображений
- Сжатие файлов
- Все задачи, которые грузят процессор, а не дисковую подсистему или сеть

---
### Links
[[Base/JavaScript/Node.js/Node.js]]
