# PostgreSQL_Ödevler

## 📝 ÖDEV-1

### Aşağıdaki sorgu senaryolarını **dvdrental** örnek veri tabanı üzerinden gerçekleştiriniz.

SORU 1 - Film tablosunda bulunan title ve description sütunlarındaki verileri sıralayınız.
```sql
SELECT title, description FROM film;
```
SORU 2 - Film tablosunda bulunan tüm sütunlardaki verileri film uzunluğu (length) 60 dan büyük VE 75 ten küçük olma koşullarıyla sıralayınız.
```sql
SELECT * FROM film 
WHERE length > 60 AND length < 75;
```
SORU 3 - Film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99 VE replacement_cost 12.99 VEYA 28.99 olma koşullarıyla sıralayınız.
```sql
SELECT * FROM film
WHERE rental_rate = 0.99 AND (replacement_cost = 12.99 OR replacement_cost = 28.99);
```
SORU 4 - Customer tablosunda bulunan first_name sütunundaki değeri 'Mary' olan müşterinin last_name sütunundaki değeri nedir?
```sql
SELECT first_name, last_name FROM customer
WHERE first_name = 'Mary';
```
SORU 5 - Film tablosundaki uzunluğu(length) 50 ten büyük OLMAYIP aynı zamanda rental_rate değeri 2.99 veya 4.99 OLMAYAN verileri sıralayınız.
```sql
SELECT * FROM film
WHERE length <= 50 AND NOT (rental_rate = 2.99 OR rental_rate = 4.99);
```

## 📝 ÖDEV-2

SORU 1 - Film tablosunda bulunan tüm sütunlardaki verileri replacement cost değeri 12.99 dan büyük eşit ve 16.99 küçük olma koşuluyla sıralayınız ( BETWEEN - AND yapısını kullanınız.)
```sql
SELECT * FROM film
WHERE replacement_cost BETWEEN 12.99 AND 16.99;
```
SORU 2 - Actor tablosunda bulunan first_name ve last_name sütunlardaki verileri first_name 'Penelope' veya 'Nick' veya 'Ed' değerleri olması koşuluyla sıralayınız. ( IN operatörünü kullanınız.)
```sql
SELECT first_name, last_name FROM actor
WHERE first_name IN ('Penelope','Nick','Ed');
```
SORU 3 - Film tablosunda bulunan tüm sütunlardaki verileri rental_rate 0.99, 2.99, 4.99 VE replacement_cost 12.99, 15.99, 28.99 olma koşullarıyla sıralayınız. ( IN operatörünü kullanınız.)
```sql
SELECT * FROM film
WHERE rental_rate IN (0.99, 2.99, 4.99) AND replacement_cost IN (12.99, 15.99, 28.99);
```

## 📝 ÖDEV-3 

### NOT: ~~ işareti LIKE anlamına gelir

SORU 1 - country tablosunda bulunan country sütunundaki ülke isimlerinden 'A' karakteri ile başlayıp 'a' karakteri ile sonlananları sıralayınız.
```sql
SELECT country FROM country 
WHERE country ~~ 'A%a';
```
SORU 2 - country tablosunda bulunan country sütunundaki ülke isimlerinden en az 6 karakterden oluşan ve sonu 'n' karakteri ile sonlananları sıralayınız.
```sql
SELECT country FROM country
WHERE country ~~ '_____%n';
```
SORU 3 - film tablosunda bulunan title sütunundaki film isimlerinden en az 4 adet büyük ya da küçük harf farketmesizin 'T' karakteri içeren film isimlerini sıralayınız.
```sql
SELECT title FROM film
WHERE title ILIKE '%t%t%t%t%';
```
SORU 4 - film tablosunda bulunan tüm sütunlardaki verilerden title 'C' karakteri ile başlayan ve uzunluğu (length) 90 dan büyük olan ve rental_rate 2.99 olan verileri sıralayınız.
```sql
SELECT * FROM film 
WHERE length > 90 AND rental_rate = 2.99 AND title ~~ 'C%';
```

## 📝 ÖDEV-4

SORU 1 - Film tablosunda bulunan replacement_cost sütununda bulunan birbirinden farklı değerleri sıralayınız.
```sql
SELECT DISTINCT replacement_cost FROM film;
```
SORU 2 - Film tablosunda bulunan replacement_cost sütununda birbirinden farklı kaç tane veri vardır?
```sql
SELECT COUNT(DISTINCT replacement_cost) FROM film;
```
SORU 3 - Film tablosunda bulunan film isimlerinde (title) kaç tanesini T karakteri ile başlar ve aynı zamanda rating 'G' ye eşittir?
```sql
SELECT COUNT(title) AS title FROM film
WHERE title LIKE 'T%' AND rating = 'G';
```
SORU 4 - Country tablosunda bulunan ülke isimlerinden (country) kaç tanesi 5 karakterden oluşmaktadır?
```sql
SELECT COUNT(country) AS country FROM country
WHERE country LIKE '_____';
```
SORU 5 - City tablosundaki şehir isimlerinin kaç tanesi R veya r karakteri ile biter?
```sql
SELECT COUNT(city) AS city FROM city
WHERE city ILIKE '%r';
```

## 📝 ÖDEV-5

SORU 1 - Film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en uzun (length) 5 filmi sıralayınız.
```sql
SELECT * FROM film
WHERE title LIKE '%n'
ORDER BY length DESC
LIMIT 5;
```
SORU 2 - Film tablosunda bulunan ve film ismi (title) 'n' karakteri ile biten en kısa (length) ikinci(6,7,8,9,10) 5 filmi(6,7,8,9,10) sıralayınız.
```sql
SELECT * FROM film
WHERE title LIKE '%n'
ORDER BY length ASC
OFFSET 5
LIMIT 5;
```
SORU 3 - Customer tablosunda bulunan last_name sütununa göre azalan yapılan sıralamada store_id 1 olmak koşuluyla ilk 4 veriyi sıralayınız.
```sql
SELECT * FROM customer
WHERE store_id = 1
ORDER BY last_name DESC
LIMIT 4;
```

## 📝 ÖDEV-6

SORU 1 - Film tablosunda bulunan rental_rate sütunundaki değerlerin ortalaması nedir?
```sql
SELECT ROUND(AVG(rental_rate),4) AS average FROM film;
```
SORU 2 - Film tablosunda bulunan filmlerden kaç tanesi 'C' karakteri ile başlar?
```sql
SELECT COUNT(*) AS count FROM film
WHERE title ~~ 'C%';
```
SORU 3 - Film tablosunda bulunan filmlerden rental_rate değeri 0.99 a eşit olan en uzun (length) film kaç dakikadır?
```sql
SELECT MAX(length) AS max FROM film
WHERE rental_rate = 0.99;
```
SORU 4 - Film tablosunda bulunan filmlerin uzunluğu 150 dakikadan büyük olanlarına ait kaç farklı replacement_cost değeri vardır?
```sql
SELECT COUNT(DISTINCT replacement_cost) FROM film
WHERE length > 150;
```

## 📝 ÖDEV-7

SORU 1 - Film tablosunda bulunan filmleri rating değerlerine göre gruplayınız.
```sql
SELECT rating FROM film
GROUP BY rating;
```
SORU 2 - Film tablosunda bulunan filmleri replacement_cost sütununa göre grupladığımızda film sayısı 50 den fazla olan replacement_cost değerini ve karşılık gelen film sayısını sıralayınız.
```sql
SELECT replacement_cost, COUNT(film_id) AS count FROM film
GROUP BY replacement_cost
HAVING COUNT(film_id) > 50; 
```
SORU 3 - Customer tablosunda bulunan store_id değerlerine karşılık gelen müşteri sayılarını nelerdir? 
```sql
SELECT store_id, COUNT(customer_id) FROM customer
GROUP BY store_id;
```
SORU 4 - City tablosunda bulunan şehir verilerini country_id sütununa göre gruplandırdıktan sonra en fazla şehir sayısı barındıran country_id bilgisini ve şehir sayısını paylaşınız.
```sql
SELECT country_id, COUNT(city_id) FROM city
GROUP BY country_id
ORDER BY COUNT(city_id) DESC
LIMIT 1;	
```

## 📝 ÖDEV-8

SORU 1 - Test veritabanınızda employee isimli sütun bilgileri id(INTEGER), name VARCHAR(50), birthday DATE, email VARCHAR(100) olan bir tablo oluşturalım.
```sql
CREATE TABLE employee(
	id INTEGER PRIMARY KEY,
	name VARCHAR(50),
	birthday DATE,
	email VARCHAR(100)
);
```
SORU 2 - Oluşturduğumuz employee tablosuna 'Mockaroo' servisini kullanarak 50 adet veri ekleyelim.
```sql
insert into employee (id, first_name, birthday, email) values (1, 'Elnore', '2019-10-04', 'echance0@sohu.com');
insert into employee (id, first_name, birthday, email) values (2, 'Tova', '2020-02-08', 'tbarcke1@unc.edu');
insert into employee (id, first_name, birthday, email) values (3, 'Redd', '2020-02-05', 'rdockrill2@nsw.gov.au');
insert into employee (id, first_name, birthday, email) values (4, 'Jaclin', '2019-06-03', 'jlodden3@angelfire.com');
insert into employee (id, first_name, birthday, email) values (5, 'Adelina', '2019-06-14', 'apennoni4@typepad.com');
insert into employee (id, first_name, birthday, email) values (6, 'Horatia', '2019-06-26', 'hsilbersak5@constantcontact.com');
insert into employee (id, first_name, birthday, email) values (7, 'Hilliard', '2019-09-24', 'hluquet6@fastcompany.com');
insert into employee (id, first_name, birthday, email) values (8, 'Ursala', '2019-11-16', 'usnaddon7@home.pl');
insert into employee (id, first_name, birthday, email) values (9, 'Liesa', '2019-07-18', 'ljefferson8@over-blog.com');
insert into employee (id, first_name, birthday, email) values (10, 'Herrick', '2019-05-24', 'hsherlock9@epa.gov');
insert into employee (id, first_name, birthday, email) values (11, 'Zackariah', null, 'zeallisa@independent.co.uk');
insert into employee (id, first_name, birthday, email) values (12, 'Celinda', '2019-08-18', null);
insert into employee (id, first_name, birthday, email) values (13, 'Aleta', '2019-10-18', 'acrollc@weather.com');
insert into employee (id, first_name, birthday, email) values (14, 'Chryste', null, 'ctinklind@vistaprint.com');
insert into employee (id, first_name, birthday, email) values (15, 'Vanna', null, 'vpantone@forbes.com');
insert into employee (id, first_name, birthday, email) values (16, 'Howard', '2019-08-25', 'hpodsf@wp.com');
insert into employee (id, first_name, birthday, email) values (17, 'Brigit', '2019-10-05', 'bdaughtong@disqus.com');
insert into employee (id, first_name, birthday, email) values (18, 'Margette', '2019-11-13', null);
insert into employee (id, first_name, birthday, email) values (19, 'Lenore', '2019-08-06', 'lsowrahi@upenn.edu');
insert into employee (id, first_name, birthday, email) values (20, 'Jodie', null, 'jkeastj@blogger.com');
insert into employee (id, first_name, birthday, email) values (21, 'Delainey', '2020-01-13', 'dgreberk@over-blog.com');
insert into employee (id, first_name, birthday, email) values (22, 'Gayleen', null, 'gbarhimsl@deliciousdays.com');
insert into employee (id, first_name, birthday, email) values (23, 'Judi', '2020-02-03', 'jheapem@intel.com');
insert into employee (id, first_name, birthday, email) values (24, 'Ailina', null, 'amaccaghann@hhs.gov');
insert into employee (id, first_name, birthday, email) values (25, 'Olivie', '2019-08-17', 'owilneo@seesaa.net');
insert into employee (id, first_name, birthday, email) values (26, 'Keane', '2019-07-30', null);
insert into employee (id, first_name, birthday, email) values (27, 'Leighton', null, 'lmucklestonq@bizjournals.com');
insert into employee (id, first_name, birthday, email) values (28, 'Madelaine', null, 'mkincaidr@who.int');
insert into employee (id, first_name, birthday, email) values (29, 'Wilek', '2019-10-13', 'witzkowiczs@uiuc.edu');
insert into employee (id, first_name, birthday, email) values (30, 'Gar', '2019-12-29', 'ggatlandt@house.gov');
insert into employee (id, first_name, birthday, email) values (31, 'Imojean', null, 'ibutleru@cornell.edu');
insert into employee (id, first_name, birthday, email) values (32, 'Gwenni', '2019-08-19', null);
insert into employee (id, first_name, birthday, email) values (33, 'Lorenza', '2020-02-03', 'lcaudrayw@boston.com');
insert into employee (id, first_name, birthday, email) values (34, 'Bill', '2020-01-24', 'bbrockhurstx@behance.net');
insert into employee (id, first_name, birthday, email) values (35, 'De witt', null, 'drowlingsy@youtube.com');
insert into employee (id, first_name, birthday, email) values (36, 'Del', null, 'dhansiez@creativecommons.org');
insert into employee (id, first_name, birthday, email) values (37, 'Zarah', '2020-02-16', 'zkirwin10@issuu.com');
insert into employee (id, first_name, birthday, email) values (38, 'Julita', null, null);
insert into employee (id, first_name, birthday, email) values (39, 'Rodrigo', '2019-03-29', 'rphetteplace12@e-recht24.de');
insert into employee (id, first_name, birthday, email) values (40, 'Janot', null, 'jmarklew13@earthlink.net');
insert into employee (id, first_name, birthday, email) values (41, 'Minda', '2019-06-29', 'mtorrance14@simplemachines.org');
insert into employee (id, first_name, birthday, email) values (42, 'Quentin', null, 'qkirckman15@123-reg.co.uk');
insert into employee (id, first_name, birthday, email) values (43, 'Wait', null, 'wvasnev16@java.com');
insert into employee (id, first_name, birthday, email) values (44, 'Dave', '2019-12-13', null);
insert into employee (id, first_name, birthday, email) values (45, 'Tonya', '2019-05-15', 'tdiprose18@hao123.com');
insert into employee (id, first_name, birthday, email) values (46, 'Franz', '2019-06-15', 'fwalklot19@linkedin.com');
insert into employee (id, first_name, birthday, email) values (47, 'Bess', '2019-08-11', 'bchinnick1a@google.it');
insert into employee (id, first_name, birthday, email) values (48, 'Olivia', '2019-04-04', 'ojovovic1b@businesswire.com');
insert into employee (id, first_name, birthday, email) values (49, 'Devan', '2019-09-10', 'dvsanelli1c@craigslist.org');
insert into employee (id, first_name, birthday, email) values (50, 'Sayer', null, 'sleil1d@trellian.com');
```
SORU 3 - Sütunların her birine göre diğer sütunları güncelleyecek 5 adet UPDATE işlemi yapalım.
```sql
--1
UPDATE employee 
SET name='Sevval',
birthday = '1999-06-01',
email = 'svvlozlem.carkit@gmail.com'
WHERE id = 5;
--2
UPDATE employee 
SET name='Alan',
birthday = '1912-06-23',
email = 'alan@turing.com'
WHERE id = 47;
--3
UPDATE employee
SET email = 'pisa@gor.com',
name = 'Pisagor'
WHERE birthday = '2019-09-10';
--4
UPDATE employee
SET birthday = '22-02-1860'
WHERE name = 'Minda';
--5
UPDATE employee
SET name = 'XXX',
birthday = '1982-02-23'
WHERE id = 33;
```
SORU 4 - Sütunların her birine göre ilgili satırı silecek 5 adet DELETE işlemi yapalım.
```sql
--1
DELETE FROM employee
WHERE name = 'Sevval';
--2
DELETE FROM employee
WHERE id = 25
RETURNING *;
--3
DELETE FROM employee
WHERE email = 'tbarcke1@unc.edu'
RETURNING *;
--4
DELETE FROM employee
WHERE birthday = '2019-09-24';
--5
DELETE FROM employee
WHERE id = 11;
```

