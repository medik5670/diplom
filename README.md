# Дипломный проект профессии «Тестировщик ПО»

## Документация

#### [План автоматизации тестирования](../main/docs/Plan.md)
#### [Отчёт о проведённом тестировании](../main/docs/Report.md)
#### [Отчёт о проведённой автоматизации](../main/docs/Summary.md)

## Инструкция по запуску SUT и авто-тестов

### Предусловия

1. Для запуска проекта и тестов на локальной машине потребуются установленные 
Git, JDK 11, IntelliJ IDEA, Docker, Docker Compose.
3. Запустить Docker Desktop.
2. Склонировать репозиторий на локальную машину командой в Git:

   `git clone https://github.com/BrainLucker/qa-diploma.git`

4. Запустить IntelliJ IDEA и открыть проект.

### 1. Запуск контейнеров

Для старта контейнеров с БД (MySQL, PostgreSQL) и симулятором банковских сервисов
выполнить в терминале из корня проекта команду: `docker-compose up`.
Дождаться пока поднимутся БД (вывод логов запуска прекратится).

### 2. Запуск SUT

В новой вкладке терминала из корня проекта выполнить одну из команд:

* С подключением к MySQL:

  `java -jar artifacts\aqa-shop.jar --spring.datasource.url=jdbc:mysql://localhost:3306/app`

* С подключением к PostgreSQL:

  `java -jar artifacts\aqa-shop.jar --spring.datasource.url=jdbc:postgresql://localhost:5432/app`

### 3. Запуск авто-тестов

#### Все тестовые классы

В консоли «Run Anything» (двойное нажатие Ctrl) выполнить одну из команд в зависимости от выбранной БД в п. 2.

* С подключением к MySQL:

  `./gradlew clean test -Ddb.url=jdbc:mysql://localhost:3306/app`

* С подключением к PostgreSQL:

  `./gradlew clean test -Ddb.url=jdbc:postgresql://localhost:5432/app`

#### Отдельный тестовый класс

Запустить необходимый тестовый класс отдельно можно командой в консоли, указав его имя, например:

`./gradlew clean test --tests BuyTourCreditPageTest` ...

Либо запустить его с помощью кнопки «Run» в IDEA.

#### Установка БД по-умолчанию

При желании можно выставить предпочтительную БД по-умолчанию для выполнения тестов. Для этого нужно раскомментировать соответствующую строку
в файле [build.gradle](../main/build.gradle).

### 4. Формирование отчета AllureReport

В консоли «Run Anything» (двойное нажатие Ctrl) выполнить команду: `./gradlew allureServe`.
Отчет сгенерируется на основе результатов последнего прогона тестов и автоматически откроется в браузере.
По окончании работы с отчетом необходимо завершить выполнение процесса allureServe, нажав Ctrl + F2 во вкладке «Run» терминала.
###Отчёт Allure
![21](https://github.com/user-attachments/assets/5a539ed1-9c30-4526-b335-e68e19cbc4d2)
###Скриншот отчёта для сервиса платежей (Оплата по карте):
![23](https://github.com/user-attachments/assets/9707a6b6-051f-4d7a-b824-1433ed40cd92)
![24](https://github.com/user-attachments/assets/6ba714af-29f9-41d4-96a4-006863a0e61e)
###Скриншот отчёта для сервиса платежей (В кредит о данным карты):
![image](https://github.com/user-attachments/assets/e1d86128-f33d-4863-988b-e02482b21bbe)
![image](https://github.com/user-attachments/assets/1f4df4cc-25a8-494c-9a80-3666c3c17985)
###Скриншот отчета: Отправка запросов с реквизитами карт на API
![image](https://github.com/user-attachments/assets/31fcf0f2-02e8-45f9-b14c-72ea9bc08fb3)




