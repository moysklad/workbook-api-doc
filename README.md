[![Build Status](https://travis-ci.org/moysklad/workbook-api-doc.svg?branch=master)](https://travis-ci.org/moysklad/workbook-api-doc)

# Workbook API МойСклад
https://moysklad.github.io/

## Установка Jekyll локально
В директории проекта запустить Docker контейнер
```
docker-compose up server
```
Сайт будет доступен по http://0.0.0.0:4000/

Для корректной навигации необходимо закомментировать следующую строку в `_config.yml`:
```javascript
url: https://dev.moysklad.ru
```

## Внутренние ссылки

В сайдбарах и статьях ссылки нужно указывать относительно корня, например, `/workbook/api/remap/1.1/ru/index.html`. permalink для статей нужно задавать относитльено `/workbook/`, например, `permalink: /api/remap/1.1/ru/meta.html`.

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
