## Метод get_dogs_by_owner
 
Метод, который будет возвращать список питомцев владельца.
 
### Общее описание 
 
* Архитектура: REST 
* Тип метода: GET 
* URL: v1/get_dogs_by_owner
* Протокол взаимодействия: HTTPS 
* Формат входных данных: QUERY PARAMS
* Формат выходных данных: JSON 
* Тип вызова: Синхронный 
 
### Описание алгоритма 
 
 <img src="/Lightshot/Picture1.png" border="5px solid red"/>
 ![Текст с описанием картинки](/Lightshot/Picture1.png)

mermaid 
{{< mermaid >}} 
sequenceDiagram 
    
    autonumber
    actor User
    participant Frontend
    participant Backend
    participant DataBase
    User ->> Frontend: Пользователь выбирает владельца
    Frontend ->> Backend: GET /get_dogs_by_owner
    Backend ->> DataBase: SELECT
    DataBase -->> Backend: Response JSON
    Backend -->> Frontend: Response JSON
    Frontend -->> User: Отображает данные
    
{{< /mermaid >}} 
 
 
1. Пользователь выбирает владельца
2. При загрзуке страницы владельца собаки вызывается метод get_dogs_by_owner
3. Backend обращается в DataBase
4. Database возвращает ответ в JSON
5. Backend возвращает ответ в JSON
6. Frontend отображает информацию в интерфейсе


### Входные данные 
| Параметр                       | Обязательное поле | Тип данных | Описание        | 
| ------------------------------ | ----------------- | ---------- | --------------- | 
| owner_id                       | Y                 | integer    | ID владельца    |

### Выходные данные 
| Параметр                       | Обязательное поле | Тип данных | Описание        | 
| ------------------------------ | ----------------- | ---------- | --------------- |
| owner_id                       | Y                 | integer    | ID владельца    |
| dogs                           |                   |            |                 | 
| [                              |                   |            |                 | 
| pet_id                         | Y                 | integer    | ID питомца      |
| name                           | Y                 | varchar    | имя питомца     |
| breed                          | Y                 | varchar    | порода          |
| age                            | Y                 | integer    | возраст         |
| ]                              |                   |            |                 | 


```json 
{ 
  "owner_id": 123,
  "dogs":[
    {
      "pet_id": 321,
      "name": "example",
      "breed": "example",
      "age": "3"
    }
  ]
{ 

  
``` 