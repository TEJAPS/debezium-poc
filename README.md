# debezium-poc

===============

SQL Script:
create table customer (
customerid serial primary key,
customername varchar(255),
city varchar(255),
country varchar(255)
);

ALTER TABLE public.customer REPLICA IDENTITY FULL;

INERT INTO Customer(CustomerName, City, Country)
VALUES ('Cardinal','Stavanger','Norway');


docker run --tty spring-boot-debezium-master-slave-example_default confluentinc/cp-kafkacat kafkacat -b kafka:9092 -C -s key-s -s value=avro -r http:/schema-registry:8081 -t postgres.public.customer

===============

Q1. who is producing it to the topic called postgres.public.consumer - debezium_master-connector
Q2. and where did we create this topic - topic name format is - <database_server_name>.<schema_name>.<table_name>
Q3. and how is debezium getting the events of postgres udpates/create/delete -  "connector.class": "io.debezium.connector.postgresql.PostgresConnector"

===============