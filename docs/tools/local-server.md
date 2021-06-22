# Локальный сервер на macOS

>Мы тут поднимаем и настраиваем локальный сервер для работы с PHP и MySQL.
>Просьба MERNутым стразу проходить мимо (с уважением... к PHP... да и вообще ко всем технологиям и тем кто их использует)

Есть два варианта поднять локальный сервер на mac:

1. Установить сторонний готовый серверный пакет
2. Использовать встроенный сервер ```Apache```

Первый вариант в топку - смысл ставить что-то стороннее, если есть встроенное в систему. О втором варианте ниже.

## Запуск ```Apache```

1. Выполни в терминале команду:
```bash
sudo apachectl start
# не забудь ввести пароль - тот что для входа при старте компа.
# юзаешь отпечаток пальца - придется вспомнить пароль
```
> не знаешь что такое `sudo` или `apachectl`? Не тупи \- иди гугли! Разберешься \- вертай сюда назад.
> Не знаешь что такое `start` \- купи [словарь](https://www.ozon.ru/context/detail/id/5817303/)

2. Введи пароль, который юзаешь для входа в систему. Когда будешь вводить в консоли ничего не измениться, как будто строка пустая и каретка не двигается \- это норма при вводе пароля! Ввел \- не забудь Enter жмакнуть.

3. Проверь, что сервак стартанул. Иди в браузер, вводи url `http://localhost`. Должно быть так:
![Запущенный сервер Apache](../../images/apache-working.png)
> Файлы localhost'а лежат в директории `/Library/WebServer/Documents`.

Да, сервер должен стартовать сам при запуске компа - проверь это.

<br>

## Установка PHP

Дежавю. PHP уже есть в системе. Включи его поддержку, отредактировав файл конфигурации Apache ```/etc/apache2/httpd.conf```:

1. Откройте данный файл любым доступным способом в редакторе кода. Но в терминале удобнее:
```bash
sudo subl /etc/apache2/httpd.conf
```
> Я н___я не умею пользоваться консольными редакторами (```nano/vim```) и настроил символьную ссылку для открытия файлов в Sublime Text 3 из консоли, отсюда в команде выше видишь ```subl```.
> [Вот тут](https://panjeh.medium.com/open-sublime-text-3-from-terminal-in-macos-linux-837d3eea3156) хороший человек пишет как это сделать.

2. Раскомментируй строку, отвечающую за загрузку модуля *php7_module* `LoadModule php7_module libexec/apache2/libphp7.so`, удалив перед строкой символ #:
![Включаем PHP в httpd.conf](../../images/local-conf.png)
    
3. Так же раскомментируй строку:
```bash
LoadModule rewrite_module libexec/apache2/mod_rewrite.so
```

4. Сохрани файл.
    
5. Конфигурация сервака изменилась. Что бы изменения применились, перезапусти сервак:
```bash
sudo apachectl restart
```

<br>

## Решение проблем с правами доступа

В macOS куча системных/технических пользователей/ролей о которых обычный юзер не знает - это сделано для безопасности системы. Например, сервер Apache будет вносить изменения на диске от имени пользователя ```_www```. Но у него нет прав на запись в папке ```/Users/your-user-name```. Нам такой доступ потребуется. Для этого:


1. Все в том же файле ```/etc/apache2/httpd.conf``` найди и закомментируй строки поставив ```#``` перед ними:
```bash
# User _www
# Group _www
```

2. Сразу под ними напиши еще две строки:
```bash
User username # Где username - имя твоего пользователя в системе
Group staff
```

4. Сохрани файл.
    
5. Перезапусти сервак:
```bash
sudo apachectl restart
```

Теперь апач будет вносить изменения от твоего имени. И не нужно будет возиться с правами доступа к директориям.

<br>

## Настройка виртуальных хостов

### Редактируем httpd.conf

1. Открой файл конфигурации Apache ```/etc/apache2/httpd.conf``` в редакторе, например так:
```bash
sudo subl /etc/apache2/httpd.conf
```

2. Найди строку ```#Include /private/etc/apache2/extra/httpd-vhosts.conf``` и добавь под ней новую строку:
```bash
Include /private/etc/apache2/vhosts/*.conf
```

3. Созрани изменения и закрой файл.

Ты добавил директиву - Apache будет искать настройки для локально разрабатываемых сайтов в файлах с расширением .conf из директории ```/private/etc/apache2/vhosts```. Для каждого сайта - свой файл ```*.conf```

### Настройка виртуального хоста по умолчанию

1. Создай директорию ```/private/etc/apache2/vhosts``` -  ты добавил путь до нее выше, но физически такой папки нет. Исправь это:
```bash
sudo mkdir /private/etc/apache2/vhosts
```

2. Перейди в эту директорию:
```bash
cd /private/etc/apache2/vhosts/
```

3. Создай файл ```_default.conf```:
```bash
sudo touch _default.conf
```

4. Открой этот файл в редакторе:
```bash
sudo subl _default.conf
```

5. Пропиши в нем конфигурацию по умолчанию:
```text
<VirtualHost *:80>
DocumentRoot "/Library/WebServer/Documents"
</VirtualHost>
```

6. Созрани и закрой файл.

7. Перезапусти сервак:
```bash
sudo apachectl restart
```

8. Открой в браузере url `http://localhost`. Если нет ошибок - все идет как надо.

<br>

### Настройка хоста для сайта

> Инструкцию из этого раздела придется выполнять каждый раз при старте разработки бекенда для очередного нового сайта.

Договоримся, что директории для локально разрабатываемых сайтов будем размещать в директории sites домашней папки (твоя папка пользователя) - ```Users/your-user-name/sites```

Для примера создай сайт, который ты будешь открывать по домену ```test-site.local```:

1. Перейди в папку ```/private/etc/apache2/vhosts/```:
```bash
cd /private/etc/apache2/vhosts/
```

2. Создай файл ```test-site.local.conf```:
```bash
sudo touch test-site.local.conf
```

3. Открой его в редакторе:
```bash
sudo subl test-site.local.conf
```

4. Введи в файле:
```bash
<VirtualHost *:80>
	DocumentRoot "/Users/your-user-folder/sites/test-site"
	ServerName test-site.local
	ErrorLog "/private/var/log/apache2/test-site.local-error_log"
	CustomLog "/private/var/log/apache2/test-site.local-access_log" common
	<Directory "/Users/your-user-folder/sites/test-site">
		AllowOverride All
		Require all granted
	</Directory>
</VirtualHost>

# где your-user-folder - имя папки твоего пользователя
# где test-site - название сайта
```