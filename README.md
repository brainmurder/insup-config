# Установка и настройка Insup

## Инструменты

  1. Установленный Ruby
  2. Установленный DevKit для Ruby
  3. Установленный gem Insup

## Установка для Windows

### Установка Ruby

Скачиваем установщик с http://rubyinstaller.org/downloads/.

### Установка DevKit
После установки, с той же страницы http://rubyinstaller.org/downloads/ скачиваем DEVELOPMENT KIT в зависимости от версии Ruby и разрядности вашей системы.

Запускаем скаченный файл и указываем путь установки, в пути установки указываем папку в которую установили Ruby.

После распаковки, в пуске находим и запускаем **Start Command Prompt with Ruby**, через команду "cd", находим папку в которую утановили Ruby и распаковали DevKit, после чего запускаем команду **ruby dk.rb init**.

```sh
cd c:\Ruby22-x64
ruby dk.rb init
```
В данной папке сгенерируется конфиг файл для установки DevKit - **config.yml**.

Открываем **config.yml** и вконце дописываем путь до папки с Ruby, обратите внимание на слеш и тире, например:

```ruby
- C:/Ruby22-x64
```
После в командной строке можем запустить команду **ruby dk.rb install**

```sh
ruby dk.rb install
```
### Установка Insup
После установки DevKit в командной строке запускаем:
```sh
gem install insup
```
## Настройка Insup

### Настройка конфигурационного файла

Скачиваем файл **.insup** и кладем его в папку в которой будем работать с темой, в файле есть обязательные поля:

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
```sh
cd c:\mysite
```

Далее запускаем команду:
```sh
insup insales download
```

Тема скачалась и теперь мы можем править её локально. Чтобы изменения сразу попадали на сервер в командной строке необходимо запустить две команды:

* chcp 65001 - это нужно, чтобы нормально обрабатывалась кодировка UTF8
* insup - эта команда включает сам insup
```sh
chcp 65001
insup
```

## Ссылки

* https://github.com/httplab/insup - Репозиторий Insup
* http://rubyinstaller.org/downloads/ - установщик Ruby для Windows
* https://github.com/oneclick/rubyinstaller/wiki/development-Kit - установка DevKit
 