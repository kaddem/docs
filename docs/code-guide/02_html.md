# Правила написания HTML разметки

## Синтаксис

1. Используй строчные буквы для тегов, атрибутов и их значений:
```html
<!-- Плохо: -->
<Img SRC="logo.svg" Width="50" height="50" alt="Company" Class="SOME-CLASS">

<!-- Хорошо: -->
<img src="logo.svg" width="50" height="50" alt="Company" class="some-class">
```
<br>

2. Пиши вложенные HTML теги с новой строки и отступом относительно родительстких.
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


3. Настрой редактор так, что бы отступы вложенных тегов формировались двумя символами пробела - размести файл [.editorconfig](https://github.com/kaddem/docs/blob/master/.editorconfig) (универсальные настройки редактора) в папке проекта и установи его поддержку в редакторе.
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
<br>
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
<br>

4. Дай пользователю самому принимать решение - приблизить ему сайт на мобильном устройстве или нет. Не используй ```user-scalable=no```, ```minimum-scale=1.0```, ```maximum-scale=1.0```.
```html
<!-- Плохо: -->
<head lang="ru">
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no ,minimum-scale=1.0, maximum-scale=1.0">
  <title>Контакты</title>
</head>

<!-- Хорошо: -->
<head lang="ru">
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Code Guide</title>
</head>
```
<br>

5. Поддерживай порядок в ```head```. Вначале пиши ```meta``` теги, потом ```title``` и далее теги ```link```:
```html
<!-- Плохо: -->
<head lang="ru">
  <meta charset="UTF-8">
  <link rel="stylesheet" href="plugin.css">
  <title>Code Guide</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="style.css">
  <meta name="description" content="Правила написания HTML разметки">
</head>

<!-- Хорошо: -->
<head lang="ru">
  <meta charset="UTF-8">
  <meta name="description" content="Правила написания HTML разметки">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Контакты</title>
  <link rel="stylesheet" href="plugin.css">
  <link rel="stylesheet" href="style.css">
</head>
```
<br>
## Подключение CSS
1. Опускай атрибут ```type```:
```html
<!-- Плохо: -->
<link rel="stylesheet" type="text/css" href="style.css">

<!-- Хорошо: -->
<link rel="stylesheet" href="style.css">
```
[О ```type``` на MDN](https://developer.mozilla.org/ru/docs/Web/HTML/Element/link#attr-type)
<br><br>

2. Подключай css в теге ```head``` после ```title```:
```html
<!-- Плохо: -->
<head lang="ru">
  <link rel="stylesheet" href="style.css">
  <title>Code Guide</title>
</head>

<!-- Плохо: -->
<head lang="ru">
  <title>Code Guide</title>
</head>
<body>
  <link rel="stylesheet" href="style.css">

  <!-- Тут разметка HTML страницы -->
</body>

<!-- Хорошо: -->
<head lang="ru">
  <title>Контакты</title>
  <link rel="stylesheet" href="style.css">
</head>
```
<br>

## Подключение JS
1. Опускай атрибут ```type```:
```html
<!-- Плохо: -->
<script src="script.js" type="text/javascript"></script>

<!-- Хорошо: -->
<script src="script.js"></script>
```
<br>

2. Подключай js перед закрывающим тегом ```</body>```:
```html
<!-- Плохо: -->
<head lang="ru">
  <title>Code Guide</title>
  <script src="script.js"></script>
</head>

<!-- Плохо: -->
<body>
  <script src="script.js"></script>

  <!-- Тут разметка HTML страницы -->
</body>

<!-- Хорошо: -->
<body>
  <!-- Тут разметка HTML страницы -->

  <script src="script.js"></script>
</body>
```
<br>
