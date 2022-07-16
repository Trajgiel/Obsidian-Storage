2022-07-16 15:21
Tags: #Redux 
__
# action
action - это объект у которого обязательно есть свойство `type`

```tsx
{
	type: 'REMOVE-TASK',
	payload: {
		id: 01
		name: 'Vova'
		country: 'Belarus'
	}
}
```
Экшены обязательно должны иметь поле `type`, которое указывает на тип исполняемого экшена. Типы должны быть, как правило, заданы, как строковые константы.

# Action Creators

Action Creators - это функция которая возвращает action

```tsx
const addTaskAC = (id: number, name: string, country: string) => {
	return {
		type: 'REMOVE-TASK',
		payload: {
			id: 01
			name: 'Vova'
			country: 'Belarus'
		}
	}
}
```
__
### Links
[[reducer]]