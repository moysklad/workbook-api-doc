---
title: Метаданные
tags: []
keywords:
summary:
sidebar: workbook_sidebar
permalink: meta.html
folder: workbook
---

# Метаданные
Одним из ключевых понятий при работе с JSON API является понятие метаданных. Под метаданными подразумевается краткое представление сущности или результата запроса JSON API, и описывается в поле `meta`. 
Поле `meta` представляет собой json-объект со следующими атрибутами:
* `href` - ссылка на объект 
* `metadataHref` - cсылка на метаданные сущности
* `type` - тип объекта
* `mediaType` - тип данных, которые приходят в ответ от сервиса, либо отправляются в теле запроса. В рамках данного API всегда равен `application/json`
* `uuidHref` - cсылка на объект в веб-версии МоегоСклада. Присутствует не во всех сущностях

В JSON API выделяются несколько типов метаданных. Рассмотрим их подробнее.

## Метаданные объекта
Возвращаемые JSON API объекты содержат поле `meta`, которое, по сути, является ссылкой на объект. Однако, `meta` является не простым полем, a составным json-элементом, содержащим краткое описание объекта.
Рассмотрим запрос контрагента
```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/ab4dd5fc-d100-11e8-ac12-00080000006d",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=ab4dd5fc-d100-11e8-ac12-00080000006d"
    },
    "id": "ab4dd5fc-d100-11e8-ac12-00080000006d",
    "accountId": "aab5daf6-d100-11e8-ac12-000a00000000",
    "owner": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/employee/ab306d83-d100-11e8-ac12-000800000042",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/employee/metadata",
            "type": "employee",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=ab306d83-d100-11e8-ac12-000800000042"
        }
    },
    "shared": false,
    "group": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/group/aab73291-d100-11e8-ac12-000a00000001",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/group/metadata",
            "type": "group",
            "mediaType": "application/json"
        }
    },
    "version": 0,
    "updated": "2018-10-16 08:02:24",
    "name": "ООО \"Поставщик\"",
    "externalCode": "42lMvkcLgj6LO6UYJLH9H3",
    "archived": false,
    "created": "2018-10-16 08:02:23",
    "companyType": "legal",
    "legalTitle": "Общество с ограниченной ответственностью \"Поставщик\"",
    "legalAddress": "г.Москва, ул.Строителей, д.12",
    "inn": "7736570901",
    "kpp": "773601001",
    "accounts": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/ab4dd5fc-d100-11e8-ac12-00080000006d/accounts",
            "type": "account",
            "mediaType": "application/json",
            "size": 0,
            "limit": 100,
            "offset": 0
        }
    },
    "tags": [],
    "contactpersons": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/ab4dd5fc-d100-11e8-ac12-00080000006d/contactpersons",
            "type": "contactperson",
            "mediaType": "application/json",
            "size": 0,
            "limit": 100,
            "offset": 0
        }
    },
    "notes": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/ab4dd5fc-d100-11e8-ac12-00080000006d/notes",
            "type": "note",
            "mediaType": "application/json",
            "size": 0,
            "limit": 100,
            "offset": 0
        }
    },
    "salesAmount": 0
}
```

В ответе содержится несколько полей `meta`.
Вначале описывается сам объект, с указанием тип объекта, ссылки в JSON API и ссылки на веб-версию
```json
"meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/ab4dd5fc-d100-11e8-ac12-00080000006d",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/counterparty/metadata",
        "type": "counterparty",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#company/edit?id=ab4dd5fc-d100-11e8-ac12-00080000006d"
    }
```

Ссылки на сотрудника, создавшего контрагента, и отдел сотрудника указаны в полях `owner` и `group`, и содержат также поля `meta`.
```json
"owner": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/employee/ab306d83-d100-11e8-ac12-000800000042",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/employee/metadata",
            "type": "employee",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=ab306d83-d100-11e8-ac12-000800000042"
        }
    },
    "group": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/group/aab73291-d100-11e8-ac12-000a00000001",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/group/metadata",
            "type": "group",
            "mediaType": "application/json"
        }
    }
```

Очевидно, что поля `href` и `uuidHref` содержат url для доступа к объектам и могут быть использованы для запроса.
Например, используя значение поля `href`, запросим данные сотрудника
```shell
curl -X GET \
  https://online.moysklad.ru/api/remap/1.1/entity/employee/ab306d83-d100-11e8-ac12-000800000042 \
  -H 'Authorization: Basic token=' \
  -H 'Cache-Control: no-cache'
```
```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/employee/ab306d83-d100-11e8-ac12-000800000042",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/employee/metadata",
        "type": "employee",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=ab306d83-d100-11e8-ac12-000800000042"
    },
    "id": "ab306d83-d100-11e8-ac12-000800000042",
    "accountId": "aab5daf6-d100-11e8-ac12-000a00000000",
    "owner": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/employee/ab306d83-d100-11e8-ac12-000800000042",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/employee/metadata",
            "type": "employee",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=ab306d83-d100-11e8-ac12-000800000042"
        }
    },
    "shared": true,
    "group": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/group/aab73291-d100-11e8-ac12-000a00000001",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/group/metadata",
            "type": "group",
            "mediaType": "application/json"
        }
    },
    "version": 1,
    "updated": "2018-10-16 08:02:24",
    "name": "Администратор",
    "externalCode": "nGxKpV-ejSRXZcxV5ZHau1",
    "archived": false,
    "created": "2018-10-16 08:02:23",
    "uid": "admin@b",
    "email": "b@b.ru",
    "lastName": "Администратор",
    "fullName": "Администратор",
    "shortFio": "Администратор",
    "cashier": {
        "id": "ab7ee032-d100-11e8-ac12-00080000007a",
        "accountId": "aab5daf6-d100-11e8-ac12-000a00000000",
        "employee": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/employee/ab306d83-d100-11e8-ac12-000800000042",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/employee/metadata",
                "type": "employee",
                "mediaType": "application/json",
                "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=ab306d83-d100-11e8-ac12-000800000042"
            }
        },
        "retailStore": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/retailstore/ab7e77a1-d100-11e8-ac12-000800000079",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/retailstore/metadata",
                "type": "retailstore",
                "mediaType": "application/json",
                "uuidHref": "https://online.moysklad.ru/app/#retailstore/edit?id=ab7e77a1-d100-11e8-ac12-000800000079"
            }
        }
    }
}
```
Аналогично и для значения из поля `uuidHref`
![useful image]({{ site.url }}/images/meta/owner.png)

### Использование meta при создании/изменении объекта
`meta` используется в качестве ссылки на другой объект, рассмотрим на примерах.

Имеем метаданные товара
```json
"meta":{
               "href":"https://online.moysklad.ru/api/remap/1.1/entity/product/3b336cc5-d10a-11e8-ac12-000b00000021",
               "metadataHref":"https://online.moysklad.ru/api/remap/1.1/entity/product/metadata",
               "type":"product",
               "mediaType":"application/json",
               "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=3b335997-d10a-11e8-ac12-000b0000001f"
            }
```
Выполним запрос на создание комплекта, указав товар в компонентах
```shell
curl -X POST \
  'https://online.moysklad.ru/api/remap/1.1/entity/bundle?expand=components' \
  -H 'Authorization: Basic token=' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -d '{
   "name":"Набор карандашей",
   "components":[
      {
         "assortment":{
            "meta":{
               "href":"https://online.moysklad.ru/api/remap/1.1/entity/product/3b336cc5-d10a-11e8-ac12-000b00000021",
               "metadataHref":"https://online.moysklad.ru/api/remap/1.1/entity/product/metadata",
               "type":"product",
               "mediaType":"application/json",
               "uuidHref":"https://online.moysklad.ru/app/#good/edit?id=3b335997-d10a-11e8-ac12-000b0000001f"
            }
         },
         "quantity":10
      }
   ]
}'
```
В ответ получим новый комлпект, который содержит указанный товар
```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/bundle/63aa9594-d13f-11e8-ac12-000b00000047?expand=components",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/bundle/metadata",
        "type": "bundle",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=63aa8826-d13f-11e8-ac12-000b00000045"
    },
    "id": "63aa9594-d13f-11e8-ac12-000b00000047",
    "accountId": "aab5daf6-d100-11e8-ac12-000a00000000",
    "owner": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/employee/ab306d83-d100-11e8-ac12-000800000042",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/employee/metadata",
            "type": "employee",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=ab306d83-d100-11e8-ac12-000800000042"
        }
    },
    "shared": true,
    "group": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/group/aab73291-d100-11e8-ac12-000a00000001",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/group/metadata",
            "type": "group",
            "mediaType": "application/json"
        }
    },
    "version": 0,
    "updated": "2018-10-16 15:31:21",
    "name": "Набор карандашей",
    "code": "00012",
    "externalCode": "tzHoMUWWhvekJxhapMxUO3",
    "archived": false,
    "pathName": "",
    "minPrice": 0,
    "salePrices": [
        {
            "value": 0,
            "currency": {
                "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.1/entity/currency/ab4e7603-d100-11e8-ac12-000800000071",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json",
                    "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=ab4e7603-d100-11e8-ac12-000800000071"
                }
            },
            "priceType": "Цена продажи"
        }
    ],
    "weight": 0,
    "volume": 0,
    "barcodes": [
        "2000000000237"
    ],
    "components": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/bundle/63aa9594-d13f-11e8-ac12-000b00000047/components",
            "type": "bundlecomponent",
            "mediaType": "application/json",
            "size": 1,
            "limit": 100,
            "offset": 0
        },
        "rows": [
            {
                "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.1/entity/bundle/63aa9594-d13f-11e8-ac12-000b00000047/components/63aa9eb7-d13f-11e8-ac12-000b0000004a",
                    "type": "bundlecomponent",
                    "mediaType": "application/json"
                },
                "id": "63aa9eb7-d13f-11e8-ac12-000b0000004a",
                "accountId": "aab5daf6-d100-11e8-ac12-000a00000000",
                "assortment": {
                    "meta": {
                        "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/3b336cc5-d10a-11e8-ac12-000b00000021",
                        "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata",
                        "type": "product",
                        "mediaType": "application/json",
                        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b335997-d10a-11e8-ac12-000b0000001f"
                    }
                },
                "quantity": 10
            }
        ]
    }
}
```

А, теперь попробуем изменить товар, указав ему единицу измерения.
```shell
curl -X PUT \
  https://online.moysklad.ru/api/remap/1.1/entity/product/3b336cc5-d10a-11e8-ac12-000b00000021 \
  -H 'Authorization: Basic token=' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -d '{
   "uom":{
      "meta":{
         "href":"https://online.moysklad.ru/api/remap/1.1/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
         "metadataHref":"https://online.moysklad.ru/api/remap/1.1/entity/uom/metadata",
         "type":"uom",
         "mediaType":"application/json"
      }
   }
}'
```
В ответе видно, что единица измерения, поле `uom`, изменилось на переданный объект.
```json
{
    "meta": {
        "href": "https://online.moysklad.ru/api/remap/1.1/entity/product/3b336cc5-d10a-11e8-ac12-000b00000021",
        "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/product/metadata",
        "type": "product",
        "mediaType": "application/json",
        "uuidHref": "https://online.moysklad.ru/app/#good/edit?id=3b335997-d10a-11e8-ac12-000b0000001f"
    },
    "id": "3b336cc5-d10a-11e8-ac12-000b00000021",
    "accountId": "aab5daf6-d100-11e8-ac12-000a00000000",
    "owner": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/employee/ab306d83-d100-11e8-ac12-000800000042",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/employee/metadata",
            "type": "employee",
            "mediaType": "application/json",
            "uuidHref": "https://online.moysklad.ru/app/#employee/edit?id=ab306d83-d100-11e8-ac12-000800000042"
        }
    },
    "shared": true,
    "group": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/group/aab73291-d100-11e8-ac12-000a00000001",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/group/metadata",
            "type": "group",
            "mediaType": "application/json"
        }
    },
    "version": 1,
    "updated": "2018-10-16 15:41:02",
    "name": "Карандаш",
    "code": "00006",
    "externalCode": "2cqTjWwjh7haLuGaokYLW0",
    "archived": false,
    "pathName": "",
    "syncId": "2b7c97cf-cf77-4f7e-b200-d264125578ab",
    "uom": {
        "meta": {
            "href": "https://online.moysklad.ru/api/remap/1.1/entity/uom/19f1edc0-fc42-4001-94cb-c9ec9c62ec10",
            "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/uom/metadata",
            "type": "uom",
            "mediaType": "application/json"
        }
    },
    "minPrice": 0,
    "salePrices": [
        {
            "value": 0,
            "currency": {
                "meta": {
                    "href": "https://online.moysklad.ru/api/remap/1.1/entity/currency/ab4e7603-d100-11e8-ac12-000800000071",
                    "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/currency/metadata",
                    "type": "currency",
                    "mediaType": "application/json",
                    "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=ab4e7603-d100-11e8-ac12-000800000071"
                }
            },
            "priceType": "Цена продажи"
        }
    ],
    "buyPrice": {
        "value": 0,
        "currency": {
            "meta": {
                "href": "https://online.moysklad.ru/api/remap/1.1/entity/currency/ab4e7603-d100-11e8-ac12-000800000071",
                "metadataHref": "https://online.moysklad.ru/api/remap/1.1/entity/currency/metadata",
                "type": "currency",
                "mediaType": "application/json",
                "uuidHref": "https://online.moysklad.ru/app/#currency/edit?id=ab4e7603-d100-11e8-ac12-000800000071"
            }
        }
    },
    "weight": 0.1,
    "volume": 0,
    "barcodes": [
        "2000000000176"
    ],
    "modificationsCount": 0,
    "isSerialTrackable": false
}
```

## Метаданные коллекции

## Метаданные сущности