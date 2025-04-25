#tp6_BigData : Cassandra

----------
## تشغيل cassandra في دوكر 
----------
<pre><code>docker run --name mon-cassandra -d -p 9042:9042 cassandra</code></pre>
------------------
## اعادة تشغيل الحاوية
----------------
<pre><code>docker start mon-cassandra </code></pre>
-----------------
## الدخول إلى واجهة أوامر Cassandra (cqlsh)
-------------
<pre><code>docker exec -it mon-cassandra cqlsh</code></pre>
----------------
## إنشاء قاعدة البيانات (Keyspace)
--------------
داخل cqlsh:
----------
<pre><code>CREATE KEYSPACE IF NOT EXISTS resto_ny 
WITH REPLICATION = { 'class': 'SimpleStrategy', 'replication_factor': 1 };

USE resto_ny;</code></pre>
-----------------
## إنشاء جدول 
-----------
جدول Restaurant:
------------
<pre><code>CREATE TABLE Restaurant (
    id text PRIMARY KEY,
    name text,
    borough text,
    buildingnum text,
    street text,
    zipcode text,
    phone text,
    cuisinetype text
);</code></pre>
--------------
جدول Inspection:
-------------
<pre><code>CREATE TABLE Inspection (
    idrestaurant text,
    inspectiondate text,
    violationcode text,
    violationdescription text,
    criticalflag text,
    score text,
    grade text,
    PRIMARY KEY (idrestaurant, inspectiondate)
);</code></pre>
----------------
##استيراد ملفات CSV إلى داخل الحاوية
-------------
<pre><code>docker cp "C:\Users\LAPTA\Downloads\restaurants\restaurants.csv" mon-cassandra:/restaurants.csv
docker cp "C:\Users\LAPTA\Downloads\restaurants\restaurants_inspections.csv" mon-cassandra:/restaurants_inspections.csv</code></pre>
--------------
## View 5 restaurants:
---------------
![2](https://github.com/user-attachments/assets/693f9d0a-a97f-4d71-bc06-b5b88d991537)

-------------
## View 5 inspections:
--------------
![1](https://github.com/user-attachments/assets/8b1b095e-eed9-4a0c-9514-90002c5f18ea)

------------
## Count total restaurants:
-----------
![3](https://github.com/user-attachments/assets/ecce3086-c38c-46a4-a566-b42ce5ba5891)

-------------
## Count total inspections:
-------------
![4](https://github.com/user-attachments/assets/3aa5a906-18af-4810-955e-bd9c0cfb0a33)

