# Домашнее задание к занятию «Системы контроля версий» - Леонид Хорошев

   
------

## Задание 1. Создать и настроить репозиторий для дальнейшей работы на курсе

### Создание репозитория и первого коммита

1. Зарегистрируйте аккаунт на [https://github.com/](https://github.com/). Если предпочитаете другое хранилище для репозитория, можно использовать его.
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.1.png)
2. Создайте публичный репозиторий, который будете использовать дальше на протяжении всего курса, желательное с названием `devops-netology`.
   Обязательно поставьте галочку `Initialize this repository with a README`.
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.2.png)
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.3.png)      
3. Создайте [авторизационный токен](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) для клонирования репозитория.
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.4.png)
4. Склонируйте репозиторий, используя протокол HTTPS 
```
git clone https://github.com/LeonidKhoroshev/devops-netology
```
5. Перейдите в каталог с клоном репозитория.
```
cd devops-netology
```
6. Произведите первоначальную настройку Git, указав своё настоящее имя, чтобы нам было проще общаться, и email.
```
git config --global user.name Leonid Khoroshev
git config --global user.email khoroshevlv@gmail.com
```
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.12.png)
7. Выполните команду `git status` и запомните результат.

8. Отредактируйте файл `README.md` любым удобным способом, тем самым переведя файл в состояние `Modified`.
   
9. Ещё раз выполните `git status` и продолжайте проверять вывод этой команды после каждого следующего шага.

10. Теперь посмотрите изменения в файле `README.md`, выполнив команды `git diff` и `git diff --staged`.
    
11. Переведите файл в состояние `staged` (или, как говорят, просто добавьте файл в коммит) командой `git add README.md`.
    
12. И ещё раз выполните команды `git diff` и `git diff --staged`. Поиграйте с изменениями и этими командами, чтобы чётко понять, что и когда они отображают.
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.5.png)
13. Теперь можно сделать коммит `git commit -m 'First commit'`.
   
14. И ещё раз посмотреть выводы команд `git status`, `git diff` и `git diff --staged`.
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.6.png)

### Создание файлов `.gitignore` и второго коммита

1. Создайте файл `.gitignore` (обратите внимание на точку в начале файла), проверьте его статус сразу после создания.
```
nano .gitignore
git status
``` 
2. Добавьте файл `.gitignore` в следующий коммит (`git add...`).
```
git add .gitignore
```
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.7.png)
3. На одном из следующих блоков вы будете изучать `Terraform`, давайте сразу создадим соотвествующий каталог `terraform` и внутри этого каталога — файл `.gitignore` по примеру: https://github.com/github/gitignore/blob/master/Terraform.gitignore.
```
mkdir terraform
cd terraform
nano .gitignore
```
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.8.png)
4. В файле `README.md` опишите своими словами, какие файлы будут проигнорированы в будущем благодаря добавленному `.gitignore`.
Для удобства проверки домашнего задания содержание .gitignore в каталоге terraform опишу ниже:

5. Закоммитьте все новые и изменённые файлы. Комментарий к коммиту должен быть `Added gitignore`.
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.9.png)

### Эксперимент с удалением и перемещением файлов (третий и четвёртый коммит)

1. Создайте файлы `will_be_deleted.txt` (с текстом `will_be_deleted`) и `will_be_moved.txt` (с текстом `will_be_moved`) и закоммите их с комментарием `Prepare to delete and move`.
```
nano will_be_deleted.txt
nano will_be_moved.txt
git add will_be_deleted.txt
git add will_be_moved.txt
git commit -m `Prepare to delete and move`.
```
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.10.png)
2. Удалите файл `will_be_deleted.txt` с диска и из репозитория.
```
rm will_be_deleted.txt
```
3. Переименуйте (переместите) файл `will_be_moved.txt` на диске и в репозитории, чтобы он стал называться `has_been_moved.txt`.
```
cp will_be_moved.txt has_been_moved.txt
```
4. Закоммитьте результат работы с комментарием `Moved and deleted`.
```
git commit -m `Moved and deleted`.
```

### Проверка изменения

1.В результате предыдущих шагов в репозитории должно быть как минимум пять коммитов (если вы сделали ещё промежуточные — нет проблем):
    * `Initial Commit` — созданный GitHub при инициализации репозитория. 
    * `First commit` — созданный после изменения файла `README.md`.
    * `Added gitignore` — после добавления `.gitignore`.
    * `Prepare to delete and move` — после добавления двух временных файлов.
    * `Moved and deleted` — после удаления и перемещения временных файлов.
Проверка пройдена
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.11.png)
Однако, при переходе в репозиторий видны файлы `will_be_moved.txt` и `will_be_deleted.txt`. Удалим их:
```
git rm will_be_moved.txt
git rm will_be_deleted.txt
git commt -m "error correction"
```
![alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/git1/git1.13.png)
Теперь все корректно.

### Отправка изменений в репозиторий

Выполните команду `git push`, если Git запросит логин и пароль — введите ваши логин и пароль от GitHub. 
```
git push https://github.com/LeonidKhoroshev/devops-netology
```
В качестве результата отправьте ссылку на репозиторий.

https://github.com/LeonidKhoroshev/devops-netology

----
