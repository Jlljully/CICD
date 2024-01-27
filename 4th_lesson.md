# Домашнее задание к занятию 10 «Jenkins»

## Подготовка к выполнению

1. Создать два VM: для jenkins-master и jenkins-agent.
2. Установить Jenkins при помощи playbook.
3. Запустить и проверить работоспособность.
4. Сделать первоначальную настройку.

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-nrqs.png "установка")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-ngea.png "установка")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-ngxo.png "установка")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-njth.png "установка")


## Основная часть

1. Сделать Freestyle Job, который будет запускать `molecule test` из любого вашего репозитория с ролью.
2. Сделать Declarative Pipeline Job, который будет запускать `molecule test` из любого вашего репозитория с ролью.
3. Перенести Declarative Pipeline в репозиторий в файл `Jenkinsfile`.
4. Создать Multibranch Pipeline на запуск `Jenkinsfile` из репозитория.
5. Создать Scripted Pipeline, наполнить его скриптом из [pipeline](./pipeline).
6. Внести необходимые изменения, чтобы Pipeline запускал `ansible-playbook` без флагов `--check --diff`, если не установлен параметр при запуске джобы (prod_run = True). По умолчанию параметр имеет значение False и запускает прогон с флагами `--check --diff`.
7. Проверить работоспособность, исправить ошибки, исправленный Pipeline вложить в репозиторий в файл `ScriptedJenkinsfile`.
8. Отправить ссылку на репозиторий с ролью и Declarative Pipeline и Scripted Pipeline.
9. Сопроводите процесс настройки скриншотами для каждого пункта задания!!

## Ответ

1. Выдала для дженкинса временный токен на гитхабе, добавила его в дженкинс

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-nmvm.png "task1")

Создала джоб с запуском молекулы и просто парой выводов, убедилась, что удаленный реп во временную директорию скачивается (видно по ls -la), молекула тест не выполняется, потому что поставила последнюю, а снова с версиями сейчас мучаться не хочется. Работу дженкинса проверила:

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-noqq.png "task1")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-nofp.png "task1")

2. Сделала такой же декларативный джоб тоже с парой лишних выводов в консоль, чтоб видеть, что работает все, кроме молекулы:

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-nthb.png "task2")

Вспомнила, что не добавляла метки))) Добавила

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-ntoi.png "task2")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-nten.png "task2")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-nvrw.png "task2")

3-4. Перенесла этот джоб в дженкинс файл в своем репе, сделала отдельный джоб:

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-oilg.png "task3")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-oiuc.png "task3")

Снова все ок, кроме самой молекулы

5-7. Создала джоб со скриптом, добавила параметр prod_run

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-oexn.png "task5")

вместо проверки secret_check закинуа проверку prod_run - если true, выполняется без --check --diff, если false - с ним. В идеале, все должно работать, но доступ, кажется, стух, потому что спустя 10 минут работает таймаут и отваливается джоб:

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-ogbo.png "task5")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-ogee.png "task5")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-ojbv.png "task5")

![Скрин](https://github.com/Jlljully/CI_files/blob/main/lesson4/SCR-20240127-oksd.png "task5")


## Необязательная часть

1. Создать скрипт на groovy, который будет собирать все Job, завершившиеся хотя бы раз неуспешно. Добавить скрипт в репозиторий с решением и названием `AllJobFailure.groovy`.
2. Создать Scripted Pipeline так, чтобы он мог сначала запустить через Yandex Cloud CLI необходимое количество инстансов, прописать их в инвентори плейбука и после этого запускать плейбук. Мы должны при нажатии кнопки получить готовую к использованию систему.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
