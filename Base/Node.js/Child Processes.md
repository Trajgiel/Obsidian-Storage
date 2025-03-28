2025-03-28 15:15
Tags: #childProcesses

Это механизм в Node.js, который позволяет создавать и запускать отдельные процессы (например, другие программы, скрипты или даже другие Node.js процессы) параллельно с основным (родительским) процессом.

Node.js работает в однопоточном режиме, но с помощью `child_process` можно запускать параллельные процессы и таким образом обрабатывать задачи вне основного event loop.

---

### Основные методы модуля `child_process`

```js
const { exec, execFile, spawn, fork } = require('child_process');
```

|Метод|Когда использовать|
|---|---|
|`exec()`|Запуск команды в shell, возвращает stdout/stderr целиком|
|`execFile()`|Запуск исполняемого файла без shell|
|`spawn()`|Более низкоуровневый, для потоков данных|
|`fork()`|Специально для запуска других Node.js скриптов и общения через IPC|

![[childProcess1.png]]

---

### Примеры:

exec
```js
const { exec } = require('child_process');

exec('ls -la', (error, stdout, stderr) => {
    if (error) {
        console.error(`Ошибка: ${error.message}`);
        return;
    }
    console.log(`Результат:\n${stdout}`);
});
```

spawn
```js
const { spawn } = require('child_process');

const ls = spawn('ls', ['-la']);

ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
});
```

fork
```js
const { fork } = require('child_process');

const child = fork('child.js'); // child.js — другой Node.js файл

child.on('message', (msg) => {
    console.log('Сообщение от дочернего процесса:', msg);
});

child.send({ hello: 'world' });
```


---

### Зачем нужны `Child Processes`?

- Выполнять тяжёлые вычисления без блокировки event loop
- Запускать сторонние утилиты (например, `ffmpeg`, `git`, `curl`, и т.п.)
- Делать масштабируемые приложения (например, через `Cluster`)
- Делить задачи между процессами (подходит для CPU-bound задач)

---
### Links
[[Node.js]]
[Все, что вам нужно знать о «child_process» в Node.js](https://www.youtube.com/watch?v=C1v4MXGhpcM)