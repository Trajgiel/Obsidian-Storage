2022-08-14 14:45
Tags: #Storybook
__
# Snapshot testing
Бибилиотека для визуального тестирования компонент

Кратко идея такая:
-   Мы видим, что компонент работает и правильно отображается. Супер. Сделаем скриншот? Сделали…
-   В будущем система тестов будет делать новые скриншоты, и если что-то поломается и компонент начнёт выглядеть иначе - нам об этом тестовая среда скажет.

Почитать обязательно о [тестах в React](https://ru.reactjs.org/docs/testing-recipes.html)
К сожалению или к радости, мы имеем множество однотипных альтернатив, как тестировать. Но что радует: принципы одни и те же, отличия небольшие в синтаксисе.  
Мы будем использовать [storybook для этих целей](https://storybook.js.org/docs/testing/automated-visual-testing/)...

---
## Snapshot:
1) Добавляем в проект зависимости:

```tsx
yarn add puppeteer jest-puppeteer jest-image-snapshot start-server-and-test --dev
```
-   Запустите проект.. проверьте, что просто всё запускается и всё ок.
-   Запустите тесты.. проверьте, что так же всё запускается и ничего не сломалось

2) В package.json добавьте скрипты для запуска:
```tsx
"jest:integration": "jest -c integration/jest.config.js",
"test:integration": "start-server-and-test storybook http-get://localhost:9009 jest:integration"
```

3) Создайте папку integration (в рутовой папке проекта ,НЕ в src), и внутри два файла:
- setupTests.js с настройками для snapshot-testing:
```tsx
​const { toMatchImageSnapshot } = require('jest-image-snapshot');

expect.extend({ toMatchImageSnapshot });
```
- jest.config.js с настройками для jest:
```tsx
module.exports = {
   preset: 'jest-puppeteer',
   testRegex: './*\\.test\\.js$',
   setupFilesAfterEnv: ['./setupTests.js']
};
```
**Да, именно с расширением js, типизация нам здесь не нужна:**

---
## Snapshot tests:
1) Запустите сторибук и откройте [какую-нибудь историю](http://localhost:9009/?path=/story/todolist-additemform--add-item-form-example)
![[Storybook.png]]
Ссылки ваши могут отличаться. Но принцип один и тот же.
Открывайте вашу историю, а дальше замените в ней жирный текст:
http://localhost:9009/**?path=/docs/**todolist-appwithredux--base-example
на этот текст:
```
iframe.html?id=
```
```
http://localhost:9009/iframe.html?id=todolist-additemform--add-item-form-example
```
2) Давайте напишем наш первый snapshot-integration тест (в файле app.test.js, который положим в ту же папку integration):
```js
describe('addItemForm', () => {
    it('base example, visually looks correct', async () => {
        // APIs from jest-puppeteer
        await page.goto('http://localhost:9009/iframe.html?id=todolist-additemform- -add-item-form-example')
        const image = await page.screenshot()

        // API from jest-image-snapshot
        expect(image).toMatchImageSnapshot()
    })
})
```
3) Запускаем наш новый integration-тест:
```js
yarn test:integration
```
---
#### Мы можем обновить старые скрины новыми:
```js
yarn run jest:integration --updateSnapshot
```
__
### Links
[[Install React]]