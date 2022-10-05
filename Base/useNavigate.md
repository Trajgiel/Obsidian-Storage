2022-10-05 21:55
Tags: #hook 
__
# useNavigate

Добавление данных в URL
```jsx
```javascript
import { createSearchParams, useNavigate } from "react-router-dom";

...

const navigate = useNavigate();

navigate({
    pathname: "profile",
    search: createSearchParams({
        name: 'Vova'
        page: '2',  
		pageCount: '25',  
    }).toString()
});

// ...URL/profile?name=Vova&page=2&pageCount=25
```

__
### Links
[[hook (Хуки)]]