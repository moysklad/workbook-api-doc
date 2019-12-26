---
title: Технические детали
tags: [api, vendor]
keywords:
summary:
sidebar: vendor_sidebar
permalink: /api/vendor/1.0/technical.html
folder: vendor
---
## Дескриптор приложения

Дескриптор приложения представляет собой XML-структуру, которая описывает технические параметры встраивания/интеграции 
приложения вендора в МойСклад.

В будущем мы предоставим формальную XML Schema (XSD) дескриптора приложения (см. здесь Дескриптор приложения). 
Сейчас рассмотрим дескриптор приложения на примерах.

### Содержимое дескриптора приложения

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.0.0.xsd">
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

На текущий момент в дескрипторе приложения есть три блока: iframe, vendorApi, access. Порядок расположения этих блоков 
относительно друг друга в дескрипторе может быть произвольный.

|Блок|Назначение|Доступно для типов приложений|Требует наличия других блоков|
|----|----------|-----------------------------|-----------------------------|
|iframe|Описывает iframe-часть приложения.|iframe-приложения, серверные приложения|Не требует|
|vendorApi|Описывает взаимодействие по Vendor API.|телефония, серверные приложения|Не требует|
|access|Описывает требуемый доступ приложения к ресурсам пользовательского аккаунта.|серверные приложения|vendorApi|

#### Блок iframe

В теге iframe/sourceUrl указывается URL, по которому будет загружаться содержимое iframe внутри UI МоегоСклада. 
В URL допускается использование только протокола HTTPS  (за исключением одного случая - для localhost допускается 
использование HTTP).

В случае отсутствия этого блока в дескрипторе считается, что у приложения отсутствует iframe-часть.

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
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.0.0.xsd">
    <iframe>
        <sourceUrl>https://example.com/iframe.html</sourceUrl>
    </iframe>
</application>
```

Можно добавить блок vendorApi (тогда будет выполняться активация и деактивация приложения по Vendor API):

```xml
<application xmlns="https://online.moysklad.ru/xml/ns/appstore/app/v1"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"                                  
      xsi:schemaLocation="https://online.moysklad.ru/xml/ns/appstore/app/v1 https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.0.0.xsd">
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
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.0.0.xsd">
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
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.0.0.xsd">
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
      https://online.moysklad.ru/xml/ns/appstore/app/v1/application-1.0.0.xsd">
    <vendorApi>
        <endpointBase>https://example.com/dummy-app</endpointBase>
    </vendorApi>
</application>
```

#### Для систем лояльности

Для интеграций с системами лояльности дескриптор на текущий момент не требуется (не поддерживается).

## Доступ по токену к JSON API 1.2

Токен для доступа к JSON API 1.2 передается вендору при активации приложения через Vendor API. Время жизни токена не ограничено.

Токен аннулируется при отключении приложения пользователем. На момент деактивации приложения через Vendor API токен уже нерабочий (аннулирован).

Токен при доступе к JSON API 1.2 следует передавать как [Bearer-токен](https://tools.ietf.org/html/rfc6750#section-2.1),
 а именно в виде заголовка HTTP-запроса:
 
 ```text
Authorization: Bearer <access_token>
 ```

Пример:

```text
Authorization: Bearer 6ab89be1ae6ff147755625ee8da948e42612233b
```

### Диаграмма последовательности предоставления доступа при подключении приложения

![useful image]({{site.url}}/images/vendor/diag_install.png)

### Диаграмма последовательности отзыва доступа при отключении приложения

![useful image]({{site.url}}/images/vendor/diag_install.png)


## Vendor API

Vendor API предназначено для взаимодействия Маркетплейса с системами вендоров касательно процессов, происходящих в 
рамках функционирования Маркетплейса.

На текущий момент Vendor API включает в себя следующие функции:

+ Активацию и деактивацию приложений на аккаунте
+ Получение контекста пользователя для iframe-приложений

Подробную справочную информацию по Vendor API можно посмотреть здесь [Vendor API](https://dev.moysklad.ru/doc/api/vendor/1.0/).

### Активация приложения на аккаунте

В общем виде процесс активации приложения выглядит так:

1. Пользователь МоегоСклада нажимает кнопку “Установить” приложение.
2. Маркетплейс делает HTTP PUT запрос на сервер вендора, в том числе передавая и токен доступа к JSON API (если в 
дескрипторе приложения таковой доступ запрашивается). При этом доступ по переданному токену уже работает.
3. Сервер вендора, в рамках допустимого тайм-аута, отвечает на запрос одним из статусов в теле ответа:
    + **Activating** - этот статус предназначен для асинхронной активации на стороне вендора (то есть если в рамках 
    допустимого тайм-аута обработки HTTP PUT запроса не получается активировать приложение - например, для активации 
    приложения требуется несколько минут). Далее вендор должен оповестить МойСклад через эндпоинт “Обратного вызова 
    изменения статуса приложения на аккаунте” о завершении активации приложения статусом **Activated** или о том, что 
    приложению требуется настройка статусом **SettingsRequired**.
    + **SettingsRequired** - таким статусом вендор сообщает МоемуСкладу, что приложению требуется настройка пользователем 
    (через iframe-часть приложения). После того, как пользователь настроит приложение, вендор должен оповестить 
    МойСклад через эндпоинт “Обратного вызова изменения статуса приложения на аккаунте” об активации приложения, 
    передав статус **Activated**.
    + **Activated** - этот статус означает, что приложение сразу полностью активировано и уже заработало.

#### Диаграмма деятельности активации приложения

![useful image]({{site.url}}/images/vendor/diag_activate.png)

### Деактивация приложения на аккаунте

Процесс деактивации приложения существенно проще процесса активации:

1. Пользователь МоегоСклада нажимает кнопку “Отключить” приложение.
2. Маркетплейс аннулирует доступ по токену (если таковой был выдан) и выполняет HTTP DELETE запрос к серверу вендора. 
То есть на момент получения вендором оповещения по деактивации доступ по токену уже не работает.

#### Диаграмма деятельности деактивации приложения

![useful image]({{site.url}}/images/vendor/diag_deactivate.png)

### Получение контекста пользователя для iframe-приложений

Функция доступна для iframe-приложений и серверных приложений с iframe-частью. 

Идея здесь в том, чтобы при загрузке iframe-части приложения в UI МоегоСклада вендор мог
 получить контекст текущего пользователя МоегоСклада (который открыл вкладку с iframe’ом приложения).

Работает это следующим образом:

1. При загрузке iframe МойСклад генерирует одноразовый ключ и добавляет его GET-параметром contextKey в URL, 
по которому загружается содержимое iframe. Например, если _<sourceUrl>https://example.com?aaa=123</sourceUrl>_, то 
URL загрузки iframe будет такого вида:
    https://example.com?aaa=123&contextKey=6S3BQLsaSRNdEnhPCoW9lplY2LozRUOq6S3BQLsaSRNdEnhPCoW9lplY2LozRUOq
2. В рамках Vendor API на стороне МоегоСклада есть специальный эндпоинт 
https://online.moysklad.ru/api/vendor/1.0/context/{contextKey}, обращаясь к которому (запросом POST) сервер вендора 
обменивает одноразовый ключ на контекст пользователя, который загрузил iframe-приложение.
Контекст пользователя возвращается в таком же виде как для ресурса 
[https://online.moysklad.ru/api/remap/1.2/context/employee](https://online.moysklad.ru/api/remap/1.2/context/employee) 
(контекста сотрудника в JSON API 1.2 ).

Воспользоваться ключом можно только один раз, после чего он сразу инвалидируется. Если произошел сбой при попытке 
получения контекста пользователя по ключу и ключ стал не валидным - можно предложить пользователю перезагрузить 
iframe (в UI МоегоСклада есть кнопочка перезагрузки iframe’a приложения).

Время жизни одноразового ключа ограничено - порядка нескольких минут, по истечении которых ключ инвалидируется на 
стороне МоегоСклада. По истечении срока жизни ключа по нему не получится получить информацию о контексте 
пользователя МоегоСклада.

## Аутентификация взаимодействия по Vendor API

Все запросы от МоегоСклада к серверу вендора и в обратную сторону от сервера вендора к МоемуСкладу должны быть 
подписаны с использованием JWT (JSON Web Token) описанным ниже образом.

### Секретный ключ secretKey

Для построения/вычисления сигнатуры JWT используется секретный ключ secretKey.

Секретный ключ генерируется на стороне МоегоСклада и выдается вендору. На текущий момент это  будет выглядеть так:

1. Вендор передает МоемуСкладу дескриптор приложения.
2. Сотрудник МоегоСклада загружает в Маркетплейс дескриптор, генерирует secretKey и передает его вендору.
3. Если по какой-то причине вендор хочет перегенерировать secretKey, то он это делает тоже через взаимодействие с 
сотрудником МоегоСклада.

### Исходящие запросы МойСклад → Вендор

МойСклад подписывает свои запросы к REST-эндпоинтам вендора, передавая JWT-токен в заголовке HTTP-запроса следующим образом:

```text
Authorization: Bearer <token>
```

JWT-header всегда такой:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

JWT-payload включает в себя следующие поля:

```json
{
  "iat": 1516239022,
  "exp": 1516239322,
  "jti": "6S3BQLsaSRNdEnhPCoW9lplY2LozRUOq"
}
```

Описание полей JWT-payload:

|Поле|Описание|Предполагаемое использование вендором|
|---|---|---|
|iat|Время генерации токена в секундах от 1970-01-01T00:00:00Z UTC|На усмотрение вендора|
|exp|Время жизни/“протухания“ токена в секундах от 1970-01-01T00:00:00Z UTC - позволяет ограничить срок валидности токена (после указанного момента времени токен считается невалидным)|При получении JWT после времени, указанного в exp, следует отклонять запрос с ошибкой аутентификации |
|jti|Уникальный идентификатор токена - позволяет отслеживать одноразовость применения токена|При получении JWT с jti, который был уже получен ранее, следует отклонять запрос с ошибкой аутентификации|

Например, для приведенных выше примеров JWT-заголовка, пэйлоада и secretKey=1234567890abcdefQWERTYXYZ передаваемый 
HTTP-заголовок будет таким:

```text
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE1MTYyMzkwMjIsImV4cCI6MTUxNjIzOTMyMiwianRpIjoiNlMzQlFMc2FTUk5kRW5oUENvVzlscGxZMkxvelJVT3EifQ.jdFKi9zJiyE3z9-rC3Z4rBsGZXJbKm4FapRdUiLEFgc
```

### Входящие запросы Вендор → МойСклад

Вендор при выполнении REST запросов к МоемуСкладу по Vendor API также должен подписывать их токеном JWT, который также 
следует передавать в заголовке HTTP-запроса:

```text
Authorization: Bearer <token>
```

JWT-header может быть как с указанием поля typ:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

так и без поля typ:

```json
{
  "alg": "HS256"
}
```

Поле alg в JWT-заголовке всегда должно иметь значение HS256. Соответственно, JWT-сигнатура всегда должна генерироваться 
по алгоритму HMAC SHA-256 с использованием секретного ключа secretKey.

JWT-payload должен содержать следующие поля (все поля являются обязательными за исключением exp - это поле опциональное):

```json
{
  "sub": "dummyapp.example-vendor",
  "iat": 1516239022,
  "exp": 1516239322,
  "jti": "6S3BQLsaSRNdEnhPCoW9lplY2LozRUOq"
}
```

Описание полей JWT-payload:

|Поле|Обязательное|Описание|Обработка на стороне МоегоСклада|
|---|-------|--------|--------------------------|
|sub|да|appUid приложения|Используется для идентификации и авторизации приложения|
|iat|да|Время генерации токена в секундах от 1970-01-01T00:00:00Z UTC|Используется для ограничения допустимого времени жизни токена| 
|exp|нет|Время жизни/“протухания“ токена в секундах от 1970-01-01T00:00:00Z UTC (после какого момента токен считается невалидным)|Если данное поле присутствует, то оно также используется для проверки валидности токена по времени|
|jti|да|Уникальный идентификатор токена|Используется для проверки одноразовости использования токена|

В системе МоегоСклада есть ограничение на максимальное время жизни для JWT-токена (порядка нескольких минут) - 
назовем его maxTokenLifetime. При проверке/валидации на стороне МоегоСклада значение exp ограничивается максимальным 
временем жизни: если _(exp - iat)_ превышает maxTokenLifetime или поле exp отсутствует, то в качестве exp 
используется _iat + maxTokenLifetime_, то есть:

```text
effectiveExp = exp ? min(exp, iat + maxTokenLifetime) : iat + maxTokenLifetime
```

### Ошибки аутентификации и авторизации

Обработка ошибок аутентификации и авторизации на стороне МоегоСклада осуществляется аналогично тому 
как это сделано в JSON API 1.2:

[https://moysklad.github.io/api-remap-1.2-doc/api/remap/1.2/ru/#obrabotka-oshibok](https://moysklad.github.io/api-remap-1.2-doc/api/remap/1.2/ru/#obrabotka-oshibok)

То есть при возникновении ошибок возвращается аналогичный объект error и заголовки HTTP-ответа X-Lognex-Auth 
и X-Lognex-Auth-Message.


 