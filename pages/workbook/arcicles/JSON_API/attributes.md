---
title: Дополнительные поля
tags: []
keywords:
summary:
sidebar: workbook_sidebar
permalink: attributes.html
folder: workbook
---
Если вы хотите сохранить информацию, для которой нет подходящего поля в документе или справочнике, вы можете создать дополнительные поля.

### Список сущностей
Список сущностей, у которых есть доп. поля, вы можете посмотреть в [документации](https://online.moysklad.ru/api/remap/1.1/doc/index.html#header-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%B4%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%BC%D0%B8-%D0%BF%D0%BE%D0%BB%D1%8F%D0%BC%D0%B8)

### Работа с дополнительными полями в АПИ
В рамках JSON API нельзя создавать дополнительные поля, но можно работать с уже созданными через основной интерфейс полями.

### Получение доп. полей
Запросить список доступных полей можно, воспользовавшись запросом метаданных необходимой вам сущности. Ниже приведен пример запроса метаданных товаров, в поле **attributes** выводится массив дополнительных полей:

```shell
curl \
    -X GET \
    -u login:password \
    -H "Lognex-Pretty-Print-JSON: true" \
    "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata"
```

Результат:
```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata",
        "mediaType": "application/json"
    },
    "attributes": [
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/839ca663-75f7-11e8-9107-5048001126a2",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "id": "839ca663-75f7-11e8-9107-5048001126a2",
            "name": "Особенности",
            "type": "string",
            "required": false
        },
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/839ca663-75f7-11e8-9107-5048001126a3",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "id": "839ca663-75f7-11e8-9107-5048001126a2",
            "name": "Объем накопителя",
            "type": "number",
            "required": false
        },
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/839ca663-75f7-11e8-9107-5048001126a3",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "id": "839ca663-75f7-11e8-9107-5048001126a2",
            "name": "Дата поступления на склад",
            "type": "time",
            "required": false
        },
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/46908d10-c4e5-11e8-9109-f8fc00209552",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "customEntityMeta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/companysettings/metadata/customEntities/9e690967-1703-4038-a8f7-95ef64d54ae6",
                "type": "customentitymetadata",
                "mediaType": "application/json"
            },
            "id": "46908d10-c4e5-11e8-9109-f8fc00209552",
            "name": "Материал изготовления",
            "type": "customentity",
            "required": false
        },
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/839ca663-75f7-11e8-9107-5048001126a3",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "id": "839ca663-75f7-11e8-9107-5048001126a2",
            "name": "Спецификация",
            "type": "file",
            "required": false
        },
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/839ca663-75f7-11e8-9107-5048001126a3",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "id": "839ca663-75f7-11e8-9107-5048001126a2",
            "name": "Время работы от аккумулятора",
            "type": "double",
            "required": false
        },
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/839ca663-75f7-11e8-9107-5048001126a3",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "id": "839ca663-75f7-11e8-9107-5048001126a2",
            "name": "Подсветка клавиатуры",
            "type": "boolean",
            "required": false
        },
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/839ca663-75f7-11e8-9107-5048001126a3",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "id": "839ca663-75f7-11e8-9107-5048001126a2",
            "name": "Описание от производителя",
            "type": "text",
            "required": false
        },
        {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/7385ab6e-ad06-11e8-9ff4-34e80004fb35",
                "type": "attributemetadata",
                "mediaType": "application/json"
            },
            "id": "7385ab6e-ad06-11e8-9ff4-34e80004fb35",
            "name": "Ссылка на интернет-магазин",
            "type": "link",
            "required": false
        }
    ],
    "priceTypes": [
        {
            "name": "Цена продажи"
        }
    ],
    "createShared": true
}
```

### Задание значений доп. полей через АПИ
Задать значение доп. полю можно как при создании объекта, так и при его обновлении.

После того, как выше мы получили идентификаторы дополнительных полей товаров, мы можем использовать их при создании новых товаров:
```shell
curl \
    -X POST \
    -u login:password \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    https://online.moysklad.ru/api/remap/1.1/entity/product \
    -d '{
        "name": "Ноутбук",
        "vat": 18,
        "effectiveVat": 18,
        "uom": {
        "meta": {
          "href": "https://online.moysklad.ru/api/remap/1.1/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
          "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/uom/metadata",
          "type": "uom",
          "mediaType": "application/json"
        }
        },
        "minPrice": 50000,
        "buyPrice": {
        "value": 50000,
        "currency": {
          "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/currency/metadata",
            "type": "currency",
            "mediaType": "application/json"
          }
        }
        },
        "salePrices": [
        {
          "value": 100000,
          "currency": {
            "meta": {
              "href": "https://online.moysklad.ru/api/remap/1.1/entity/currency/6314188d-2c7f-11e6-8a84-bae500000055",
              "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/currency/metadata",
              "type": "currency",
              "mediaType": "application/json"
            }
          },
          "priceType": "Цена продажи"
        }
        ],
        "attributes": [
            {
              "id": "839ca663-75f7-11e8-9107-5048001126a2",
              "name": "Время работы от аккумулятора",
              "type": "double",
              "value": 9.6
            },
            {
              "id": "839ca663-75f7-11e8-9107-5048001126a3",
              "name": "Спецификация",
              "type": "file",
              "file": {
                "name": "filename",
                "content": "5cYwMpOmNk5kSVr4YgZGKtXJb/7KpHVLDUawyZrD5Nf0WDhB7mS1I77VcAMqYQ8DkP/1wDLhb0X6b2JO4pdpKA=="
              }
            }
        ]
    }'
```
Для нового товара "Ноутбук" мы указали значения двух доп. полей - `Время работы от аккумулятора` и `Спецификация`. Так как все доп. поля товара из нашего примера имеют флаг **required=false**, т.е. не являются обязательными, то не обязательно задавать значения всем доп. полям.

При обновлении товара мы можем как обновить уже имеющиеся значения доп. полей, так и задать новые.
```shell
curl \
    -X PUT \
    -u login:password \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    https://online.moysklad.ru/api/remap/1.1/entity/product/630c578a-cb05-11e8-9109-f8fc0037889a \
    -d '{
  "name": "Ноутбук обновленный",
  "attributes": [
    {
      "id": "839ca663-75f7-11e8-9107-5048001126a2",
      "name": "Время работы от аккумулятора",
      "type": "double",
      "value": 10.6
    },
    {
      "id": "839ca663-75f7-11e8-9107-5048001126a2",
      "name": "Подсветка клавиатуры",
      "type": "boolean",
      "value": "true"
    }
  ]
}'
```
В примере мы обновили значение поля `Время работы от аккумулятора`, проставленное при создании товара, а также задали значение полю `Подсветка клавиатуры` - при создании мы оставили его пустым.

Также для необязательных полей есть возможность обнулить значение поля. Для этого в поле **value** необходимо передать значение **null**.

Если в теле запроса на обновление/создание сущности в массиве доп. полей:

+ Не указаны id каких-либо доп. полей - доп. поля обновлены не будут.
+ Указаны id доп. полей, которым в данной сущности ещё не присвоено значение - соответствующим доп. полям будут присвоены переданные значения.
+ Указаны id доп. полей, которым в данной сущности уже присвоено значение - соответствующим доп. полям будут присвоены новые значения.
+ Указан несуществующий id, которого нет в метаданных сущности - возникнет ошибка.

### Возможные типы доп. полей
С возможными типами доп. полей вы можете ознакомиться в [документации](https://online.moysklad.ru/api/remap/1.1/doc/index.html#header-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D0%B4%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%BC%D0%B8-%D0%BF%D0%BE%D0%BB%D1%8F%D0%BC%D0%B8).

### Доп. поле типа Файл
Для загрузки значения доп. поля типа файл нужно в поле **value** указать объект следующей структуры:

+ filename - Имя файла `Необходимое`
+ content - Байты файла, закодированные в base64 `Необходимое`

Пример создания товара с доп. полем типа Файл приведен ниже
```shell
curl \
    -X POST \
    -u login:password \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    https://online.moysklad.ru/api/remap/1.1/entity/product \
    -d '{
    "name": "Ноутбук",
    "attributes": [
        {
          "id": "839ca663-75f7-11e8-9107-5048001126a3",
          "name": "Спецификация",
          "type": "file",
          "file": {
            "name": "filename",
            "content": "5cYwMpOmNk5kSVr4YgZGKtXJb/7KpHVLDUawyZrD5Nf0WDhB7mS1I77VcAMqYQ8DkP/1wDLhb0X6b2JO4pdpKA=="
          }
        }
    ]
}'
```
### Фильтрация по значению дополнительного поля
JSON API позволяет осуществлять фильтрацию по значению дополнительного поля. На примере дополнительных полей, приведенных выше, можно отфильтровать все товары, у которых значение доп. поля `Время работы от аккумулятора` больше или равно 5:
```shell
curl \
    -X GET \
    -u login:password \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    "https://online.moysklad.ru/api/remap/1.1/entity/product?filter=https://online.moysklad.ru/api/remap/1.1/entity/product/metadata/attributes/630c578a-cb05-11e8-9109-f8fc0037889a%3E%3D5"
```

Для этого нам необходимо в параметре filter указан href доп. поля для фильтрации, знак сравнения (в нашем случае `>=`) и значение. В ответе вернутся все сущности, подходящие под переданный критерий.

### Сортировка по дополнительному полю
Сортировка по доп. полям в данный момент не поддерживается.