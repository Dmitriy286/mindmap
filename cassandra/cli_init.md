Работа в консоли 



**Docker**

Запустить Docker Desktop.

Открыть консоль (терминал).

Выполнить команду:

docker run --name cassandra-cluster -p 9042:9042 -d cassandra:latest

Выполнить команду:

docker exec -it cassandra-cluster cqlsh

Выполнить команду:

CREATE KEYSPACE spring_cassandra WITH replication = {'class': 'SimpleStrategy', 'replication_factor' : 1};




При широких таблицах можно ввести в консоли expand on для включения более читаемого отображения записей


