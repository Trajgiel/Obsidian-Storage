2022-07-30 00:07
Tags: #Redux #hook
__
# useDispatch
```tsx
const dispatch =  useDispatch()

dispatch(action)
```
useDispatch - получение функции store.dispatch в компоненте. Раньше для вызова action функциональный компонент приходилось оборачивать в вызов connect:
```tsx
const Foo = ({ dispatch }) => {
	const handler = useCallback(() => {
		dispatch(action());
	}, []);
	
	return (
		<Bar onClick={handler} />
	);
};

export default connect()(Foo);
```
Сейчас:
```tsx
const Foo = () => {
	const dispatch = useDispatch();
	
	const handler = useCallback(() => {
		dispatch(action());
	}, []);
	
	return (
		<Bar onClick={handler} />
	);
};

export default Foo;
```
__
### Links
[[hook (Хуки)]]