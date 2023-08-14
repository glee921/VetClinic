## Метод get_list_pets
 
Метод, котоырй будет возвращать список питомцев владельца.
 
### Общее описание 
 
* Архитектура: REST 
* Тип метода: GET 
* URL: v1/get_list_pets
* Протокол взаимодействия: HTTPS 
* Формат входных данных: QUERY PARAMS
* Формат выходных данных: JSON 
* Тип вызова: Синхронный 
 
### Описание алгоритма 
 
mermaid 
{{< mermaid >}} 
sequenceDiagram 
     
    actor Client 
    participant Platformeco 
    participant PostgreSQL 
    Client->>+Platformeco: POST data for needs 
    Platformeco->>Platformeco: use Shared Flow core_createNewNeeds_SF 
    Platformeco->>+PostgreSQL: INSERT comment for need 
    Platformeco->>+ELT: use ELT methods (POST /integration/v1/elt/assistance/save) 
    Platformeco->>+PostgreSQL: INSERT data for needs 
    end 
{{< /mermaid >}} 
 
 
1. Пользователь из предварительных расчётов от страховых компаний по продукту Карты помощи на дороге выбирает конкретное предложение для оформления окончательного расчёта. На вход дефиниция получает JSON объект, содержащий свойство data_as_json c данными для создания потребности и данными для записи в базу. 
2. Для генерации uuid потребностей (needs_and_orders_b_uuid) необходимо использовать Shared Flow core_createNewNeeds_SF. 
3. Для верхнеуровневой потребности, uuid которой приходит к нам в параметре "needs_and_orders_b4generalizing_need_uuid" - в таблицу needs_and_orders_comments_b добавить комментарий, который пришел в параметре "good_as_text_description".<br>Использовать Shared Flow 
### Входные данные 
 
#### Входные данные для Оформления страховых продуктов + описание параметров 
 
```json 
{ 
  "f_and_i_calculation_purpose_d_uuid": "9415fa64-0938-46ca-b467-5077331cb2bf", // ссылка на справочник со значением Окончательный расчет 
  "communication_b_uuid": "", //uuid передаем с фронта из данных предыдущего метода 
  "persons_or_org_s4client_uuid": "", //uuid передаем с фронта из данных предыдущего метода 
  "business_domain_d_uuid": "e805886c-c8d3-4108-b7ec-1cff6ea08231", //По умолчанию - Фин. услуги 
  "good_ref_type_d_uuid": "661e68b9-7901-49c0-89aa-4c1a30015bb2", //По умолчанию - Конкретные данные услуги F&I 
  "quantity": 1, //По умолчанию 1, может быть передам с фронта 
  "needs_and_orders_class_d_uuid": "82109a9a-409a-11ed-b878-0242ac120002", //По умолчанию - Продажа 
  "operation_direction_sign": 1, //По умолчанию - 1 
  "is_return": false, //По умолчанию - Нет 
  "sale_stage_d_uuid": "d2dbebe6-409a-11ed-b878-0242ac120002", //по умолчанию 
  "good_as_vehicle_b_uuid": "", //Не заполняется 
  "needs_and_orders_b4generalizing_need_uuid": "", // ДОБАВИТЬ uuid потребности “Страховка” передаем с фронта из данных предыдущего метода 
  "persons_or_org_s4salesman_uuid": "", // uuid текущего авторизованного пользователя, передаем с фронта 
  "data_as_json": { 
  "CFO": 2, 
  "calculationId":