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
  initial={{   // Изночальное значение
	x: -1000,
  }}
  animate={{   // Изменения на момент анимации
	x: 0,
  }}
  transition={{
	duration: 2,
	repeat: 'Infinity'
  }}
  whileHover={{   // Изменеия на ховер эфект
	scale: 1.3,
	color: 'red'
  }}
/>
```

**AnimatePresence** - для анимации при появлении в дом дереве и при удалении от туда

---

```

Пример с вариантами анимации
```tsx
const pVariants = {
	hidden: {
		x: -1000,
		opacity: 0
	}
	visible: {
		x: 0,
		opacity: 1
	}
}

<motion.div  
  className="styles"
  initial={'hidden'} // Изночальное значение
  animate={'visible'} // Изменения на момент анимации
  transition={{
	duration: 2,
	repeat: 'Infinity'
  }}
  variants={{pVariants}}
/>
```

Отрисовка массива с анимацией
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