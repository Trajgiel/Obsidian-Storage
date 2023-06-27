2023-06-12 22:43
Tags: #react 

---
 `yarn add framer-motion`   |   `npm i framer-motion`

[Framer Motion](https://www.framer.com/motion/) - библиотека анимации

Пример использования:
```tsx
import { motion } from 'framer-motion';

<motion.div  
  className="styles"
  initial={{ x: -1000 }} // Изночальное значение
  animate={{ x: 0 }} // Изменения на момент анимации
  transition={{ // Настройки анимации
	duration: 2,
	repeat: 'Infinity'
  }}
  whileHover={{ scale: 1.3 }} // Изменеия на hover эфект
  whileTop={{ bacgroundColor: '#000'}} // Изменение на событие active
/>
```

---

**AnimatePresence** - для анимации при появлении в дом дереве и при удалении от туда
```tsx
const [visibility, setVisibility] = useState(false);

<button onClick={() => { setVisibility(!visibility) }}> Кнопка </button>

<AnimatePresence
	initial={true} // Изночальное состояние приложения будет БЕЗ анимации
	exitBeforeEnter // Сперва исчезнут старые элементы и после появятся новые
>
	{visibility &&
		<motion.p
			initial={{ height: 0 }} // Изночальное значение
			animate={{ height: 'auto' }} // Изменения на момент анимации
			exit={{ height: 0 }} // Анимация на исчезновение из ДОМ дерева
			transition={{ duration: 0.5 }} // Настройки анимации
			styles={{verflow: 'hidden'}}
		>	
			Появляющийся текс
		</motion.p>
	}
</AnimatePresence>
```

---

**AnimateSharedLayout** - связывает между собой несколько элементов и объединяет их в общую анимацию. Должен присутствовать `layoutId` или `layout` с уникальным значением, библиотека поймёт что это общий элемент и будет его анимировать как один
```tsx
<AnimateSharedLayout>
	{items.map((el, index) => (
	<motion.li
		key={index}
		layoutId={'activeItem'} // Обязательно должен быть создан
		initial={{ height: 0 }} // Изночальное значение
		animate={{ height: 'auto' }} // Изменения на момент анимации
		transition={{ duration: 0.5 }} // Настройки анимации
	>
		{el}
	</motion.li>

	))
}
</AnimateSharedLayout>
```

---

### Пример с вариантами анимации
```tsx
const pVariants = {
	hidden: { x: -1000, opacity: 0 }
	visible: { x: 0, opacity: 1 }
}

<motion.div  
  className="styles"
  initial={'hidden'} // Изночальное значение
  animate={'visible'} // Изменения на момент анимации
  transition={{ duration: 2, repeat: 'Infinity' }} // Настройки анимации
  variants={{pVariants}}
/>
```

### Отрисовка массива с анимацией
```tsx
const items = ['item1', 'item2', 'item3']

const listVariants = {
	hidden: { opacity: 0 }
	visible: i => ({
		opacity: 1
		transition: {
			delay: i * 0.5
		}
	})
}

{items.map((el, index) => (
	<motion.li
		key={index}
		variants={{listVariants}}
		initial={'hidden'} // Изночальное значение
		animate={'visible'} // Изменения на момент анимации
		custom={index}   // Значение для функции
	>
		{el}
	</motion.li>

	))
}

```
__
### Links
[[Библиотеки]]