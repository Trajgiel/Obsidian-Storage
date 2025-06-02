2025-06-01 16:33
Tags: #webComponents

Это набор стандартов веб-технологий, позволяющих создавать переиспользуемые HTML-элементы с инкапсулированным поведением и стилями. Это **нативная технология** , не зависящая от фреймворков, что делает компоненты пригодными к использованию в любом проекте на HTML/JS/CSS.

`npm create vite@latest my-lit-app --template lit-ts` установка с Vite и TS
##### Основные части Web Components:
1. [Custom Elements](#Custom%20Elements)
2. [Shadow DOM](#Shadow%20DOM)
3. [HTML Templates](#HTML%20Templates)

---
### Custom Elements

Это пользовательские HTML-теги, определённые разработчиком. Браузер может их зарегистрировать и использовать как обычные элементы.

```ts
const template = document.createElement('template');
template.innerHTML = `
<style>  
  .user-card {...}  
  .user-card img {...}  
  .user-card button {...}  
</style>

<div class="user-card">  
   <img />  
   <div>    <h3></h3>  
    <div class="info">  
     <p>EMAIL</p>  
     <p>PHONE</p>  
    </div>  
    <button id="toggle-info">Hide Info</button>  
   </div>  
  </div>  
`

class UserCard extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: 'open' }); // вызов теневого дерева
    this.shadowRoot.appendChild(template.content.cloneNode(true));
    
    // добавлеиние атрибутов
	this.shadowRoot.querySelector('img').src = this.getAttribute('avatar')
  }

  connectedCallback(){  
	  // вызывается когда компонент добавился в DOM
	  this.shadowRoot.querySelector('#toggle-info').addEventListener('click', ()=> this.toggleInfo())
  }

  disconnectedCollBack(){
	  // вызывается при удалении компонента из DOM
	  this.shadowRoot.querySelector('#toggle-info').removeEventListener()
  }

  attributeChangedCallback(attrName, oldValue, newValue){
	  // вызывается когда атрибут добавляется/изменяется/удаляется
  }
}

customElements.define('user-card', UserCard);
```

```html
<user-card
	name="Jone Doe"
	avatar="https://randomuser.me/api/portraits/men/1.jpg"
>

</user-card>
```

---

### Shadow DOM

Технология, которая позволяет изолировать DOM и CSS внутри элемента. Это помогает избежать конфликтов стилей и случайного изменения внутренней структуры.

```ts
const shadow = this.attachShadow({ mode: 'open' });
shadow.innerHTML = `
  <style> p { color: red; } </style>
  <p>Текст внутри Shadow DOM</p>
`;
```

---

### HTML Templates

`<template>` — позволяет хранить HTML-разметку, которая не отображается напрямую, но может быть клонирована и добавлена в DOM.
`<slot>` — используется для проекции контента внутрь кастомного элемента.

```html
<template id="myTemplate">
  <p><slot>Значение по умолчанию</slot></p>
</template>
```

---
### Links
