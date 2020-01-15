---
title: Дескриптор приложения
tags: [api, vendor]
keywords:
summary:
sidebar: vendor_sidebar
permalink: /api/vendor/1.0/descriptor.html
folder: vendor
---

Дескриптор приложения представляет собой XML-структуру, которая описывает технические параметры встраивания/интеграции 
приложения вендора в МойСклад.

Дескриптор приложения должен соответствовать последней версии XSD схемы. Актуальной версией считается [1.1.0](https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.1.0.xsd).

Сейчас рассмотрим дескриптор приложения на примерах.

### Содержимое дескриптора приложения

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.1.0.xsd">
    <iframe>
        <sourceUrl>https://example.com/iframe.html</sourceUrl>
        <expand>true</expand>
    </iframe>
    <vendorApi>
        <endpointBase>https://example.com/dummy-app</endpointBase>
    </vendorApi>
    <access>
        <resource>https://online.moysklad.ru/api/remap/1.2</resource>
        <scope>admin</scope>
    </access>
</application>
```

На текущий момент в дескрипторе приложения есть три блока: iframe, vendorApi, access. Порядок расположения этих блоков 
относительно друг друга в дескрипторе может быть произвольный.

|Блок|Назначение|Доступно для типов приложений|Требует наличия других блоков|
|----|----------|-----------------------------|-----------------------------|
|iframe|Описывает iframe-часть приложения.|iframe-приложения, серверные приложения|Не требует|
|vendorApi|Описывает взаимодействие по Vendor API.|телефония, серверные приложения|Не требует|
|access|Описывает требуемый доступ приложения к ресурсам пользовательского аккаунта.|серверные приложения|vendorApi|

#### Блок iframe

В теге **iframe/sourceUrl** указывается URL, по которому будет загружаться содержимое iframe внутри UI МоегоСклада. 
В URL допускается использование только протокола HTTPS.

В теге **iframe/expand** указывается **boolean** значение, которое отвечает, будет ли iframe расширяться в основном приложении 
МоегоСклада. Под расширением подразумевается автоматическое масштабирование **iframe** элемента в зависимости от контента.
Причем, данный элемент является опциональным со значением `false` по умолчанию. Чтобы расширение iframe работало верно, 
на стринице, которая указана в `sourceUrl` должен работать скрипт, который оповещает страницу МоегоСклада об изменении высоты 
его контента, то есть:

* Реализовать посылку сообщения “EventMessage” при любом изменении высоты контента, причем
    * сообщение послать parent окну
    * данные сообщения должны содержать свойство “height” - высоту содержимого, страницы которая сейчас отображается (в px)

Для удобства можно добавить следующий [js скрипт](https://online.moysklad.ru/js/ns/appstore/app/v1/moysklad-iframe-expand-1.js) 
на свою страницу.

Пример: 

```html
<!doctype html>
<html>

<head>
...
</head>

<body>
...
<script type="text/javascript" src="https://online.moysklad.ru/js/ns/appstore/app/v1/moysklad-iframe-expand-1.js"></script>
</body>

</html>
```

В случае отсутствия блока `iframe` в дескрипторе считается, что у приложения отсутствует iframe-часть.

#### Блок vendorApi

В теге vendorApi/endpointBase указывается базовый URL эндпоинта на стороне вендора, к которому будет обращаться 
МойСклад. В URL допускается использование только протокола HTTPS.

Для получения полного адреса конкретного эндпоинта Vendor API на стороне вендора к базовому URL’у добавляется суффикс 
/api/moysklad/vendor/1.0 и путь эндпоинта. То есть шаблон формирования полного URL ресурса в общем случае такой:

`{endpointBase}/api/moysklad/vendor/1.0/{endpointPath}/…`

Для эндпоинта активации/деактивации приложений на аккаунте шаблон следующий (endpointPath = apps):

`{endpointBase}/api/moysklad/vendor/1.0/apps/{appId}/{accountId}`

Например, если:

+ <endpointBase>https://example.com/dummy-app</endpointBase>
+ appId = 5f3c5489-6a17-48b7-9fe5-b2000eb807fe
+ accountId = f088b0a7-9490-4a57-b804-393163e7680f
+ endpointPath = apps

то полный URL ресурса на стороне вендора, к которому будет выполнять запросы МойСклад при активации (и деактивации) 
приложения на аккаунте будет следующим: 

`https://example.com/dummy-app/api/moysklad/vendor/1.0/apps/5f3c5489-6a17-48b7-9fe5-b2000eb807fe/f088b0a7-9490-4a57-b804-393163e7680f`
 
В случае отсутствия блока vendorApi в дескрипторе не выполняется активация и деактивация приложения на серверах вендора.

#### Блок access

В тегах access/resource (в перспективе их может быть несколько) указываются ресурсы, к которым приложению нужен доступ.
 В тегах access/scope (в перспективе их тоже может быть несколько) указывается требуемые разрешения/требуемый уровень 
 доступа. При наличии блока access должны присутствовать как минимум по одному тегу resource и scope.
 
Наличие блока access требует наличия блока vendorApi для передачи токена(ов) к ресурсам аккаунта при активации 
приложения по Vendor API.

В случае отсутствия этого блока в дескрипторе приложения при установке на аккаунт приложению не выдаются никакие доступы 
к ресурсам аккаунта.

На текущий момент для access/resource возможно только одно значение: **https://online.moysklad.ru/api/remap/1.2**

Для access/scope на текущий момент доступно тоже только одно значение: **admin**

Другими словами, на текущий момент блок access может иметь только такой вид:

```xml
<access>
    <resource>https://online.moysklad.ru/api/remap/1.2</resource>
    <scope>admin</scope>
</access>
```

### Примеры дескрипторов

#### Для iframe-приложений

Дескриптор для iframe-приложения:

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.1.0.xsd">
    <iframe>
        <sourceUrl>https://example.com/iframe.html</sourceUrl>
    </iframe>
</application>
```

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.1.0.xsd">
    <iframe>
        <sourceUrl>https://example.com/iframe.html</sourceUrl>
        <expand>true</expand>
    </iframe>
</application>
```


Можно добавить блок vendorApi (тогда будет выполняться активация и деактивация приложения по Vendor API):

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.1.0.xsd">
    <iframe>
        <sourceUrl>https://example.com/iframe.html</sourceUrl>
    </iframe>
    <vendorApi>
        <endpointBase>https://example.com/dummy-app</endpointBase>
    </vendorApi>
</application>
```

#### Для серверных приложений

Минимальный дескриптор для серверных приложений (без возможности настройки параметров приложения пользователем 
МоегоСклада, так как у приложения отсутствует iframe-часть):

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.1.0.xsd">
    <vendorApi>
        <endpointBase>https://example.com/dummy-app</endpointBase>
    </vendorApi>
    <access>
        <resource>https://online.moysklad.ru/api/remap/1.2</resource>
        <scope>admin</scope>
    </access>
</application>
```

Полный дескриптор для серверных приложений (с iframe-частью):

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.1.0.xsd">
    <iframe>
        <sourceUrl>https://example.com/iframe.html</sourceUrl>
    </iframe>
    <vendorApi>
        <endpointBase>https://example.com/dummy-app</endpointBase>
    </vendorApi>
    <access>
        <resource>https://online.moysklad.ru/api/remap/1.2</resource>
        <scope>admin</scope>
    </access>
</application>
```

#### Для телефонии

Для приложений телефонии в минимальном варианте дескриптор не нужен.

Если вендору требуется получать оповещения по активации и деактивации приложений, тогда нужен дескриптор с блоком vendorApi:

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.1.0.xsd">
    <vendorApi>
        <endpointBase>https://example.com/dummy-app</endpointBase>
    </vendorApi>
</application>
```

#### Для систем лояльности

Для интеграций с системами лояльности дескриптор на текущий момент не требуется (не поддерживается).