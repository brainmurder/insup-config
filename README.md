# Установка и настройка Insup для Windows

[Insup](https://github.com/httplab/insup) - иструмент для работы с темами платформы InSales.

## Необходимые интрументы для работы с Insup

  1. Установленный Ruby
  2. Установленный DevKit для Ruby
  3. Установленный gem Insup

## Установка инструментов 

### Установка Ruby

Скачиваем установщик с http://rubyinstaller.org/downloads/.

>При выборе папки для установки следует выбирать путь в котором не будут встречаться кириллические символы.

>Иначе будут возникать ошибки в работе скриптов.

### Установка DevKit
После установки Ruby, с той же страницы http://rubyinstaller.org/downloads/ скачиваем DEVELOPMENT KIT в зависимости от версии Ruby и разрядности вашей системы.

Запускаем скаченный файл и указываем путь установки, в пути установки указываем папку в которую установили Ruby.

После распаковки, в пуске находим и запускаем **Start Command Prompt with Ruby**, через команду "cd", находим папку в которую утановили Ruby и распаковали DevKit, после чего запускаем команду **ruby dk.rb init**.

```
cd c:\Ruby22-x64
ruby dk.rb init
```
В данной папке сгенерируется конфиг файл для установки DevKit - **config.yml**.

Открываем **config.yml** и вконце дописываем путь до папки с Ruby, обратите внимание на слеш и тире, например:

```ruby
- C:/Ruby22-x64
```
После в командной строке можем запустить команду **ruby dk.rb install**

```
ruby dk.rb install
```
### Установка Insup
После установки DevKit в командной строке запускаем:
```
gem install insup
```
## Настройка Insup

### Настройка конфигурационного файла

Скачиваем файл **.insup** и кладем его в папку в которой будем работать с темой.

>При выборе папки для работы с темой, следует выбирать путь в котором не будут встречаться кириллические символы.

>Иначе Insup выдаст ошибку.

В файле есть обязательные поля:

* subdomain
* api_key
* password
* theme_id


**api_key** и **password** необходимо сгенерировать в бэк-офисе: Приложения -> Разработчикам -> Создать новый ключ доступа

#### Заполняем поля
```ruby
insales:
  subdomain: shop.myinsales.ru
  api_key: 00000000000000000000
  password: 000000000000000000000
```

```ruby
uploader:
  class: insales
  theme_id: 000000
```

После того как файл конфигурации заполнен, мы можем скачать нашу тему через Insup.

Открываем **Start Command Prompt with Ruby** и через команду "cd", находим папку в которой мы сохранили **.insup**.

Например
```
cd c:\mysite
```

Далее запускаем команду:
```
insup insales download
```

Тема скачалась и теперь мы можем править её локально. Чтобы изменения сразу попадали на сервер в командной строке необходимо запустить две команды:

* chcp 65001 - это нужно, чтобы нормально обрабатывалась кодировка UTF8
* insup - эта команда включает сам insup
```
chcp 65001
insup
```
## Возможные проблемы

* При отслеживании изменений в файлах, Insup следит только за файлами которые находятся у вас локально, поправив файл в бэк-офисе, insup не скачает изменения в локальную версию. Если вы все же поправили файл при запущеном Insup, стоит обновить локальную версию. (Отключить Insup нажав ctrl+c, после чего запустить команду **insup insales download [-f] [-t theme-id]**. Флаг [-f] означает, что локальные файлы будут перезаписаны. Так же можно удалить в локальной теме все файлы кроме файла конфигурации, предварительно отключив Insup, чтоб избежать уаления файлов на сервере, а потом заново скачать тему через **insup insales download**).
* Insup не стабильно отправляет картинки и шрифты на сервер, картинки и шрифты желательно добавлять вручную в бэк-офисе (Подробнее https://github.com/httplab/insup/issues/13).
* Insup или DevKit могут не устанавливаться из-за некорректной версии DevKit, необходимо проверить для какой системы и какой версии Ruby вы скачали DevKit.
* Кирилические символы в пути к папке в которой лежит тема, могут стать проблемой при работе с Insup, избегайте подобных путей - C:\Users\Пользователь\Documents\Новый_шаблон.
* Перед запуском команды insup или insup listen обязательно запускайте команду **chcp 65001**, иначе кириллические символы будут испорчены в тех файлах, что вы поправили.
* Если в вашем проекте присутствуют файлы с расширением css.liquid или js.liquid, есть большая вероятность того, что при загрузке этих файлов на сервер или при загрузке темы с сервера, Insup сотрет содержимое файлов. Такие файлы желательно править в бэк-офисе.
* При работе с Insup будьте внимательны в написании кода на Liquid, при сохранении файла с ошибками в синтаксисе, Insup выдаст ошибку и прекратит отслеживание изменений.

## Ссылки

* [Репозиторий Insup](https://github.com/httplab/insup)
* [Установщик Ruby для Windows](http://rubyinstaller.org/downloads/) 
* [Установка DevKit](https://github.com/oneclick/rubyinstaller/wiki/development-Kit) 
 
