## Метод get_dogs
 
Метод, который будет возвращать список питомцев, как для определенного владельца, так и общий список.
 
### Общее описание 
 
* Архитектура: REST 
* Тип метода: GET 
* URL: v1/get_dogs
* Протокол взаимодействия: HTTPS 
* Формат входных данных: QUERY PARAMS
* Формат выходных данных: JSON 
* Тип вызова: Синхронный 
 
### Описание алгоритма 
 
mermaid 
{{< mermaid >}} 
sequenceDiagram    
    autonumber
    actor User
    participant Frontend
    participant Backend
    participant DataBase
    User ->> Frontend: Переход на страницу
    Frontend ->> Backend: GET /get_dogs
    alt Во входных данных передан owner_id
    Backend ->> DataBase: SELECT
    DataBase -->> Backend: Response по конкретному владельцу
    else Во входных данных нет owner_id
    Backend ->> DataBase: SELECT
    DataBase -->> Backend: Response по всем собакам
    end
    Backend -->> Frontend: Response JSON
    Frontend -->> User: Отображает данные
    opt 
    User ->> Frontend: Использовать фильтр по владельцам
    Frontend -->> User: Фильтрует список
    end
    
{{< /mermaid >}} 
 
 
1. Переход на страницу
2. При загрзуке страницы владельца собаки вызывается метод get_dogs
3. Backend обращается в DataBase. Если во входных данных есть owner_id - то отбираем его собак, если нет - вернуть весь список собак.
4. Database возвращает ответ в JSON
5. Backend возвращает ответ в JSON
6. Frontend отображает информацию в интерфейсе


### Входные данные 
| Параметр     | Обязательное поле | Тип данных | Описание                                | 
| ------------ | ----------------- | ---------- | --------------------------------------- | 
| owner_id     |                   | integer    | ID владельца. Eсли во входных данных есть owner_id - то selectим только его собак, если нет - то всех собак        |

### Выходные данные 
| Параметр     | Обязательное поле | Тип данных | Описание                                |
| ------------ | ----------------- | ---------- | --------------------------------------- |
| dogs         |                   |            |                                         |
| [            |                   |            |                                         |
| pet_id       | Y                 | integer    | ID питомца                              |
| name         | Y                 | varchar    | имя питомца                             |
| breed        | Y                 | varchar    | порода                                  |
| age          |                   | integer    | возраст                                 |
| owner_id     |                   | integer    | ID владельца (данный атрибут нужен для определения наличия владельца: заполнено - да, пусто - нет)                                                                              |
| ]            |                   |            |                                         |


```json 
{ 
  "dogs":[
    {
      "pet_id": 321,
      "name": "example",
      "breed": "example",
      "age": "3",
      "owner_id": 123,
    }
  ]
{ 

  
``` 

КОДЫ ОШИБОК