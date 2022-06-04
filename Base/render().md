2022-06-04 23:59
Tags: #
__
# render()
```
ReactDOM.render(element, container[, callback])
```

Рендерит React-элемент в DOM-элемент, переданный в аргумент `container` и возвращает [ссылку](https://ru.reactjs.org/docs/more-about-refs.html) на компонент (или возвращает `null` для [компонентов без состояния](https://ru.reactjs.org/docs/components-and-props.html#function-and-class-components)).

Если React-элемент уже был ранее отрендерен в `container`, то повторный вызов произведёт его обновление и изменит соответствующую часть DOM, чтобы она содержала последние изменения.

Если дополнительно был предоставлен колбэк, он будет вызван после того, как компонент отрендерится или обновится.
__
### Links
