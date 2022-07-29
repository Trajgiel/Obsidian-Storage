2022-07-30 00:18
Tags: #Redux #hook 
__
# useSelector
```tsx
const tasks = useSelector<StoreType, TasksStateType>(state => state.tasks)
```
`StoreType` - тип всего стора
`TasksStateType` - тип ветки которую мы возвращаем

useSelector - маппинг значения из store.  
Раньше:
```tsx
const Foo = ({ value }) => {
	return (
		<Bar value={value} />
	);
};

const mapStateToProps = state => ({
	value: state.value,
});

export default connect(mapStateToProps)(Foo);
```
Сейчас:
```tsx
const Foo = () => {
	const value = useSelector(state => state.value);
	
	return (
		<Bar value={value} />
	);
};

export default Foo;
```


__
### Links
[[hook (Хуки)]]