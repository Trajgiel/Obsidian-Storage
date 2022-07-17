2022-07-11 11:12
Tags: #React 
__
# React.memo (hoc)
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

# React.memo
React. memo — это компонент высшего порядка (hoc). Не запускает перерисовку компоненты, если props которые приходят в неё, не изменились. 
```jsx
const UsersSecret = (props: {users: Array<string>}) => {  
    console.log('Users')  
    return <div>{props.users.map((el, i) => <div key={i}>{el}</div>)}</div>  
}

const Users = React.memo(UsersSecret)
```

При оборачивании компонента с помощью `React.memo` React будет использовать последнюю отрисованную версию этого компонента. Мемоизация используется в приложениях React для повышения производительности.

_Мемоизация — это метод_ оптимизации, используемый в основном для ускорения компьютерных программ _путем хранения результатов дорогостоящих_ вызовов функций и возврата кэшированного результата вычислений при повторном использовании тех же входных данных.
__
### Links
[[React]]