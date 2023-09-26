2023-09-25 18:14
Tags: #prettier

---

`npm i -D prettier`

В корне приложения создаём файл **.prettierrc**
``` json
{
"tabWidth": 2, // Длина таба 2, два пробела
"singleQuote": true, // Одинарные ковычки

"arrowParens": "avoid", // Стрелочная функция с одним элементов, скобок нету
"semi": true, // В конце точка с запятой
"trailingComma": "none", // Не ставить последнию запятую в объекте

"trailingComma": "es5",  
"printWidth": 120,  
"endOfLine": "auto"
}
```

---
### Links
