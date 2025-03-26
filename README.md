# Домашнее задание к занятию 7 «Жизненный цикл ПО - Мельник Юрий Александрович»

## Подготовка к выполнению

1. Получить бесплатную версию Jira - https://www.atlassian.com/ru/software/jira/work-management/free (скопируйте ссылку в адресную строку). Вы можете воспользоваться любым(в том числе бесплатным vpn сервисом) если сайт у вас недоступен. Кроме того вы можете скачать [docker образ](https://hub.docker.com/r/atlassian/jira-software/#) и запустить на своем хосте self-managed версию jira.
2. Настроить её для своей команды разработки.
3. Создать доски Kanban и Scrum.
4. [Дополнительные инструкции от разработчика Jira](https://support.atlassian.com/jira-cloud-administration/docs/import-and-export-issue-workflows/).

## Основная часть

Необходимо создать собственные workflow для двух типов задач: bug и остальные типы задач. Задачи типа bug должны проходить жизненный цикл:

1. Open -> On reproduce.
2. On reproduce -> Open, Done reproduce.
3. Done reproduce -> On fix.
4. On fix -> On reproduce, Done fix.
5. Done fix -> On test.
6. On test -> On fix, Done.
7. Done -> Closed, Open.

Остальные задачи должны проходить по упрощённому workflow:

1. Open -> On develop.
2. On develop -> Open, Done develop.
3. Done develop -> On test.
4. On test -> On develop, Done.
5. Done -> Closed, Open.

**Что нужно сделать**

1. Создайте задачу с типом bug, попытайтесь провести его по всему workflow до Done. 
1. Создайте задачу с типом epic, к ней привяжите несколько задач с типом task, проведите их по всему workflow до Done. 
1. При проведении обеих задач по статусам используйте kanban. 
1. Верните задачи в статус Open.
1. Перейдите в Scrum, запланируйте новый спринт, состоящий из задач эпика и одного бага, стартуйте спринт, проведите задачи до состояния Closed. Закройте спринт.
2. Если всё отработалось в рамках ожидания — выгрузите схемы workflow для импорта в XML. Файлы с workflow и скриншоты workflow приложите к решению задания.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---

# Решение

## Установка Jira.
### Установим Jira с помощью docker используя инструкцию 
[docker образ Jira ](https://hub.docker.com/r/atlassian/jira-software/#)

устновим pgsql командой 
```sh
sudo -i docker run -d   --name jira-postgres   -e POSTGRES_DB=jiradb   -e POSTGRES_USER=jirauser   -e POSTGRES_PASSWORD=секретный_пароль   -p 5432:5432   postgres:13
Unable to find image 'postgres:13' locally
```

установим Jira командой 
```sh
docker volume create --name jiraVolume
docker run -v jiraVolume:/var/atlassian/application-data/jira --name="jira" -d -p 8080:8080 atlassian/jira-software
```

## Создадим собственные workflow для двух типов задач: bug и остальные типы задач. Задачи типа bug должны проходить жизненный цикл:

### Bug Workflow 
  
Статус     	| Категория  
-----------------------  
Open	       | To Do  
On reproduce   | In Progress  
Done reproduce | Done  
On fix	       | In Progress  
Done fix       | Done  
On test	       | In Progress  
Done	       | Done  
Closed	       | Done  

![Рисунок 1](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_1.jpg)  

### Simple Workflow

Статус     	| Категория  
-----------------------  
Open         | To Do  
On develop   | In Progress  
Done develop | Done  
On test	     | In Progress  
Done	     | Done  
Closed       | Done  

![Рисунок 2](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_2.jpg)  

для это нужежно перейти Настройки Issues, Workflows. Создать новые Workflows    Bug Workflow и Simple Workflow  
Используя **Add status** и **Add transition** нужно добавить статусы шагов и связи  
![Рисунок 3](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_3.jpg)  

нужно добавить схему  Workflow
![Рисунок 4](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_4.jpg) и применить ее к проекту!   
Перейди в Jira → Settings (⚙) → Issues → Workflow Schemes.  
Нажми Add Workflow Scheme, назовите, например: Custom Workflow Scheme.  
Добавьте туда оба workflow:  
Привяжите Bug Workflow к типу задачи Bug.  
Привяжите Simple Workflow ко всем остальным типам (Task, Epic, Story и т.д.).  

Применение к проекту   
Найдите свой проект → Project Settings → Workflows.  
Нажмите Switch Scheme или Use a different scheme, выбери Custom Workflow Scheme.  
Подтвердите переход (если предложит миграцию задач — соглашаемся с сохранением текущих статусов).  

## Создание задач и прогон через Kanban
### Создаём Epic - большая задача                                  "Big Mission"
### Создаём Task - подзадача                                       "Реализовать фронтенд"  
### Создаём Bug - тип ошибка, требует внесения исправлений в код   "Кнопка не работает"  
![Рисунок 5](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_5.jpg)
![Рисунок 6](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_6.jpg)
Задачи созданы!


## Kanban-доска и переходы
Доска типа Kanban создана 
![Рисунок 7](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_7.jpg)


Проведем все задачи через статус
Bug:
Через статусы: Open → On reproduce → Done reproduce → On fix → Done fix → On test → Done  
![Рисунок 8](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_8.jpg)  
![Рисунок 9](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_9.jpg) 

Task:
Через: Open → On develop → Done develop → On test → Done  
![Рисунок 10](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_10.jpg)  
![Рисунок 11](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_11.jpg)  
![Рисунок 12](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_12.jpg)  
![Рисунок 13](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_13.jpg)  

Вернtv задачи в статус Open - Согласно задания

## Scrum-доска и спринт
![Рисунок 14](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_14.jpg)  

Создадим спринт и перетащим на него задачи
![Рисунок 15](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_15.jpg)  
Стартуем спринт

![Рисунок 16](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_16.jpg)  
![Рисунок 17](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_17.jpg)  

Завершим спринт
![Рисунок 18](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_18.jpg)  
![Рисунок 19](https://github.com/ysatii/live_cicle_softwar/blob/main/img/img_19.jpg)  

## Файлы с workflow и скриншоты workflow
[Bug_Workflow.](https://github.com/ysatii/live_cicle_softwar/blob/main/Bug_Workflow.xml)  
[Simple_Workflow](https://github.com/ysatii/live_cicle_softwar/blob/main/Simple_Workflow.xml)  