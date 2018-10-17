---
title: Работа с коллекциями - сортировка
tags: []
keywords:
summary:
sidebar: workbook_sidebar
permalink: sorting.html
folder: workbook
---
# Сортировка
Для большинства коллекций, возвращаемых JSON API, доступна сортировка.

Сортировка поддерживается для следующих типов полей:
* числовой, 
* строковый, 
* дата-время, 
* логический,
* uuid.

## Доступные поля для сортировки
В зависимости от вызываемого endpoint'а сортируемые поля могут отличаться.
В таблицах ниже представлены сортируемые поля справочников и документов.

| Endpoint (справочники) | Сортируемые поля |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Контрагент](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%BA%D0%BE%D0%BD%D1%82%D1%80%D0%B0%D0%B3%D0%B5%D0%BD%D1%82-%D0%BA%D0%BE%D0%BD%D1%82%D1%80%D0%B0%D0%B3%D0%B5%D0%BD%D1%82%D1%8B-get)|`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`, `name`, `description`, `code`, `externalCode`, `archived`, `created`, `inn`, `actualAddress`, `legalTitle`, `legalAddress`, `kpp`, `phone`, `email`, `fax`, `discountCardNumber`, `priceType` |
| [Валюта](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B2%D0%B0%D0%BB%D1%8E%D1%82%D0%B0-%D0%B2%D0%B0%D0%BB%D1%8E%D1%82%D1%8B-get)|`id`, `accountId`, `name`, `archived`, `shared`, `default`, `fullname`, `code`, `isoCode`, `multiplicity`                                                                                                                                      |
| [Товар](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%82%D0%BE%D0%B2%D0%B0%D1%80-%D1%82%D0%BE%D0%B2%D0%B0%D1%80%D1%8B-get)|`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`,  `name`, `description`, `code`, `externalCode`, `archived`, `pathName`, `syncId`, `vat`, `isSerialTrackable`, `article`, `weighed`, `weight`, `volume`, `minimumBalance`                  |
| [Услуга](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%83%D1%81%D0%BB%D1%83%D0%B3%D0%B0-%D1%83%D1%81%D0%BB%D1%83%D0%B3%D0%B8-get)|`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`, `name`, `description`, `code`, `externalCode`, `archived`, `pathName`, `syncId`                                                                                             |
| [Комплект](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%BA%D0%BE%D0%BC%D0%BF%D0%BB%D0%B5%D0%BA%D1%82-%D0%BA%D0%BE%D0%BC%D0%BF%D0%BB%D0%B5%D0%BA%D1%82%D1%8B-get)|`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`, `name`, `description`, `code`, `externalCode`, `archived`, `pathName`, `syncId`, `article`, `weight`, `volume`                                                                    |
| [Группа товаров](https://online.moysklad.ru/api/remap/1.1/doc/index.html#группа-товаров-группы-товаров-get)|`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`, `name`, `description`, `code`, `externalCode`, `archived`, `pathName`                                                                                                     |
| [Модификация](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%BC%D0%BE%D0%B4%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F-%D0%BC%D0%BE%D0%B4%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8-get)|`name`, `description`, `code`,  `externalCode`, `archived`                                                                                                                                                                           |
| [Серия](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%81%D0%B5%D1%80%D0%B8%D1%8F-%D1%81%D0%B5%D1%80%D0%B8%D0%B8-get)|`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`                                                                                                                      |
| [Договор](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%B3%D0%BE%D0%B2%D0%BE%D1%80-%D0%B4%D0%BE%D0%B3%D0%BE%D0%B2%D0%BE%D1%80%D1%8B-get)|`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`, `name`, `description`, `code`, `externalCode`, `archived`, `moment`                                                                                                       |
| [Проект](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D1%8B-get)|`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`, `archived`                                                                                                            |
| [Статья расходов](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%81%D1%82%D0%B0%D1%82%D1%8C%D1%8F-%D1%80%D0%B0%D1%81%D1%85%D0%BE%D0%B4%D0%BE%D0%B2-%D1%81%D1%82%D0%B0%D1%82%D1%8C%D0%B8-%D1%80%D0%B0%D1%81%D1%85%D0%BE%D0%B4%D0%BE%D0%B2-get)|`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`                                                                                                                      |
| [Страна](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%81%D1%82%D1%80%D0%B0%D0%BD%D0%B0-%D1%81%D1%82%D1%80%D0%B0%D0%BD%D1%8B-get)|`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`                                                                                                                      |
| [Отдел](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%BE%D1%82%D0%B4%D0%B5%D0%BB-%D0%BE%D1%82%D0%B4%D0%B5%D0%BB%D1%8B-get)|`id`, `accountId`                                                                                                                                                                                                              |
| [Единица измерения](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B5%D0%B4%D0%B8%D0%BD%D0%B8%D1%86%D0%B0-%D0%B8%D0%B7%D0%BC%D0%B5%D1%80%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B5%D0%B4%D0%B8%D0%BD%D0%B8%D1%86%D1%8B-%D0%B8%D0%B7%D0%BC%D0%B5%D1%80%D0%B5%D0%BD%D0%B8%D1%8F-get)|`id`,  `accountId`, `name`, `archived`, `shared`, `default`, `fullname`, `code`, `isoCode`, `multiplicity`                                                                                                                                     |
| [Сотрудник](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%81%D0%BE%D1%82%D1%80%D1%83%D0%B4%D0%BD%D0%B8%D0%BA-%D1%81%D0%BE%D1%82%D1%80%D1%83%D0%B4%D0%BD%D0%B8%D0%BA%D0%B8-get)|`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`, `name`, `description`, `code`, `externalCode`,`archived`,`email`,`phone`,`lastname`, `firstname`, `middlename`, `uid`                                                               |
| [Склад](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%81%D0%BA%D0%BB%D0%B0%D0%B4-%D1%81%D0%BA%D0%BB%D0%B0%D0%B4%D1%8B-get)|`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`, `address`, `active`                                                                                                     |
| [Юрлицо](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%8E%D1%80%D0%BB%D0%B8%D1%86%D0%BE-%D1%8E%D1%80%D0%BB%D0%B8%D1%86%D0%B0-get)|`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`, `archived`, `created`, `inn`, `actualAddress`, `legalTitle`, `legalAddress`, `kpp`, `phone`, `email`, `fax`                             |
| [Точка продаж](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D1%82%D0%BE%D1%87%D0%BA%D0%B0-%D0%BF%D1%80%D0%BE%D0%B4%D0%B0%D0%B6-%D1%82%D0%BE%D1%87%D0%BA%D0%B8-%D0%BF%D1%80%D0%BE%D0%B4%D0%B0%D0%B6-get)|`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`, `address`, `active`                                                                                                     |
| [Задача](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D0%B0-%D0%B7%D0%B0%D0%B4%D0%B0%D1%87%D0%B8-get)|`id`, `accountId`, `created`, `version`, `updated`, `deleted`, `description`, `dueToDate`, `done`                                                                                                                                            |                                                                                                                                                                                                                           |                                                                                                                                                                                                        |

| Endpoint (документы) | Сортируемые поля |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Розничная смена](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%80%D0%BE%D0%B7%D0%BD%D0%B8%D1%87%D0%BD%D0%B0%D1%8F-%D1%81%D0%BC%D0%B5%D0%BD%D0%B0-%D1%80%D0%BE%D0%B7%D0%BD%D0%B8%D1%87%D0%BD%D1%8B%D0%B5-%D1%81%D0%BC%D0%B5%D0%BD%D1%8B-get)               |`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`, `name`, `description`, `code`, `externalCode`, `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `closeDate`                                              |
| [Оприходования](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%BE%D0%BF%D1%80%D0%B8%D1%85%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BE%D0%BF%D1%80%D0%B8%D1%85%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-get)                 |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`,  `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`,  `sum`, `isDeleted`, `created`                                                   |
| [Заказ покупателя](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7-%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%B0%D1%82%D0%B5%D0%BB%D1%8F-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7%D1%8B-%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%B0%D1%82%D0%B5%D0%BB%D0%B5%D0%B9-get)              |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`,  `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`,  `sum`, `isDeleted`, `created`, `deliveryPlannedMoment`                            |
| [Заказ поставщику](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA%D1%83-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7%D1%8B-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA%D0%B0%D0%BC-get)              |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`,  `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`,  `sum`, `isDeleted`, `created`, `deliveryPlannedMoment`                            |
| [Счет покупателю](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%81%D1%87%D1%91%D1%82-%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%B0%D1%82%D0%B5%D0%BB%D1%8E-%D1%81%D1%87%D0%B5%D1%82%D0%B0-%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%B0%D1%82%D0%B5%D0%BB%D1%8F%D0%BC-get)               |`id`,   `accountId`, `shared`, `version`, `updated`,   `updatedBy`, `deleted`,   `name`, `description`, `code`,   `externalCode`,   `syncId`, `moment`, `applicable`,   `sum`, `isDeleted`, `created`                                             |
| [Счет поставщика](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%81%D1%87%D1%91%D1%82-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA%D0%B0-%D1%81%D1%87%D0%B5%D1%82%D0%B0-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA%D0%BE%D0%B2-get)               |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `incomingNumber`, `incomingDate`, `paymentPlannedMoment` |
| [Входящий платеж](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B2%D1%85%D0%BE%D0%B4%D1%8F%D1%89%D0%B8%D0%B9-%D0%BF%D0%BB%D0%B0%D1%82%D0%B5%D0%B6-%D0%B2%D1%85%D0%BE%D0%B4%D1%8F%D1%89%D0%B8%D0%B5-%D0%BF%D0%BB%D0%B0%D1%82%D0%B5%D0%B6%D0%B8-get)               |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `paymentPurpose`, `incomingNumber`, `incomingDate`       |
| [Исходящий платеж](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B8%D1%81%D1%85%D0%BE%D0%B4%D1%8F%D1%89%D0%B8%D0%B9-%D0%BF%D0%BB%D0%B0%D1%82%D0%B5%D0%B6-%D0%B8%D1%81%D1%85%D0%BE%D0%B4%D1%8F%D1%89%D0%B8%D0%B5-%D0%BF%D0%BB%D0%B0%D1%82%D0%B5%D0%B6%D0%B8-get)              |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `paymentPurpose`                                     |
| [Приходный ордер](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%BF%D1%80%D0%B8%D1%85%D0%BE%D0%B4%D0%BD%D1%8B%D0%B9-%D0%BE%D1%80%D0%B4%D0%B5%D1%80-%D0%BF%D1%80%D0%B8%D1%85%D0%BE%D0%B4%D0%BD%D1%8B%D0%B5-%D0%BE%D1%80%D0%B4%D0%B5%D1%80%D0%B0-get)               |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `paymentPurpose`                                     |
| [Расходный ордер](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%80%D0%B0%D1%81%D1%85%D0%BE%D0%B4%D0%BD%D1%8B%D0%B9-%D0%BE%D1%80%D0%B4%D0%B5%D1%80-%D1%80%D0%B0%D1%81%D1%85%D0%BE%D0%B4%D0%BD%D1%8B%D0%B5-%D0%BE%D1%80%D0%B4%D0%B5%D1%80%D0%B0-get)               |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `paymentPurpose`                                     |
| [Отгрузка](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%BE%D1%82%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0-%D0%BE%D1%82%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B8-get)                      |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Приемка](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%BF%D1%80%D0%B8%D1%91%D0%BC%D0%BA%D0%B0-%D0%BF%D1%80%D0%B8%D1%91%D0%BC%D0%BA%D0%B8-get)                       |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Списание](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%81%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D0%B5-%D1%81%D0%BF%D0%B8%D1%81%D0%B0%D0%BD%D0%B8%D1%8F-get)                      |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Перемещение](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%BF%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D1%89%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BF%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D1%89%D0%B5%D0%BD%D0%B8%D1%8F-get)                   |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Розничная продажа](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%80%D0%BE%D0%B7%D0%BD%D0%B8%D1%87%D0%BD%D0%B0%D1%8F-%D0%BF%D1%80%D0%BE%D0%B4%D0%B0%D0%B6%D0%B0-%D1%80%D0%BE%D0%B7%D0%BD%D0%B8%D1%87%D0%BD%D1%8B%D0%B5-%D0%BF%D1%80%D0%BE%D0%B4%D0%B0%D0%B6%D0%B8-get)             |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Розничный возврат](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%80%D0%BE%D0%B7%D0%BD%D0%B8%D1%87%D0%BD%D1%8B%D0%B9-%D0%B2%D0%BE%D0%B7%D0%B2%D1%80%D0%B0%D1%82-%D1%80%D0%BE%D0%B7%D0%BD%D0%B8%D1%87%D0%BD%D1%8B%D0%B5-%D0%B2%D0%BE%D0%B7%D0%B2%D1%80%D0%B0%D1%82%D1%8B-get)             |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Внесение денег](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B2%D0%BD%D0%B5%D1%81%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%B5%D0%BD%D0%B5%D0%B3-%D0%B2%D0%BD%D0%B5%D1%81%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B4%D0%B5%D0%BD%D0%B5%D0%B3-get)                |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Выплата денег](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B2%D1%8B%D0%BF%D0%BB%D0%B0%D1%82%D0%B0-%D0%B4%D0%B5%D0%BD%D0%B5%D0%B3-%D0%B2%D1%8B%D0%BF%D0%BB%D0%B0%D1%82%D1%8B-%D0%B4%D0%B5%D0%BD%D0%B5%D0%B3-get)                 |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Возврат покупателя](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B2%D0%BE%D0%B7%D0%B2%D1%80%D0%B0%D1%82-%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%B0%D1%82%D0%B5%D0%BB%D1%8F-%D0%B2%D0%BE%D0%B7%D0%B2%D1%80%D0%B0%D1%82%D1%8B-%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%B0%D1%82%D0%B5%D0%BB%D0%B5%D0%B9-get)            |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Возврат поставщику](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B2%D0%BE%D0%B7%D0%B2%D1%80%D0%B0%D1%82-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA%D1%83-%D0%B2%D0%BE%D0%B7%D0%B2%D1%80%D0%B0%D1%82%D1%8B-%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D1%89%D0%B8%D0%BA%D0%B0%D0%BC-get)            |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Счет-фактура выданный](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%81%D1%87%D0%B5%D1%82-%D1%84%D0%B0%D0%BA%D1%82%D1%83%D1%80%D0%B0-%D0%B2%D1%8B%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9-%D1%81%D1%87%D0%B5%D1%82%D0%B0-%D1%84%D0%B0%D0%BA%D1%82%D1%83%D1%80%D1%8B-%D0%B2%D1%8B%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5-get)         |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Счет-фактура полученный](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%81%D1%87%D0%B5%D1%82-%D1%84%D0%B0%D0%BA%D1%82%D1%83%D1%80%D0%B0-%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%BD%D1%8B%D0%B9-%D1%81%D1%87%D0%B5%D1%82%D0%B0-%D1%84%D0%B0%D0%BA%D1%82%D1%83%D1%80%D1%8B-%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5-get)       |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Инвентаризация](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B8%D0%BD%D0%B2%D0%B5%D0%BD%D1%82%D0%B0%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D0%B8%D0%BD%D0%B2%D0%B5%D0%BD%D1%82%D0%B0%D1%80%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-get)                |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Полученный отчет комиссионера](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%BD%D1%8B%D0%B9-%D0%BE%D1%82%D1%87%D1%91%D1%82-%D0%BA%D0%BE%D0%BC%D0%B8%D1%81%D1%81%D0%B8%D0%BE%D0%BD%D0%B5%D1%80%D0%B0-%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5-%D0%BE%D1%82%D1%87%D1%91%D1%82%D1%8B-%D0%BA%D0%BE%D0%BC%D0%B8%D1%81%D1%81%D0%B8%D0%BE%D0%BD%D0%B5%D1%80%D0%B0-get) |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `incomingDate`                                       |
| [Выданный отчет комиссионера](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B2%D1%8B%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9-%D0%BE%D1%82%D1%87%D1%91%D1%82-%D0%BA%D0%BE%D0%BC%D0%B8%D1%81%D1%81%D0%B8%D0%BE%D0%BD%D0%B5%D1%80%D0%B0-%D0%B2%D1%8B%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D0%B5-%D0%BE%D1%82%D1%87%D1%91%D1%82%D1%8B-%D0%BA%D0%BE%D0%BC%D0%B8%D1%81%D1%81%D0%B8%D0%BE%D0%BD%D0%B5%D1%80%D0%B0-get)   |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Прайс-лист](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%BF%D1%80%D0%B0%D0%B9%D1%81-%D0%BB%D0%B8%D1%81%D1%82-%D0%BF%D1%80%D0%B0%D0%B9%D1%81-%D0%BB%D0%B8%D1%81%D1%82%D1%8B-get)                    |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`                                                     |
| [Тех. карта](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%82%D0%B5%D1%85.-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D1%82%D0%B5%D1%85.-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-get)                     |`id`, `accountId`, `shared`, `version`, `updated`, `updatedBy`, `deleted`, `name`, `description`, `code`, `externalCode`                                                                                                              |
| [Заказ на производство](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7-%D0%BD%D0%B0-%D0%BF%D1%80%D0%BE%D0%B8%D0%B7%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7%D1%8B-%D0%BD%D0%B0-%D0%BF%D1%80%D0%BE%D0%B8%D0%B7%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-get)         |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `deliveryPlannedMoment`, `quantity`                    |
| [Тех. операция](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D1%82%D0%B5%D1%85.-%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D1%8F-%D1%82%D0%B5%D1%85.-%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D0%B8-get)                 |`id`,  `accountId`, `shared`, `version`, `updated`,  `updatedBy`, `deleted`, `name`, `description`, `code`,  `externalCode`,  `syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `quantity`                                           |
| [Внутренний заказ](https://online.moysklad.ru/api/remap/1.1/doc/index.html#%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82-%D0%B2%D0%BD%D1%83%D1%82%D1%80%D0%B5%D0%BD%D0%BD%D0%B8%D0%B9-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7-%D0%B2%D0%BD%D1%83%D1%82%D1%80%D0%B5%D0%BD%D0%BD%D0%B8%D0%B5-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7%D1%8B-get)              |`id`,`accountId`, `shared`, `version`, `updated`,`updatedBy`, `deleted`, `name`, `description`, `code`,`externalCode`,`syncId`, `moment`, `applicable`, `sum`, `isDeleted`, `created`, `quantity`                                               |

## Как использовать сортировку через JSON API
Для применения сортировки к коллекции необходимо добавить в запрос `order=[field name],[asc/desc]`, где field name - имя поля для сортировки. Опционально через запятую можно указать направление сортировки:
* `asc` - по возрастанию, значение по умолчанию,
* `desc` - по убыванию.
Например, для сортировки поля `name` по возрастанию нужно использовать `?order=name, asc` или `?order=name`, а по убыванию `?order=name,desc`.

Сортировка также доступна одновременно для нескольких полей, поля для сортировки необходимо указывать через разделитель `;`. Например, `?order=name=asc;code=desc`.

Рассмотрим применение сортировки.
Предварительно создадим товары с наименованиями `Pencil`, `Pencil Blue`, `Pencil Red`, `Pencil 123`, `Карандаш 123`, `Карандаш зеленый`, `Карандаш желтый`, `Карандаш`, `12345`, `!!! Это карандаш`.
```shell
curl -X POST \
  http://localhost/api/remap/1.1/entity/product \
  -H 'Authorization: Basic token=' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -d '[
   {
      "name":"12345",
      "weight":0.1,
      "weighed":true,
      "syncId":"8b7c97cf-cf77-4f7e-b200-d264125578ab"
   },
   {
      "name":"Pencil",
      "weight":0.01,
      "syncId":"5b7c97cf-cf77-4f7e-b200-d264125578ab"
   },
   {
      "name":"Pencil 123",
      "weight":0.01,
      "syncId":"3b7c97cf-cf77-4f7e-b200-d264125578ab"
   },
   {
      "name":"Pencil Blue",
      "weight":0.11,
      "weighed":true
   },
   {
      "name":"Pencil Red",
      "weight":0.2,
      "syncId":"1b7c97cf-cf77-4f7e-b200-d264125578ab"
   },
   {
      "name":"Карандаш",
      "weight":0.1,
      "syncId":"2b7c97cf-cf77-4f7e-b200-d264125578ab"
   },
   {
      "name":"Карандаш 123",
      "weight":0.32,
      "syncId":"4b7c97cf-cf77-4f7e-b200-d264125578ab"
   },
   {
      "name":"Карандаш желтый",
      "weight":0.12,
      "weighed":true,
      "syncId":"7b7c97cf-cf77-4f7e-b200-d264125578ab"
   },
   {
      "name":"Карандаш зеленый",
      "weight":0.4,
      "syncId":"8c7c97cf-cf77-4f7e-b200-d264125578ab"
   },
   {
      "name":"!!! Это карандаш",
      "weight":0.1,
      "syncId":"3d7c97cf-cf77-4f7e-b200-d264125578ab"
   }
]'
```

Чтобы получить коллекцию товаров, отстортированных по имени, необходимо указать поле `name` и направление сортировки, как в примере ниже
```shell
curl -X GET \
  'https://online.moysklad.ru/api/remap/1.1/entity/product?order=name' \
  -H 'Authorization: Basic token==' \
  -H 'Cache-Control: no-cache'
```
Ответ будет содержать следующий порядок по возрастанию:

|name|
|------------------|
| 12345 |
| Pencil |
| Pencil 123 |
| Pencil Blue |
| Pencil Red |
| Карандаш |
| Карандаш 123 |
| Карандаш желтый |
| Карандаш зеленый |
| !!! Это карандаш |

Изменим направление сортировки
```shell
curl -X GET \
  'https://online.moysklad.ru/api/remap/1.1/entity/product?order=name,desc' \
  -H 'Authorization: Basic token==' \
  -H 'Cache-Control: no-cache'
```

|name|
|------------------|
| !!! Это карандаш |
| Карандаш зеленый |
| Карандаш желтый |
| Карандаш 123 |
| Карандаш |
| Pencil Red |
| Pencil Blue |
| Pencil 123 |
| Pencil |
| 12345 |

Попробуем отсортировать товары одновременно по убыванию логического поля `weighed` и по возрастанию поля `name`.
```shell
curl -X GET \
  'https://online.moysklad.ru/api/remap/1.1/entity/product?order=weighed,desc;name' \
  -H 'Authorization: Basic token=' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json'
```

|weighed|name|
|------------------|------------------|
| true | 12345 |
| true | Pencil Blue |
| true | Карандаш желтый |
| false | Pencil |
| false | Pencil 123 |
| false | Pencil Red |
| false | Карандаш |
| false | Карандаш 123 |
| false | Карандаш зеленый |
| false | !!! Это карандаш |

Добавим еще сортировку по числовому полю `weight`.
```shell
curl -X GET \
  'https://online.moysklad.ru/api/remap/1.1/entity/product?order=weighed,desc;weight,desc;name' \
  -H 'Authorization: Basic token=' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json'
```

|weighed|weight|name|
|------------------|------------------|------------------|
|true|0.12| Карандаш желтый |
|true|0.11| Pencil Blue |
|true|0.1| 12345 |
|false|0.4| Карандаш зеленый |
|false|0.32| Карандаш 123 |
|false|0.2| Pencil Red |
|false|0.1| Карандаш |
|false|0.1| !!! Это карандаш |
|false|0.01| Pencil |
|false|0.01| Pencil 123 |

Кроме текстовых, числовых и логических полей доступна сортировка по полям типов uuid и дата-время.
Например, применим сортировку по полю `syncId`.
```shell
curl -X GET \
  'https://online.moysklad.ru/api/remap/1.1/entity/product?order=syncId' \
  -H 'Authorization: Basic token=' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json'
```

|syncId|name|
|------------------|------------------|
| 1b7c97cf-cf77-4f7e-b200-d264125578ab|Pencil Red |
| 2b7c97cf-cf77-4f7e-b200-d264125578ab|Карандаш |
| 3b7c97cf-cf77-4f7e-b200-d264125578ab|Pencil 123 |
| 3d7c97cf-cf77-4f7e-b200-d264125578ab|!!! Это карандаш |
| 4b7c97cf-cf77-4f7e-b200-d264125578ab|Карандаш 123 |
| 5b7c97cf-cf77-4f7e-b200-d264125578ab|Pencil |
| 7b7c97cf-cf77-4f7e-b200-d264125578ab|Карандаш желтый |
| 8b7c97cf-cf77-4f7e-b200-d264125578ab|12345 |
| 8c7c97cf-cf77-4f7e-b200-d264125578ab|Карандаш зеленый |
| null |Pencil Blue |

У товара `Pencil Blue` отсутствует значение поля `syncId`, поэтому при сортировке по возрастанию, оно выводится в конце. Аналогичное поведение и для других полей со значением `null`.
