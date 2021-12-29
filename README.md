Snoop Project for Termux
========================

## Snoop Project один из самых перспективных OSINT-инструментов по поиску никнеймов.
- [X] This is the most powerful software taking into account the CIS location.  
• [English readme Snoop for Termux](https://github.com/snooppr/snoop/blob/snoop_termux/README.en.md "Please feel free to improve the translation of this page.")  

<p align="center">  
  <img src="https://raw.githubusercontent.com/snooppr/snoop/master/images/snoopandroid.png" />  
</p>  

Ваша жизнь Слайд-шоу? Спросите снуп.  
Snoop Project разработан без учета мнения АНБ и их приятелей, то есть доступен рядовому пользователю.  

## Самостоятельная сборка ПО из исходно кода  
**Snoop for Android/Demo**  
<p align="center">  
  <img src="https://raw.githubusercontent.com/snooppr/snoop/master/images/Snoop_termux.plugins.png" width="90%" />  
</p>  

**Self-build software from source**  
**Native Installation**  

Установить [Termux](https://f-droid.org/ru/packages/com.termux/ "Termux с F-Droid, на GP Termux больше не обновляется!")  
```
# ПРИМЕЧАНИЕ_1!: установка Snoop на Termux продолжительная по времени (минуты).
# ПРИМЕЧАНИЕ_2!: если у пользователя ошибки при $ 'pkg update', например из-за цензуры в стране,
# и/или из-за того, что Termux давно не обновлялся на устройстве пользователя,
# то удаление/установка Termux-приложения не поможет,
# т.к. после удаления старые репозитории остаются на устройстве пользователя, решение:
$ termux-change-repo 
# и выбрать получение обновлений (для всех репо) из другого зеркала-репозитория.

# Войти в домашнюю папку Termux (т.е. просто открыть Termux)
$ termux-setup-storage
$ pwd #/data/data/com.termux/files/home # дефолтный/домашний каталог

# Установить python3 и зависимости
$ apt update && pkg upgrade && pkg install python libcrypt libxml2 libxslt git
$ pip install --upgrade pip

# Клонировать репозиторий
$ git clone https://github.com/snooppr/snoop -b snoop_termux
# (если флешкa FAT (ни ext4), в таком случае,
# клонировать репозиторий только в домашнюю директорию Termux)

# Войти в рабочий каталог Snoop
$ cd ~/snoop
# Установить зависимости 'requirements'
$ python3 -m pip install -r requirements.txt

# Чтобы расширить вывод терминала в Termux (по умолчанию 2к строк отображение в CLI), например, 
# отображение всей БД опции '--list-all [1/2]'
# добавить строку 'terminal-transcript-rows=10000' в файл '~/.termux/termux.properties'
# (крайне полезная опция доступна в Termux v0.114+). 
# Перезапустить Termux.  

# Пользователь также может запустить snoop по команде 'snoop' из любого места в CLI, создав alias.  
$ printf "alias snoop='cd && cd snoop && python snoop.py'" >> .bashrc  

# Пользователь также может выполнить быструю проверку интересующего его сайта по БД,
# не используя опцию "--list-all", используя команду "snoopcheck"  
$ alias snoopcheck='cd && cd snoop && printf 2 | python snoop.py --list-all | grep -i' >> .bashrc  
# перезапустить Termux.  
```
<p align="center">  
  <img src="https://raw.githubusercontent.com/snooppr/snoop/master/images/snoop_alias.gif" width="40%" />  
</p>  


## Using
**English version — of Snoop see release (available old 'Snoop EN version').**
```
Справка

optional arguments:
  -h, --help            show this help message and exit

service arguments:
  --version, -V         About: вывод на печать версий:: OS; Snoop;
                        Python и Лицензии
  --list-all, -l        Вывести на печать детальную информацию о базе
                        данных Snoop
  --donate, -d          Пожертвовать на развитие Snoop Project-а,
                        получить/приобрести Snoop full version
  --autoclean, -a       Удалить все отчеты, очистить место
  --update, -U          Обновить Snoop

plugins arguments:
  --module, -m          OSINT поиск: задействовать различные плагины
                        Snoop:: IP/GEO/YANDEX (список плагинов будет
                        пополняться)

search arguments:
  nickname              Никнейм разыскиваемого пользователя.
                        Поддерживается поиск одновременно нескольких имён.
                        Ник, содержащий в своем имени пробел, заключается в
                        кавычки
  --verbose, -v         Во время поиска 'nickname' выводить на печать
                        подробную вербализацию
  --base , -b <path>    Указать для поиска 'nickname' другую БД
                        (Локально)/В demo version функция отключена
  --web-base, -w        Подключиться для поиска 'nickname' к
                        обновляемой web_БД (Онлайн)/ В demo version функция
                        отключена
  --site , -s <site_name> 
                        Указать имя сайта из БД '--list-all'. Поиск
                        'nickname' на одном указанном ресурсе, допустимо
                        использовать опцию '-s' несколько раз
  --exclude , -e <country_code> 
                        Исключить из поиска выбранный регион,
                        допустимо использовать опцию '-e' несколько раз,
                        например, '-e RU -e WR' исключить из поиска Россию и
                        Мир
  --one-level , -o <country code> 
                        Влючить в поиск только выбранный регион,
                        допустимо использовать опцию '-o' несколько раз,
                        например, '-o US -o UA' поиск по США и Украине
  --country-sort, -c    Сортировка 'печать/запись_результатов' по
                        странам, а не по алфавиту
  --time-out , -t <digit> 
                        Установить выделение макс.времени на ожидание
                        ответа от сервера (секунды). Влияет на
                        продолжительность поиска. Влияет на 'Timeout ошибки'.
                        Вкл. эту опцию необходимо при медленном интернет
                        соединении, чтобы избежать длительных зависаний при
                        неполадках в сети (по умолчанию значение выставлено
                        5с)
  --found-print, -f     Выводить на печать только найденные аккаунты
  --no-func, -n         ✓Монохромный терминал, не использовать цвета
                        в url ✓Отключить звук ✓Запретить открытие web
                        browser-а ✓Отключить вывод на печать флагов стран
                        ✓Отключить индикацию и статус прогресса. Экономит
                        ресурсы системы и ускоряет поиск
  --userlist , -u <path> 
                        Указать файл со списком user-ов. Snoop
                        интеллектуально обработает данные и предоставит
                        доп.отчёты. Пример для Linux: 'python3 snoop.py -u
                        ~/users.txt'. Пример для Windows: 'python snoop.py -u
                        c:\User\User\Documents\users.txt'
  --save-page, -S       Сохранять найденные странички пользователей в
                        локальные файлы
  --cert-off, -C        Выкл проверку сертификатов на серверах. По
                        умолчанию проверка сертификатов на серверах включена
                        на Snoop for Android, что повышает скорость поиска, но
                        может дать больший percent ложных срабатываний
  --headers , -H <name> 
                        Задать user-agent вручную, агент заключается
                        в кавычки, по умолчанию для каждого сайта задаётся
                        случайный либо переопреденный user-agent из БД snoop.
                        https://юзерагент.рф/
  --normal-mode, -N     Переключатель режимов: SNOOPninja >
                        нормальный режим > SNOOPninja. По_умолчанию (GNU/Linux
                        full version) вкл 'режим SNOOPninja': ускорение поиска
                        ~25pct, экономия ОЗУ ~50pct, повторное 'гибкое'
                        соединение на сбойных ресурсах. Режим SNOOPninja
                        эффективен только для Snoop for GNU/Linux full
                        version. По_умолчанию (в Windows) вкл 'нормальный
                        режим'. В demo version переключатель режимов
                        деактивирован
  --quick-mode , -q     Вкл тихий режим поиска. Промежуточные
                        результаты не выводятся на печать. Повторные гибкие
                        соединения на сбойных ресурсах без замедления ПО.
                        Самый прогрессивный режим поиска (в разработке - не
                        использовать)
```


**Example**
```
# Для поиска только одного пользователя:
$ python3 snoop.py username1
# Или, например, кириллица поддерживается:
$ python3 snoop.py олеся
# Для поиска имени, содержащего пробел:
$ python3 snoop.py "ivan ivanov"
$ python3 snoop.py ivan_ivanov
$ python3 snoop.py ivan-ivanov

# Для поиска одного и более юзеров:
$ python3 snoop.py username1 username2 username3 username4

# Поиск множества юзеров — сортировка вывода результатов по странам;
# избежание длительных зависаний на сайтах (чаще 'мёртвая зона' зависит от вашего ip-адреса);
# выводить на печать только найденные аккаунты; сохранять странички найденных
# аккаунтов локально; указать файл со списком разыскиваемых аккаунтов;
# подключиться для поиска к расширяемой и обновляемой web-base Snoop:
$ python3 snoop.py -с -t 9 -f -S -u ~/file.txt -w
```
**'ctrl + c'** — прервать поиск (остановить корректно ПО).  

Найденные учетные записи будут храниться в '~/snoop/results/nicknames/*/username.{txt.csv.html}'.  
Для доступа браузера к результатам поиска на платформе Android желательно иметь рут права.  
csv открывать в *office, разделитель полей **запятая**.  

Уничтожить **все** результаты поиска — удалить каталог '~/snoop/results'.  
или ```python snoop.py --autoclean```

```
# Обновляйте Snoop для тестирования новых функций в ПО:
$ python3 snoop.py --update y #Требуется установка Git.
```

**An example snoop for android**  
<p align="center">  
  <img src="https://raw.githubusercontent.com/snooppr/snoop/master/images/Android%20snoop_run.gif" width="40%" />  
</p>  
