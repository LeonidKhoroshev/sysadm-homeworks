# Домашнее задание к занятию «Инструменты Git» - Леонид Хорошев

### Цель задания

В результате выполнения задания вы:

* научитесь работать с утилитами Git;
* потренируетесь решать типовые задачи, возникающие при работе в команде. 

### Подготовка к выполнению задания:

```
mkdir terraform
cd terraform
git init
git clone https://github.com/hashicorp/terraform
```


------

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.

Воспользуемся командой `git log` с флагом -n и его значением 1, чтобы вывести только первый лог с общей информацией (хэш, автор, дата создания).
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git1.png)


2. Ответьте на вопросы.

* Какому тегу соответствует коммит `85024d3`?

Воспользуемся командой `git tag --points-at HEAD`, где заменим `HEAD` на хэш коммита, тэг которого мы ищем.
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git2.png)

* Сколько родителей у коммита `b8d720`? Напишите их хеши.

В данном случае воспользуемся простой командой `git show` и хэш коммита
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git3.png)
В выводе команды видим, что коммит создан в результате merge двух коммитов:
- 56cd785;
- 9ea88f2.

* Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.
Воспользуемся командой `git log v0.12.23..v0.12.24`.

Вывод команды получился, слишком объемным и не поместился на экран для скриншота, добавим опцию вывода коммитов и комментариев в одну строчку `--pretty=oneline`
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git4.png)
Теперь из представленной информации легко понять, что между заданными тегами было 9 коммитов, в них 3 раза вносили изменения в файл CHANGELOG.md, добавляли ссылку на сайте терраформа на vmc провайдера (видимо имеется ввиду, что-то связанное с виртуализацией), исправлены ошибки, связанные с недоступностью сервера и авторизацией в OC Windows.

* Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).

Пробуем искать через `git log -s function_name`, где имя нашей функции пишем как `func providerSource(` без аргументов (потому что мы их не знаем, более того, теоретически набор аргументов может отличаться)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git5.png)
Как видим, функция появилась в коммите 8c928e8 и судя по комментарию к коммиту тут добавлена возможность взаимодействия с облачными провайдерами.

* Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.

Решения в одно действие для данной задачи не найдено, поэтому сначала определяем файл (или файлы), содержащие данную функцию:
```
git grep 'func globalPluginDirs'
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git6.png)
Функция содержится в файле `plugins.go`, следовательно применяем выражение из презентации к данному занятию:
```
git log -L :globalPluginDirs:plugins.go
```
В результате получаем ошибку (как я понял путь к файлу не найден):
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git7.png)

Пробуем через регулярное выражение:
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git8.png)
Снова неудача, хотя это странно, так как данный ход решения кажется верным, более того, аналогичные примеры приведенные в лекции - отлично работали.

### В соответствии с полученными замечаниями рамках доработки данного пункта домашнего задания пробуем получить корректный вывод изменений тела функции через флаг -L
```
git log -L:globalPluginDirs:plugins.go
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git11.png)
Скорее всего проблема не в некорректной записи команды 'git log -L', а в версии Git.
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git12.png)
Так и есть, пробуем обновить версию git
```
yum upgrade git
yum update git
```
Результатов нет, следовательно необходимос качать git из стороннего репозитория, так как стандартные репозитории Centos7 безнадежно устарели
```
yum install http://opensource.wandisco.com/centos/7/git/x86_64/wandisco-git-release-7-2.noarch.rpm
yum install git
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git13.png)
Новая версия git установлена успешно, повторяем поиск изменений в функции
```
git log -L:globalPluginDirs:plugins.go
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git14.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git15.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git16.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git17.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git18.png)

Обилие информации на скриншотах демонтсрирует удобство работьы в последней версии Git, хэши коммитов выделены желтым цветом, изменения, внесенные в функцию globalPluginDirs выделены зелеными и красными цветами (добавленные и удаленные части кода).

А теперь, для удобства прочтения информации посмотрим краткий вывод
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git19.png)
Изменения в функцию вносились в 5 коммитах.

* Кто автор функции `synchronizedWriters`?

Воспользуемся функцией из предыдущего задания, только с более подробным выводом:
```
git log -S 'synchronizedWriters'
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-04-tools/tool/git10.png)

Автор первого коммита, в котором добавлена искомая функция - Martin Atkin.



