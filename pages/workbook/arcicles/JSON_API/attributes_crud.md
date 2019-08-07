### Работа с дополнительными полями через API.

Для задания дополнительных свойств объекта в сервисе МойСклад есть возможность работы с дополнительными полями (атрибутами). Они представляют собой свойства сущности (объекта или документа), которые формируются пользователем и могут быть использованы для более подробного описания объекта или фильтрации по значениям этих полей. (Подробнее о типах и свойствах доп. полей можно прочитать в документации.)

JSON API позволяет работать со значениями доп. полей, обращаясь к конкретному объекту (документу). Это подробно описано в статье (attributes). В данной же статье рассмотрим на примере магазина ноубуков просмотр, создание, редактирование и удаление самих доп. полей средствами JSON API.

У созданного дополнительного поля есть набор свойств, назначаемых при создании. Некоторые из них можно позднее изменить.

Рассмотрим в качестве примера работу магазина по продаже ноутбуков. Создадим дополнительные поля для товара. После этого рассмотрим их просмотр, редактирование и удаление. При этом наличие самих товаров не обязательно. 

(UI?)

### Создание нового доп. поля через АПИ
Выполним POST-запрос, в теле которого укажем название и тип доп. поля (атрибута). В данном случае добавим строковое поле, описывающее материал корпуса ноутбука. Свойства "name" и "type" являются обязательными для создания нового атрибута. 

Создание двух доп. полей с одинаковыми именами запрещено.


```shell
curl -X POST \
  -u login:password \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes \
  -d '{
    "name": "Материал корпуса",
    "type": "string"
    }'
```

Результат:
```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/acd884ce-b44f-11e9-7ae5-884b00009002",
        "type": "attributemetadata",
        "mediaType": "application/json"
    },
    "id": "acd884ce-b44f-11e9-7ae5-884b00009002",
    "name": "Материал корпуса",
    "type": "string",
    "required": false
}
```

Создано дополнительное поле (атрибут), ему автоматически присвоен id. Значение свойства required по умолчанию устанавливается в false, что делает созданный атрибут не обязательным для заполнения при создании товара.

### Массовое создание(обновление) новых доп. полей через АПИ
Доступно также массовое создание доп. полей. Для этого надо передать в теле POST-запроса массив со свойствами каждого из создаваемых атрибутов.
Массив должен содержать данные по каждому создаваемому полю, перечисленные через запятую и заключенные в фигурные скобки. Обязательные к передаче свойтва - это имя и тип поля. Если добавить к ним id существующего доп. поля, то оно будет изменено.
Сформируем тело запроса из 3 элемнтов. Для поля "Материал корпуса" укажем его id, свойство "name" изменим на "Материал корпуса (дополнение)". Новое значение свойства name не должно совпадать с существующими. Свойство "type" не может быть изменено

```shell
curl -X POST \
  -u login:password \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes \
  -d '[
        {
            "id": "acd884ce-b44f-11e9-7ae5-884b00009002",
            "name": "Материал корпуса (дополнение)",
            "type": "string"
        },
        {
            "name": "Наличие CD-Rom",
            "type": "boolean"
        },
        {
            "name": "Наличие type-C разъема",
            "type": "boolean"
        }
      ]'
```

Результат:
```json
[
    {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/acd884ce-b44f-11e9-7ae5-884b00009002",
            "type": "attributemetadata",
            "mediaType": "application/json"
        },
        "id": "acd884ce-b44f-11e9-7ae5-884b00009002",
        "name": "Материал корпуса (дополнение)",
        "type": "string",
        "required": false
    },
    {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/33b2fe47-b465-11e9-7ae5-884b0001562f",
            "type": "attributemetadata",
            "mediaType": "application/json"
        },
        "id": "33b2fe47-b465-11e9-7ae5-884b0001562f",
        "name": "Наличие CD-Rom",
        "type": "boolean",
        "required": false
    },
    {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/33b30b2e-b465-11e9-7ae5-884b00015630",
            "type": "attributemetadata",
            "mediaType": "application/json"
        },
        "id": "33b30b2e-b465-11e9-7ae5-884b00015630",
        "name": "Наличие type-C разъема",
        "type": "boolean",
        "required": false
    }
]
```

После выполнения данного запроса поле "Материал корпуса" обновится на "Материал корпуса (дополнение)". Добавятся новые поля "Наличие CD-Rom" и "Наличие type-C разъема" с типом флажок.

### Вывод доп. полей через АПИ

Для отображения списка атрибутов сущности нужно выполнить запрос 

```shell
curl \
    -X GET \
    -u login:password \
    -H "Lognex-Pretty-Print-JSON: true" \
    "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata"
```

В ответ получим список созданных атрибутов

```json
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes",
        "type": "attributemetadata",
        "mediaType": "application/json",
        "size": 3,
        "limit": 25,
        "offset": 0
    },
    "rows": [
        {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/acd884ce-b44f-11e9-7ae5-884b00009002",
            "type": "attributemetadata",
            "mediaType": "application/json"
        },
        "id": "acd884ce-b44f-11e9-7ae5-884b00009002",
        "name": "Материал корпуса (дополнение)",
        "type": "string",
        "required": false
    	},
    	{
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/33b2fe47-b465-11e9-7ae5-884b0001562f",
            "type": "attributemetadata",
            "mediaType": "application/json"
        },
        "id": "33b2fe47-b465-11e9-7ae5-884b0001562f",
        "name": "Наличие CD-Rom",
        "type": "boolean",
        "required": false
    	},
   	 	{
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/33b30b2e-b465-11e9-7ae5-884b00015630",
            "type": "attributemetadata",
            "mediaType": "application/json"
        },
        "id": "33b30b2e-b465-11e9-7ae5-884b00015630",
        "name": "Наличие type-C разъема",
        "type": "boolean",
        "required": false
    	}
    ]

```

Если указать в запросе id конкретного атрибута, то получим только его.
(Пример?)

### Редактирование доп. полей через АПИ

Для изменения свойств существующего доп. поля необходимо выполнить PUT-запрос, содержащий его id, а в теле запроса передать изменяемые свойства. Следует учесть, что свойство "type" не может быть изменено. Изменим название атрибута "Наличие CD-Rom":
```shell
curl -X PUT \
  -u login:password \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/33b2fe47-b465-11e9-7ae5-884b0001562f \
  -d '{
        "name":"Наличие DVD-Rom"
      }'
```

Результат:
```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/33b2fe47-b465-11e9-7ae5-884b0001562f",
        "type": "attributemetadata",
        "mediaType": "application/json"
    },
    "id": "9e9baa04-b455-11e9-7ae5-884b0000c7d9",
    "name": "Наличие DVD-Rom",
    "type": "boolean",
    "required": false
}
```
Поле "Наличие CD-Rom" изменено на "Наличие DVD-Rom". Неуказанные свойства останутся без изменений.

### Удаление доп. поля через АПИ
Для удаления доп. поля через АПИ необходимо выполнить DELETE-запрос, содержащий id поля.

```shell
curl -X DELETE \
  -u login:password \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/33b2fe47-b465-11e9-7ae5-884b0001562f \
```
Получим пустой ответ со статусом 200. Атрибут с указанным id будет удален.

### Массовое удаление доп. поля через АПИ
Для удаления сразу нескольких атрибутов нужно выполнить следующий POST-запрос, указав в теле meta-данные удаляемых полей:

```shell
curl -X POST \
  -u login:password \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/delete \
  -d '[
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/acd884ce-b44f-11e9-7ae5-884b00009002",
            "type": "attributemetadata",
            "mediaType": "application/json"
          }
        },
        {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/33b30b2e-b465-11e9-7ae5-884b00015630",
            "type": "attributemetadata",
            "mediaType": "application/json"
          }
        }
      ]'
``` 

Также получим пустой ответ со статусом 200. В результате удалены указанные атрибуты. Если в теле такого запроса указать meta несуществующего атрибута, то весь запрос не выполнится, даже если в нем присутствуют существующие meta.