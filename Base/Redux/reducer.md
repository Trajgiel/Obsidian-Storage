2022-07-11 12:16
Tags: #Redux 
__
# reducer
reducer - это чистая функция которая принимает state, принимает action, и если нужно применяет этот action к этаму state и возврвщает новый state или возвращает не изменёный state

```jsx
function reducer(state, action) {
	switch (action.type) {
		case 'increment':
		    return {count: state.count + 1};
	    case 'decrement':
			return {count: state.count - 1};
	    default:
		    throw new Error();
	}
}
```
__
### Links
[[Redux]]
