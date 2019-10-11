[![Build Status](https://travis-ci.org/moysklad/workbook-api-doc.svg?branch=master)](https://travis-ci.org/moysklad/workbook-api-doc)

# Workbook API МойСклад
https://moysklad.github.io/

## Установка Jekyll локально
В директории проекта запустить Docker контейнер
```
docker-compose up server
```
Сайт будет доступен по http://0.0.0.0:4000/

## Внутренние ссылки

Внутренние ссылки задаются относительно корня. Для локальной сборки это `http://0.0.0.0:4000`, а для прода - `https://dev.moysklad.ru/workbook`. Для этого во всех скриптах и ссылках используется переменная **site.url**, которая определена в [файле конфига](_config.yml).

В сайдбарах и permalink для статей нужно задавать ссылки относитльено `/workbook/`, например, `permalink: /api/remap/1.1/ru/some.html`.

При использвании внутренних ссылок в статье, используем **site.url**:

+ `[Текст ссылки]({{ site.url }}/api/remap/1.1/ru/some.html)`.

В страницах шаблонов и скриптах также используем **site.url**:

+ `<link rel="stylesheet" href="{{site.url}}/css/customstyles.css">`
+ `<atom:link href="{{ "/feed.xml" | prepend: site.url }}" rel="self" type="application/rss+xml"/>`

## Инструкция по добавлению новых тэгов
1\. Добавить новый тэг в выбранный md-файл в разделе `tags`. Тэги не должны содержать пробелов, разделяются между собой запятыми.
```
tags: [getting_started, api]
```

2\. Новый тэг необходимо добавить в список поддерживаемых тэгов - `/_data/tags.yml`

3\. Для корректной работы отображения списка статей с новым тэгом необходимо для тэга сформировать свой md-файл в папке `/pages/tags`. Название файла должно строиться по маске `tag_tagname.md`

4\. Содержимое файла `tag_tagname.md` :
```
    ---
    title: "Заголовок"
    tagName: tagname
    search: exclude
    permalink: tag_tagname.html
    sidebar: mydoc_sidebar
    folder: tags
    ---
    {% include taglogic.html %}

    {% include links.html %}
```
