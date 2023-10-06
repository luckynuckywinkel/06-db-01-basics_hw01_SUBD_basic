# Домашнее задание к занятию 1. «Типы и структура СУБД»

## Введение

Перед выполнением задания вы можете ознакомиться с 
[дополнительными материалами](https://github.com/netology-code/virt-homeworks/tree/virt-11/additional).

## Задача 1

Архитектор ПО решил проконсультироваться у вас, какой тип БД 
лучше выбрать для хранения определённых данных.

Он вам предоставил следующие типы сущностей, которые нужно будет хранить в БД:

- электронные чеки в json-виде,
- склады и автомобильные дороги для логистической компании,
- генеалогические деревья,
- кэш идентификаторов клиентов с ограниченным временем жизни для движка аутенфикации,
- отношения клиент-покупка для интернет-магазина.

Выберите подходящие типы СУБД для каждой сущности и объясните свой выбор.  

### Ответ:  

- Электронные чеки в JSON-виде -  NoSQL СУБД, такая как MongoDB. Эта СУБД позволяет легко хранить и индексировать документы JSON.


- Склады и автомобильные дороги для логистической компании - можно использовать т.н. географические СУБД или географические расширения для реляционных СУБД, например, PostGIS для PostgreSQL.

- Генеалогические деревья - графовых СУБД, таких как Neo4j (если често, первый раз услышал про нее).

- Кэш идентификаторов клиентов с ограниченным временем жизни для движка аутентификации - для кэширования идентификаторов с ограниченным временем жизни можно использовать in-memory базу данных, такую как Redis.

- Отношения клиент-покупка для интернет-магазина - реляционный СУБД, PostgreSQL, MySQL или Microsoft SQL Server


---

## Задача 2

Вы создали распределённое высоконагруженное приложение и хотите классифицировать его согласно 
CAP-теореме. Какой классификации по CAP-теореме соответствует ваша система, если 
(каждый пункт — это отдельная реализация вашей системы и для каждого пункта нужно привести классификацию):

- данные записываются на все узлы с задержкой до часа (асинхронная запись);
- при сетевых сбоях система может разделиться на 2 раздельных кластера;
- система может не прислать корректный ответ или сбросить соединение.

Согласно PACELC-теореме как бы вы классифицировали эти реализации?  

### Ответ:  

- Для начала, приведем тут расшифровку CAP. Consistency (согласованность), Availability (доступность), Partition Tolerance (устойчивость к разделению).

-   данные записываются на все узлы с задержкой до часа (асинхронная запись) - **CP**

-  при сетевых сбоях система может разделиться на 2 раздельных кластера - **CA**

-  система может не прислать корректный ответ или сбросить соединение - **AP**

  

- Согласно PACELC-теореме, которая расширяет CAP-теорему, системы могут быть классифицированы следующим образом:

-   

P (Partition tolerance): Все три реализации вероятно обеспечивают устойчивость к разделению, так как они способны продолжать работать даже при сетевых разделениях.  

A (Availability): Вторая и третья реализации обеспечивают доступность, даже если это означает отправку некорректных ответов или сброс соединения. Первая реализация, возможно, также обеспечивает доступность, но с задержкой в час.  

C (Consistency): Первая и вторая реализации компрометируют согласованность, так как данные могут не быть согласованными между всеми узлами из-за асинхронной записи и сетевых разделений. Третья реализация также компрометирует согласованность из-за возможности отправки некорректных ответов.  

  
---

## Задача 3

Могут ли в одной системе сочетаться принципы BASE и ACID? Почему?  

### Ответ:    

- Данные принципы применяются в разных контекстах и могут представлять разные компромиссы в отношении доступности и согласованности данных. Думаю, что их использование в одной системе возможно, например, в случае использования контейнеров (микросервисов), либо в неких гибридных системах, но, думаю, это очень сложный процесс взаимодействия.

---

## Задача 4

Вам дали задачу написать системное решение, основой которого бы послужили:

- фиксация некоторых значений с временем жизни,
- реакция на истечение таймаута.

Вы слышали о key-value-хранилище, которое имеет механизм Pub/Sub. 
Что это за система? Какие минусы выбора этой системы?  

### Ответ:  

- И это, конечно же....Redis!) Что из себя представляет Redis и Pub/Sub (из гугла):
Redis - это in-memory key-value хранилище данных с поддержкой различных структур данных, таких как строки, списки, множества и другие. Он также предоставляет механизм Pub/Sub, который позволяет клиентам подписываться на каналы и получать уведомления (события) о событиях, происходящих в системе. Redis также может использоваться для установки времени жизни для ключей (ttl).

- Главным, пожалуй, минусом данной системы является потеря данных при перезапуске, т.к. Redis хранит данные в оперативной памяти. Также, пишут, что Redis - это система со сложным обеспечением ее отказоустойчивости при ее использовании в сложных конфигурациях и кластерах.

---

