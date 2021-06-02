# Правила написания CSS

## Синтаксис

1. Селекторы, объявления и значения пиши строчными буквами:
```css
/* Плохо: */
.Selector {
  WIDTH: 50PX;
}

/* Хорошо: */
.selector {
  width: 50px;
}
```
<br>

2. Ставь пробел после селектора и до открывающей фигурной скобки. После открывающей фигурной скобки делай перенос строки. Закрывающую фигурную скобку пиши с новой строки и после неё оставляй пустую строку
```css
/* Плохо: */
.selector{width: 50px;}
.next-selector{width: 50px;}

/* Хорошо: */
.selector {
  width: 50px;
}

.next-selector {
  width: 50px;
}
```
<br>

3. Группируя селекторы пиши каждый на отдельной строке:
```css
/* Плохо: */
.selector, .yet-selector {
  width: 50px;
}

/* Хорошо: */
.selector,
.yet-selector {
  width: 50px;
}
```
<br>

4. Пиши каждое объявление свойства на новой строке:
```css
/* Плохо: */
.selector {
  width: 50%; padding: 0 15px;
}

/* Хорошо: */
.selector {
  width: 50%; 
  padding: 0 15px;
}
```
<br>

4. Ставь ```:``` сразу после объявления свойства. После ```:``` ставь один пробел:
```css
/* Плохо: */
.selector {
  width :50%;
}

/* Хорошо: */
.selector {
  width: 50%; 
}
```
<br>

5. Ставь ```;``` в конце каждого объявления:
```css
/* Плохо: */
.selector {
  width: 50%
}

/* Хорошо: */
.selector {
  width: 50%; 
}
```
<br>

6. Опускай единицы измерения для нулевых значений:
```css
/* Плохо: */
.selector {
  margin: 0px;
}

/* Хорошо: */
.selector {
  margin: 0;
}
```
<br>

7. Пиши пробел после запятой внутри таких значений как ```rgb()```, ```rgba()```, ```linear-gradient()``` и подобных:
```css
/* Плохо: */
.selector {
  background-color: rgba(0,0,0,.5);
  background-image: linear-gradient(45deg,#333,#333 50%,#eee 75%,#333 75%);
}

/* Хорошо: */
.selector {
  background-color: rgba(0, 0, 0, .5);
  background-image: linear-gradient(45deg, #333, #333 50%, #eee 75%, #333 75%);
}
```
<br>

8. Опускай ноль для дробных значений:
```css
/* Плохо: */
.selector {
  opacity: 0.5;
}

/* Хорошо: */
.selector {
  opacity: .5;
}
```
<br>

9. Hex значения пиши строчными буквами:
```css
/* Плохо: */
.selector {
  color: #3E3E3E;
}

/* Хорошо: */
.selector {
  color: #3e3e3e;
}
```
<br>

10. Сокращаю Hex значения по возможности:
```css
/* Плохо: */
.selector {
  color: #ffffff;
}

/* Хорошо: */
.selector {
  color: #fff;
}
```
<br>

11. Ставь пробелы до и после комбинаторов:
```css
/* Плохо: */
.prev+.next  {
  margin-top: 2em;
}

/* Хорошо: */
.prev + .next  {
  margin-top: 2em;
}
```
<br>

12. Пиши значения атрибутов в кавычках:
```css
/* Плохо: */
a[href^=http] {
  ...
}

/* Хорошо: */
a[href^="http"] {
  ...
}
```
<br>

13. Настрой редактор так, что бы отступы объфвлений формировались двумя символами пробела - размести файл [.editorconfig]() (универсальные настройки редактора) в папке проекта и установи его поддержку в редакторе.
Что бы VSCode научился работать с ```.editorconfig``` файлом - [установи плагин](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)