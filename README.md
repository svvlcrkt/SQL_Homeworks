# PostgreSQL_Homeworks

## 📝 HW-1

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
