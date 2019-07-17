# Workbook API МойСклад 
https://moysklad.github.io/

## Установка Jekyll локально
В директории проекта запустить Docker контейнер
```
docker-compose up server
```
Сайт будет доступен по http://0.0.0.0:4000/

## Инструкция по добавлению новых тэгов
1\. Добавить новый тэг в выбранный md-файл в раздел `tags`. Тэги не должны содержать пробелов, разделяются между собой запятыми. 
```
tags: [getting_started, api]
```

2\. Новый тэг необходимо добавить в список поддерживаемых тэгов - `/_data/tags.yml`

3\. Для корректной работы отображения списка статей с новым тэгом, необходимо для тэга сформировать свой md-файл в папке `/pages/tags`. Название файла должно строиться по маске `tag_tagname.md`

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
