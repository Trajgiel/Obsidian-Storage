2025-04-12 15:17
Tags: #Interview #CSS

Правило в CSS (Cascading Style Sheets) — это базовая единица стилизации, которая определяет, как элементы HTML должны быть отображены в браузере. Каждое правило состоит из трех основных частей: **селектора** , **блока объявления** и **самого объявления**.

Правило CSS состоит из селектора и блока объявления:
```css
селектор {
  свойство: значение;
}
```

- [Селекторы](#Селекторы)
- [Селекторы атрибутов](#Селекторы%20атрибутов)
- [Специфичность](#Специфичность)
- [Переменные](#Переменные)
- [calc()](#calc())
- [CSS Hack](#CSS%20Hack)
- [Media](#Media)
- [BEM](#BEM)
- [Mobile First](#Mobile%20First)
- [Настройки для шрифтов](#Настройки%20для%20шрифтов)
- [Свойства display](#Свойства%20display)
- [Псевдокласы](#Псевдокласы)
- [Как центрировать блок](#Как%20центрировать%20блок)
- [Z-index](#Z-index)
- [Восстановить значение свойства по умолчанию](#Восстановить%20значение%20свойства%20по%20умолчанию)
- [Прекрасная деградация](#Прекрасная%20деградация)
- [Прогрессивное улучшение](#Прогрессивное%20улучшение)
- [Каковы ограничения CSS](#Каковы%20ограничения%20CSS)

---
### Селекторы

Определяют, к каким элементам HTML применяются стили.
- Типовые селекторы: `h1`; `p`; `div`
- Классы: `.class-name`
- ID: `#id-name`
- Универсальный селектор: `*`
- Составные селекторы: `div p`; `div > p`; `div + p`; `div ~ p`; `div, p`

---
### Селекторы атрибутов

Позволяют выбирать элементы на основе их атрибутов и значений этих атрибутов.
- `a[href]` - все элементы `<a>`, у которых есть атрибут "href"
- `input[type="submit"]` - все элементы `<input>`, где type="submit"
- `a[href*="example.com"]` - все ссылки, где href содержит "example.com"
- `a[href^="https://"]` - все ссылки, где href начинается с "https://"
- `a[href$=".pdf"]` - все ссылки, где href заканчивается на ".pdf"
- `div[class~="active"]` - все элементы `<div>`, где class содержит "active"
- `p[lang|="en"]` - все элементы `<p>`, где lang начинается с "en"

---
### Специфичность

Механизм определения какие CSS-правила будут применяться к элементу, если несколько правил конфликтуют между собой. Это своего рода "приоритет", который присваивается каждому CSS-правилу.
1. Inline-стили: `style="..."`
2. ID-селекторы: `#header { color: blue; }`
3. Классы, псевдоклассы и атрибуты: `.my-class`, `:hover`, `[type="text"]`
4. Элементы и псевдоэлементы: `div`, `::before`
5. Универсальный селектор (`*`) и комбинаторы: `*`, `>`, `+`, `~`

`!important` переопределяет все остальные правила

---
### Переменные

Позволяют определять переиспользуемые значения для различных свойств CSS

```css
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --padding-default: 16px;
}

body {
  background-color: var(--primary-color);
  color: white;
  padding: var(--padding-default);
}

button {
  background-color: var(--secondary-color);
  border: none;
  padding: var(--padding-default);
  color: white;
}
```

Функция `var()` позволяет указать значение по умолчанию, если переменная не определена:
```css
p {
  color: var(--text-color, black);
}
```

Переменные могут быть локальными или глобальными:

- **Глобальные переменные** объявляются в `:root` и доступны во всем документе.
- **Локальные переменные** объявляются внутри конкретного селектора и доступны только в его контексте.
```css
:root {
  --global-color: blue;
}

.container {
  --local-color: red;
  color: var(--local-color); /* Красный */
  background-color: var(--global-color); /* Синий */
}

.text {
  color: var(--global-color); /* Синий */
  /* --local-color здесь недоступна */
}
```

---
###  calc()

Функция CSS, которая позволяет выполнять математические операции на основе различных единиц измерения.
```css
width: calc(100% - 20px);
```

---
### CSS Hack

Техника используемая для написания специфичных правил CSS, которые будут применяться только в определенных браузерах или версиях браузеров.

```css
.example {
    -webkit-border-radius: 5px; /* Для Safari и старых Chrome */
    -moz-border-radius: 5px;    /* Для Firefox */
    border-radius: 5px;         /* Стандарт */
}
```

---
### Media

Инструмент, который позволяет применять стили в зависимости от характеристик устройства (ширина экрана, высота, ориентация и т.д.)

```css
@media media-type and (condition: breakpoint) {
  /* CSS rules */
}
```

Пример
```css
@media (max-width: 768px) {
  body {
    font-size: 14px;
  }
}
```

---

### BEM

(Block Element Modifier) - это методология именования классов для CSS.
Она помогает создавать переиспользуемые и независимые компоненты.

**Block (Блок)** - независимый, самодостаточный компонент, который может быть переиспользован в разных частях приложения.
Например, кнопка, карточка, меню.

**Element (Элемент)** - часть блока, которая не имеет смысла вне контекста блока.
Например, текст внутри кнопки или иконка внутри карточки.

**Modifier (Модификатор)** - флаг или свойство, которое изменяет внешний вид или поведение блока или элемента.
Например, активная кнопка, отключенная карточка.

```css
block-name__element-name--modifier-name
```

**block-name** : Имя блока
(например, `button`, `card`).

**element-name** : Имя элемента внутри блока
(например, `button__text`, `card__title`).

**modifier-name** : Имя модификатора
(например, `button--disabled`, `card--active`).

---

### Mobile First

Это подход, при котором стили сначала пишутся для мобильных устройств, а затем адаптируются для больших экранов с помощью медиа-запросов.

---

### Настройки для шрифтов

- `font-family`: семейство шрифтов
- `font-size`: размер шрифта
- `font-weight`: толщина шрифта
- `line-height`: межстрочный интервал
- `letter-spacing`: расстояние между буквами


### Свойства display

- `block`: блочный элемент
- `inline`: строчный элемент
- `inline-block`: строчно-блочный элемент
- `flex`: флексбокс контейнер
- `grid`: грид-контейнер
- `none`: элемент скрыт

---
### Псевдокласы

Ключевые слова, которые добавляются к селекторам для определения специфического состояния элемента.

1. Псевдоклассы состояния элемента
	- `:hover`, `:active`, `:focus`
2. Псевдоклассы положения элемента
	- `:first-child` — выбирает первый дочерний элемент внутри родителя
	- `:last-child` — выбирает последний дочерний элемент
	- `:nth-child(n)` — выбирает элемент по его порядковому номеру
	- `:only-child` — если он единственный потомок своего родителя
3. Псевдоклассы для форм и ввода
	- `:checked` — применяется к отмеченным чекбоксам или радиокнопкам
	- `:disabled` — применяется к отключенным элементам формы
	- `:valid` и `:invalid` — применяются к элементам формы в зависимости от валидности введенных данных
4. Псевдоклассы для работы с ссылками
	- `:link` — применяется к не посещенным ссылкам
	- `:visited` — применяется к посещенным ссылкам
5. Псевдоклассы для анимаций и переходов
	- `:target` — применяется к элементу, который является целью URL-хэша
	- `:empty` — применяется к элементам, которые не содержат дочерних элементов или текста.
6. Современные псевдоклассы
	- `is()` — позволяет группировать селекторы
	- `:where()` — аналогичен `:is()`, но имеет нулевую специфичность.

---

### Как центрировать блок

1. Flexbox
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

2. Grid
```CSS
.container {
  display: grid;
  place-items: center;
}
```

3. Абсолютное позиционирование
```CSS
.block {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

4. Margin: auto
```CSS
margin: 20px auto;
```

---

### Z-index

CSS-свойство, которое определяет порядок наложения элементов на веб-странице. Оно используется для управления тем, какой элемент будет находиться "поверх" других, когда они перекрываются

Работает только с позиционированными элементами (`position: relative/absolute/fixed`).

---

### Восстановить значение свойства по умолчанию

CSS существует возможность восстановить значение свойства по умолчанию. Для этого используется ключевое слово `initial`

```css
button {
  background-color: initial;
}
```

---
### Прекрасная деградация

Подход к разработке, при котором веб-приложение или сайт создаются сначала для современных браузеров с использованием всех доступных технологий и возможностей. Затем добавляется поддержка старых браузеров, чтобы обеспечить базовую функциональность.

---

### Прогрессивное улучшение

Подход, при котором сайт сначала разрабатывается для базовой функциональности, а затем добавляются улучшения для современных браузеров.

---

### Каковы ограничения CSS

1. **Восхождение по селекторам невозможно** - CSS работает только "вниз" по DOM-дереву: вы можете стилизовать дочерние элементы на основе родительских, но не наоборот.
2. **Ограничения вертикального контроля** - ограниченные возможности для управления вертикальным позиционированием элементов.
3. **Нет выражений** - нельзя использовать выражения или логические операции.
4. **Нет объявления столбца** - не предоставляет прямых средств для создания сложных таблиц или колонок без использования дополнительных свойств.
5. **Псевдокласс, не управляемый динамическим поведением** - вы не можете создать собственный псевдокласс, поведение зависит от событий, которые уже предусмотрены в CSS.
6. **Правила, стили, таргетинг на конкретный текст невозможны** - не позволяет стилизовать текст на основе его содержимого.

---
### Links
[[Interview]]