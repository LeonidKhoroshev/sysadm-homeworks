# Домашнее задание к занятию «Основы Git» - Леонид Хорошев

### Цель задания

В результате выполнения задания вы:

* научитесь работать с Git, как с распределённой системой контроля версий; 
* сможете создавать и настраивать репозиторий для работы в GitHub, GitLab и Bitbucket; 
* попрактикуетесь работать с тегами;
* поработаете с Git при помощи визуального редактора.

------

## Задание 1. Знакомимся с GitLab и Bitbucket 


### GitLab

Создание аккаунта в GitLab:

1. GitLab. Для [регистрации](https://gitlab.com/users/sign_up)  можно использовать аккаунт Google, GitHub и другие.
   
2. Создание нового проекта: 

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git1.1.png)

3. Вывод команды `git remote -v` на localhost (виртуалка на базе Centos7, развернутая в VirtualBox для выполнения домашних заданий по данному курсу).

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git1.2.png)

4. Добавление репозитория на GitLab, как дополнительного к созданному в рамках предыдущего домашнего задания:
```
git remote add gitlab https://gitlab.com/LeonidKhoroshev/devops_netology
git push https://gitlab.com/LeonidKhoroshev/devops_netology.git main
```

5. Проверка изменения работы команды `git remote -v`.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git1.3.png)


### Bitbucket* (задание со звёздочкой) 
____

Создание репозитория и добавление его как дополнительного выполнено аналогично операциям с репозиторием в GitLab

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git1.5.png)

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git1.4.png)

Поскольку использование Bitbucket предполагает постоянный обход блокировок (в моем случае через включенный VPN клиент, что не удобно при работе в териминале PuTTY), то дальнейшие задания выполнены в репозиториях GitHub и GitLab.

Выполните push локальной ветки `main` в новые репозитории. 

Подсказка: `git push -u gitlab main`. На этом этапе история коммитов во всех трёх репозиториях должна совпадать. 

## Задание 2. Теги

Представьте ситуацию, когда в коде была обнаружена ошибка — надо вернуться на предыдущую версию кода,
исправить её и выложить исправленный код в продакшн. Мы никуда не будем выкладывать код, но пометим некоторые коммиты тегами и создадим от них ветки. 

1. Создайте легковестный тег `v0.0` на HEAD-коммите и запуште его во все три добавленных на предыдущем этапе `upstream`.
   
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git2.1.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git2.2.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git2.4.png)
2. Аналогично создайте аннотированный тег `v0.1`.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git2.3.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git2.5.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git2.8.png)

3. Перейдите на страницу просмотра тегов в GitHab (и в других репозиториях) и посмотрите, чем отличаются созданные теги. 

Просмотр тегов в GitLab:

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git2.6.png)

Просмотр тегов в GitHub:

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git2.7.png)


## Задание 3. Ветки 

Давайте посмотрим, как будет выглядеть история коммитов при создании веток. 

1. Переключитесь обратно на ветку `main`, которая должна быть связана с веткой `main` репозитория на `github`.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.1.png)

2. Посмотрите лог коммитов и найдите хеш коммита с названием `Prepare to delete and move`, который был создан в пределах предыдущего домашнего задания.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.2.png)

3. Выполните `git checkout` по хешу найденного коммита. 
4. Создайте новую ветку `fix`, базируясь на этом коммите `git switch -c fix`.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.3.png)
![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.4.png)

5. Отправьте новую ветку в репозиторий на GitHub `git push -u origin fix`.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.5.png)

6. Посмотрите, как визуально выглядит ваша схема коммитов: https://github.com/YOUR_ACCOUNT/devops-netology/network.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.6.png)

7. Теперь измените содержание файла `README.md`, добавив новую строчку.

```
nano README.md
# devops-netology
Repository from my educational projects
This repository created following netology's lesson about version control system and Git introduction.
A new row has been created.
```

8. Отправьте изменения в репозиторий и посмотрите, как изменится схема на странице https://github.com/YOUR_ACCOUNT/devops-netology/network 
и как изменится вывод команды `git log`.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.7.png)


![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.8.png)

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git3.9.png)

## Задание 4. Упрощаем себе жизнь

Попробуем поработь с Git при помощи визуального редактора. 

Поскольку работа выполняется в OC Centos7 без графического интерфейса, в качестве подготовки к выполнению Задания 4 выполним установку GUI

```
yum update
sudo yum -y groups install "GNOME Desktop"
echo "exec gnome-session" >> ~/.xinitrc
startx
```

1. В используемой IDE PyCharm откройте визуальный редактор работы с Git, находящийся в меню View -> Tool Windows -> Git.

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git4.1.png)

2. Измените какой-нибудь файл, и он сразу появится на вкладке `Local Changes`, отсюда можно выполнить коммит, нажав на кнопку внизу этого диалога.

Меняем Readme:

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git4.2.png)

Создаем коммит и пушим его в репозиторий на GitHub:

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git4.3.png)

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git4.4.png)

3. Проверяем изменения:

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git4.5.png)

![Alt text](https://github.com/LeonidKhoroshev/sysadm-homeworks/blob/devsys10/01-intro-01/git2/git4.6.png)

Эксперимент удачный, но по-поводу "упрощения" вывод неоднозначный, так как графический интерфейс на виртуальной машине несет в себе дополнительные проблемные моменты, как например его установка, скорость работы и удобство использования (тот же браузер например).
 
----

### Ссылки на  репозитории:

https://github.com/LeonidKhoroshev/devops-netology

https://gitlab.com/LeonidKhoroshev/devops_netology
