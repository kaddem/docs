# html

## Синтаксис

1. Используй строчные буквы для тегов, атрибутов и их значений:
```html
<!-- Плохо: -->
<Img SRC="logo.svg" Width="50" height="50" alt="Company" Class="SOME-CLASS">

<!-- Хорошо: -->
<img src="logo.svg" width="50" height="50" alt="Company" class="some-class">
```
<br>

2. Пиши каждый вложенные HTML тег с новой строки и отступом относительно родительсткого.
Исключение - строчные теги (```span```, ```a```, ```strong```, ```em```, ```del```, ```ins``` и т.п.). Их можешь не переносить.
```html
<!-- Плохо: -->
  <nav>
<ul>
<li><a href="/index.html">Главная</a></li>
<li><a href="/contacts.html">Контакты</a></li>
</ul>
</nav>

<!-- Хорошо: -->
<nav>
  <ul>
    <li><a href="/index.html">Главная</a></li>
    <li><a href="/contacts.html">Контакты</a></li>
  </ul>
</nav>
```
<br>


3. Настрой редактор так, что бы отступы вложенных тегов формировались двумя символами пробела - размести файл [.editorconfig]() (универсальные настройки редактора) в папке проекта и установи его поддержку в редакторе.
Что бы VSCode научился работать с ```.editorconfig``` файлом - [установи плагин](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)
<br><br>

4. Значения атрибутов пиши в двойных кавычках:
```html
<!-- Плохо: -->
<img src='logo.svg' width='50' height='50' alt='Company X logo'>

<!-- Хорошо: -->
<img src="logo.svg" width="50" height="50" alt="Company X logo">
```
<br>

5. Опускай слэш ```/``` у одиночных тегов:
```html
<!-- Плохо: -->
<br />

<!-- Хорошо: -->
<br>
```
<br>

6. Всегда пиши "необязательные" закрывающие теги, такие как  ```</li>``` или ```</body>```:
```html
<!-- Плохо: -->
<ul>
  <li>item 1
  <li>item 2
</ul>

<!-- Хорошо: -->
<ul>
  <li>item 1</li>
  <li>item 2</li>
</ul>
```

## Базовая разметка

1. Пиши ```<!DOCTYPE html>```
2. Указывай нужный язык в атрибуте ```lang``` тега ```<html>```
3. Указывай кодироку документа как - ```utf-8```
```html
<!-- Плохо: -->
<html>
<head>
  <title>Контакты</title>
</head>
<body>
  
</body>
</html>

<!-- Хорошо: -->
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Контакты</title>
</head>
<body>
  
</body>
</html>
```

4. Дай пользователю самому принимать решение - приблизить ему сайт на мобильном устройстве или нет. Не используй ```user-scalable=no```, ```minimum-scale=1.0```, ```maximum-scale=1.0```. Тем более Safari на iOS игнорирует эти директивы ;)
```html
<!-- Плохо: -->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no ,minimum-scale=1.0, maximum-scale=1.0">
  <title>Контакты</title>
</head>

<!-- Хорошо: -->
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Контакты</title>
</head>
```