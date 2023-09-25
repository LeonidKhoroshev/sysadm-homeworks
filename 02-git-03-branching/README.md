# Домашнее задание к занятию «Ветвления в Git» - Леонид Хорошев

### Цель задания

В процессе работы над заданием вы потренеруетесь делать merge и rebase. В результате вы поймете разницу между ними и научитесь решать конфликты.   

Обычно при нормальном ходе разработки выполнять `rebase` достаточно просто. 
Это позволяет объединить множество промежуточных коммитов при решении задачи, чтобы не засорять историю. Поэтому многие команды и разработчики предпочитают такой способ.   


## Задание «Ветвление, merge и rebase»  

**Шаг 1.** Предположим, что есть задача — написать скрипт, выводящий на экран параметры его запуска. 
Давайте посмотрим, как будет отличаться работа над этим скриптом с использованием ветвления, merge и rebase. 

Создайте в своём репозитории каталог `branching` и в нём два файла — `merge.sh` и `rebase.sh` — с 
содержимым:

```bash
#!/bin/bash
# display command line options

count=1
for param in "$*"; do
    echo "\$* Parameter #$count = $param"
    count=$(( $count + 1 ))
done
```

Этот скрипт отображает на экране все параметры одной строкой, а не разделяет их.

```
mkdir branching
cd branching
nano merge.sh
nano rebase.sh
cd ..
git add branching
```

**Шаг 2.** Создадим коммит с описанием `prepare for merge and rebase` и отправим его в ветку main.

```
git checkout main
git commit -m "prepare for merge and rebase"
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/megre1.1.png)

#### Подготовка файла merge.sh 
 
**Шаг 1.** Создайте ветку `git-merge`. 
```
git checkout -b git-merge
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.2.png)

**Шаг 2**. Замените в ней содержимое файла `merge.sh` на:

```bash
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "\$@ Parameter #$count = $param"
    count=$(( $count + 1 ))
done
```

```
nano branching/merge.sh
git add branching
```


**Шаг 3.** Создайте коммит `merge: @ instead *`, отправьте изменения в репозиторий. 
```
git commit -m "merge: @ instead *"
git push https://github.com/LeonidKhoroshev/devops-netology git-merge
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.3.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.4.png)

**Шаг 4.** Разработчик подумал и решил внести ещё одно изменение в `merge.sh`:
 
```bash
#!/bin/bash
# display command line options

count=1
while [[ -n "$1" ]]; do
    echo "Parameter #$count = $1"
    count=$(( $count + 1 ))
    shift
done
```

Теперь скрипт будет отображать каждый переданный ему параметр отдельно.

**Шаг 5.** Создайте коммит `merge: use shift` и отправьте изменения в репозиторий. 
```
git commit -m "merge: use shift"
git push https://github.com/LeonidKhoroshev/devops-netology git-merge
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.5.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.6.png)

#### Изменим main  

**Шаг 1.** Вернитесь в ветку `main`. 
```
git checkout main
```

**Шаг 2.** Предположим, что пока мы работали над веткой `git-merge`, кто-то изменил `main`. Для этого
изменим содержимое файла `rebase.sh` на:

```bash
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "\$@ Parameter #$count = $param"
    count=$(( $count + 1 ))
done

echo "====="
```

В этом случае скрипт тоже будет отображать каждый параметр в новой строке. 

**Шаг 3.** Отправляем изменённую ветку `main` в репозиторий.

```
git add branching
git commit -m "changing rebase.sh"
git push https://github.com/LeonidKhoroshev/devops-netology main
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.7.png)

#### Подготовка файла rebase.sh  

**Шаг 1.** Предположим, что теперь другой участник нашей команды не сделал `git pull` либо просто хотел ответвиться не от последнего коммита в `main`, а от коммита, когда мы только создали два файла
`merge.sh` и `rebase.sh` на первом шаге.  
Для этого при помощи команды `git log` найдём хеш коммита `prepare for merge and rebase` и выполним `git checkout` на него так:
```
git log --oneline
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.8.png)

**Шаг 2.** Создадим ветку `git-rebase`, основываясь на текущем коммите.
```
git checkout -f e790614
git checkout git-rebase
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.9.png)

**Шаг 3.** И изменим содержимое файла `rebase.sh` на следующее, тоже починив скрипт, но немного в другом стиле:

```bash
#!/bin/bash
# display command line options

count=1
for param in "$@"; do
    echo "Parameter: $param"
    count=$(( $count + 1 ))
done

echo "====="
```

**Шаг 4.** Отправим эти изменения в ветку `git-rebase` с комментарием `git-rebase 1`.
```
git add branching
git commit -m "git-rebase 1"
git push https://github.com/LeonidKhoroshev/devops-netology git-rebase
```
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.10.png)


**Шаг 5.** И сделаем ещё один коммит `git-rebase 2` с пушем, заменив `echo "Parameter: $param"` на `echo "Next parameter: $param"`.

```
nano branching/rebase.sh
```

```
#!/bin/bash
# display command line options
count=1 for param in "$@"; do
    echo "Next parameter: $param"
    count=$(( $count + 1 )) done
echo "====="
```

```
git add branching
git commit -m "git-rebase 2"
git push https://github.com/LeonidKhoroshev/devops-netology git-rebase
```

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.11.png)

#### Промежуточный итог  

Мы сэмулировали типичную ситуации в разработке кода, когда команда разработчиков работала над одним и тем же участком кода, и кто-то из разработчиков 
предпочитает делать `merge`, а кто-то — `rebase`. Конфликты с merge обычно решаются просто, 
а с rebase бывают сложности, поэтому давайте смержим все наработки в `main` и разрешим конфликты. 

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.12.png)


#### Merge

Сливаем ветку `git-merge` в main и отправляем изменения в репозиторий, должно получиться без конфликтов:

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.13.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.14.png)

В результате получаем такую схему:
  
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merga1.15.png)

#### Rebase

**Шаг 1.** Перед мержем ветки `git-rebase` выполним её `rebase` на main. Да, мы специально создали ситуацию с конфликтами, чтобы потренироваться их решать. 

**Шаг 2.** Переключаемся на ветку `git-rebase` и выполняем `git rebase -i main`. 
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.16.png)

Если посмотреть содержимое файла `rebase.sh`, то увидим метки, оставленные Git для решения конфликта:
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.17.png)


**Шаг 3.** Удалим метки, отдав предпочтение варианту:

```bash
echo "\$@ Parameter #$count = $param"
```

**Шаг 4.** Сообщим Git, что конфликт решён `git add rebase.sh` и продолжим rebase `git rebase --continue`.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.18.png)

**Шаг 5.** Опять получим конфликт в файле `rebase.sh` при попытке применения нашего второго коммита. Давайте разрешим конфликт, оставив строчку `echo "Next parameter: $param"`.
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.19.png)
**Шаг 6.** Далее опять сообщаем Git о том, 
что конфликт разрешён — `git add rebase.sh` — и продолжим rebase — `git rebase --continue`.

**Шаг 7.** И попробуем выполнить `git push` либо `git push -u origin git-rebase`, чтобы точно указать, что и куда мы хотим запушить. 

Эта команда завершится с ошибкой:
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.20.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.21.png)
Это произошло, потому что мы пытаемся перезаписать историю. 

**Шаг 8.** Чтобы Git позволил нам это сделать, добавим флаг `force`:
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.22.png)

**Шаг 9**. Теперь можно смержить ветку `git-rebase` в main без конфликтов и без дополнительного мерж-комита простой перемоткой: 
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.23.png)

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/02-git-03-branching/merge/merge1.24.png)

 Репозиторий devops-netology
 https://github.com/LeonidKhoroshev/devops-netology
 
----
