2022-07-23 19:06
Tags: #React 
__
# hoc
### High Order Component
hoc (High Order Component) - компонента высшего порядка.
Это функция которая на входе принимает одну компоненту, а возвращает другую компоненту.

Задача hoc создавать контейнерную компоненту(ы)
```jsx
let hoc = (Component) => {
	let WrapperContainer = (props) => {
		return <Component bla='yo'/>
	}
	return WrapperContainer;
}
```

- [[React.memo]] - не запускает перерисовку компоненты, если props...

__
### Links
[[React]]