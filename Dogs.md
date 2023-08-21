## Метод get_dogs_
 
Метод, котрый получает список всех собак.
 
### Общее описание 
 
* Архитектура: REST 
* Тип метода: GET 
* URL: v1/get_dogs
* Протокол взаимодействия: HTTPS 
* Формат входных данных: QUERY PARAMS
* Формат выходных данных: JSON 
* Тип вызова: Синхронный 
 
### Описание алгоритма 
 
 <image src="/Lightshot/Picture1.png" alt="Picture1">

mermaid 
{{< mermaid >}} 
sequenceDiagram 
    
    autonumber
    actor User
    participant Frontend
    participant Backend
    participant DataBase
    User ->> Frontend: Пользователь выбирает владельца
    Frontend ->> Backend: GET /get_dogs
    Backend ->> DataBase: SELECT
    DataBase -->> Backend: Response JSON
    Backend -->> Frontend: Response JSON
    Frontend -->> User: Отображает данные
    
{{< /mermaid >}} 
 
 
1. Пользователь выбирает флаг на необходимость на необходимость получения списка собак без владельца
2. При загрзуке страницы списка собак вызывается метод get_dogs
3. Backend обращается в DataBase
4. Database возвращает ответ в JSON
5. Backend возвращает ответ в JSON
6. Frontend отображает информацию в интерфейсе


### Входные данные 
| Параметр          | Обязательное поле | Тип данных | Описание                                                                   | 
| ----------------- | ----------------- | ---------- | -------------------------------------------------------------------------- | 
| without_owner     |                   | boolean    | Флаг, указывающий на необходимость получения списка собак без владельца    |

### Выходные данные 
| Параметр          | Обязательное поле | Тип данных | Описание                                                                   | 
| ----------------- | ----------------- | ---------- | ---------------------------------------------------------------------------|
| dogs              |                   |            |                                                                            | 
| [                 |                   |            |                                                                            |
| pet_id            | Y                 | integer    | ID питомца                                                                 |
| name              | Y                 | varchar    | имя питомца                                                                |
| breed             | Y                 | varchar    | порода                                                                     |
| age               |                   | integer    | возраст                                                                    |
| owner_id          |                   | integer    | ID владельца                                                               |
| ]                 |                   |            |                                                                            |


```json 
{ 
  "dogs":[
    {
      "pet_id": 321,
      "name": "example",
      "breed": "example",
      "age": 3,
      "owner_id": 123
    }
  ]
{ 

  
``` 