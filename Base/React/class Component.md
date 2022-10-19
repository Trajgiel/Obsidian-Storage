2022-06-04 23:51
Tags: #React
__
# class React.Component
React позволяет определять компоненты как классы или функции. В настоящее время классовые компоненты имеют больше возможностей. Они разобраны на этой странице. Чтобы определить такой компонент, необходимо отнаследоваться от `React.Component`:

```jsx
class Component extends React.Component {
	render() {  
	    return (
			<h1>Привет, {this.props.name}</h1>;
		)
	}
}

```

Единственный _обязательный_ метод в подклассе `React.Component` — [`render()`](https://ru.reactjs.org/docs/react-component.html#render).

---
### Методы жизненого цикла:

- componentDidUpdate(prevProps, prevState) {...} - при обновлении компоненты выполняет код внутки этого метода.
	`prevProps`, `prevState` - это предыдущие значания которые были до момента перерисовки компоненты.
- shouldComponentUpdate(nextProps, nextState) {return boolean} - сравнивает если текущие пропсы или стейт не изменились, не перерисовывает компоненту.

__
### Links
[[Компонента]]