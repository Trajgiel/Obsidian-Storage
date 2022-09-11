2022-08-20 20:18
Tags: #axios
__
# Axios
Установить axios библиотеку - `yarn add axios`

Схема взаимодействия с сервером (REST API)
![[api.png]]
**API (Application Programming Interface)** - интерфейс взаимодействия с программным продуктом.  

**REST (RESTful)** - это общие принципы организации взаимодействия приложения/сайта с сервером посредством протокола HTTP. Особенность REST в том, что сервер не запоминает состояние пользователя между запросами - в каждом запросе передаётся информация, идентифицирующая пользователя (например, token, полученный через OAuth-авторизацию) и все параметры, необходимые для выполнения операции.  

**REST API характеризуется:**
1.   Адресом (base address) + endpoint
2.  Типом запроса (GET, POST, PUT (PATCH), DELETE, OPTION)
3.  Что отправляем на сервер (request payload)
4.  Что получаем с сервера (response data)
5.  Код ответа (состояния) HTTP показывает, был ли успешно выполнен определённый HTTP запрос. Коды сгруппированы в 5 классов:
-   1XX - информационные,
-   2XX - успешные,
-   3XX - перенаправления (редирект),
-   4XX - ошибки клиента
-   5XX - ошибки сервера

[Более подробно про коды ответа HTTP](https://developer.mozilla.org/ru/docs/Web/HTTP/Status)

---
Всё взаимодействие с сервером сводится к следующим операциям:
1.  `GET` - получение данных с сервера (обычно в формате JSON, или XML).  
    Операция получения данных не может приводить к изменению состояния сервера.
2.  `POST` - добавление новых данных на сервер.
3.  `PUT` - модификация существующих данных на сервере
4.  `DELETE` - удаление данных на сервере
5.  `OPTIONS` - preflight запрос. Проверяет можем ли мы с одного адреса делать запрос на другой

**Отличия запросов:**

-  У GET и DELETE запросов нету тела запроса (body, payload)
-  У POST и PUT(PATCH) есть тела запроса (body, payload)
-  Разница между PUT и PATCH в том, что PUT обновляет объект целиком, а PATCH — только указанное поле.
---
```ts
const instance = axios.create({  
    baseURL: 'https://social-network.samuraijs.com/api/1.1/',  
    withCredentials: true,  
    headers: {  
        'API-KEY': 'fe0bde16-910d-49bc-94ec-281d4e7919c5'  
    }  
})

export const todolistsAPI = {  
    getTodolists() {  
        return instance.get<TodolistType[]>('todo-lists');  
    },
    ...
    updateTask(todolistId: string, taskId: string, model: 
    UpdateTaskModelType) {  
	    return instance.put<UpdateTaskModelType, 
        AxiosResponse<ResponseType<{ item: TaskType }>>>(`todo- 
        lists/${todolistId}/tasks/${taskId}`, model);  
	}
}
```

__
### Links
[[React]]