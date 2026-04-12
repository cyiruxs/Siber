## Karakter Dizisi (String) Fonksiyonları

String fonksiyonları, bir karakter dizisi üzerinde işlemler gerçekleştirerek onunla ilişkili bir değer döndürür.

#### CONCAT() Fonksiyonu

Bu fonksiyon iki veya daha fazla karakter dizisini birbirine eklemek için kullanılır. Farklı sütunlardaki metinleri birleştirmek için yararlıdır.

**Terminal**

SQL

```
mysql> SELECT CONCAT(name, " is a type of ", category, " book.") AS book_info FROM books;
+------------------------------------------------------------------+
| book_info                                                         |
+------------------------------------------------------------------+
| Android Security Internals is a type of Defensive Security book. |
| Bug Bounty Bootcamp is a type of Offensive Security book.        |
| Car Hacker's Handbook is a type of Offensive Security book.      |
| Designing Secure Software is a type of Defensive Security book.  |
| Ethical Hacking is a type of Offensive Security book.            |
+------------------------------------------------------------------+

5 rows in set (0.00 sec)
```

Bu sorgu, `books` tablosundaki `name` ve `category` sütunlarını `book_info` adlı tek bir sütunda birleştirir.

#### GROUP_CONCAT() Fonksiyonu

Bu fonksiyon, birden fazla satırdaki verileri tek bir alanda birleştirmemize yardımcı olabilir. Kullanımına dair bir örneği inceleyelim.

**Terminal**

SQL

```
mysql> SELECT category, GROUP_CONCAT(name SEPARATOR ", ") AS books
    FROM books
    GROUP BY category;
+--------------------+-------------------------------------------------------------+
| category           | books                                                       |
+--------------------+-------------------------------------------------------------+
| Defensive Security | Android Security Internals, Designing Secure Software       |
| Offensive Security | Bug Bounty Bootcamp, Car Hacker's Handbook, Ethical Hacking |
+--------------------+-------------------------------------------------------------+

2 rows in set (0.01 sec)
```

Yukarıdaki sorgu, kitapları `category` (kategori) bazında gruplandırır ve her kategorideki kitap başlıklarını virgülle ayrılmış tek bir karakter dizisi halinde birleştirir.

#### SUBSTRING() Fonksiyonu

Bu fonksiyon, bir sorgu içerisindeki karakter dizisinden, belirlenen konumdan başlayarak bir alt dizge (substring) alır. Bu alt dizgenin uzunluğu da belirtilebilir.

**Terminal**

SQL

```
mysql> SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books;
+----------------+
| published_year |
+----------------+
| 2014           |
| 2021           |
| 2016           |
| 2021           |
| 2021           |
+----------------+

5 rows in set (0.00 sec)
```

Yukarıdaki sorguda, `published_date` sütunundan ilk dört karakteri nasıl çıkardığını ve bunları `published_year` sütununda sakladığını gözlemleyebiliriz.

#### LENGTH() Fonksiyonu

Bu fonksiyon, bir karakter dizisindeki karakter sayısını döndürür. Buna boşluklar ve noktalama işaretleri dahildir. Aşağıda bir örneğini görebiliriz.

**Terminal**

SQL

```
mysql> SELECT LENGTH(name) AS name_length FROM books;
+-------------+
| name_length |
+-------------+
|          26 |
|          19 |
|          21 |
|          25 |
|          15 |
+-------------+

5 rows in set (0.00 sec)
```

Yukarıda gözlemleyebileceğimiz gibi sorgu, `name` sütunundaki karakter dizisinin uzunluğunu hesaplar ve bunu `name_length` adlı bir sütunda saklar.

---

## Toplama (Aggregate) Fonksiyonları

Bu fonksiyonlar, sorguda belirtilen bir kritere göre birden fazla satırın değerini birleştirir; birden fazla değeri tek bir sonuçta toplayabilir.

#### COUNT() Fonksiyonu

Aşağıdaki örnekte gösterildiği gibi, bu fonksiyon bir ifade içindeki kayıt sayısını döndürür.

**Terminal**

SQL

```
mysql> SELECT COUNT(*) AS total_books FROM books;
+-------------+
| total_books |
+-------------+
|           5 |
+-------------+

1 row in set (0.01 sec)
```

Yukarıdaki bu sorgu, `books` tablosundaki toplam satır sayısını sayar. `books` tablosunda beş kitap olduğu için sonuç 5'tir ve `total_books` sütununda saklanır.

#### SUM() Fonksiyonu

Bu fonksiyon, belirlenen bir sütundaki tüm değerleri (NULL olmayanlar) toplar. **Not:** Bu sorguyu çalıştırmanıza gerek yoktur. Bu sadece örnek amaçlıdır.

**Terminal**

SQL

```
mysql> SELECT SUM(price) AS total_price FROM books;
+-------------+
| total_price |
+-------------+
|      249.95 |
+-------------+

1 row in set (0.00 sec)
```

Yukarıdaki sorgu, `price` sütununun toplamını hesaplar. Sonuç, `total_price` sütunundaki tüm kitapların toplam fiyatını sağlar.

#### MAX() Fonksiyonu

Bu fonksiyon, bir ifade içinde sağlanan sütundaki maksimum değeri hesaplar.

**Terminal**

SQL

```
mysql> SELECT MAX(published_date) AS latest_book FROM books;
+-------------+
| latest_book |
+-------------+
| 2021-12-21  |
+-------------+

1 row in set (0.00 sec)
```

Yukarıdaki sorgu, `books` tablosundan en son yayınlanma tarihini (maksimum değer) getirir. `2021-12-21` sonucu `latest_book` sütununda saklanır.

#### MIN() Fonksiyonu

Bu fonksiyon, bir ifade içinde sağlanan sütundaki minimum değeri hesaplar.

**Terminal**

SQL

```
mysql> SELECT MIN(published_date) AS earliest_book FROM books;
+---------------+
| earliest_book |
+---------------+
| 2014-10-14    |
+---------------+

1 row in set (0.00 sec)
```

Yukarıdaki sorgu, `books` tablosundan en eski yayınlanma tarihini (minimum değer) getirir. `2014-10-14` sonucu `earliest_book` sütununda saklanır.

---

## 🛠 Ek Bilgiler ve Kavramlar

Fonksiyonlar, veritabanı seviyesinde veri temizliği ve ön işleme yapmak için en güçlü araçlardır.

## String Manipülasyonunun Önemi

Karakter dizisi fonksiyonları sadece metin birleştirmekle kalmaz, aynı zamanda verilerin standart hale getirilmesini (örneğin tüm isimleri büyük harfe çeviren `UPPER()` fonksiyonu gibi) sağlar.

## Aggregate Fonksiyonlar ve NULL Değerler

Aggregate fonksiyonları (özellikle `SUM` ve `AVG`), hesaplama yaparken `NULL` değerleri otomatik olarak yok sayar. Ancak `COUNT(*)` tüm satırları sayarken, `COUNT(sütun_adı)` sadece o sütunda değeri olan satırları sayar.

---

## 🚩 CTF & Siber Güvenlik İpuçları

Fonksiyonlar, siber güvenlik dünyasında özellikle "Blind SQL Injection" ve "Veri Sızdırma" aşamalarında hayati rol oynar.

## 1. SUBSTRING() ve Karakter Tahmini

Kör SQL Enjeksiyonu (Blind SQLi) sırasında bir saldırgan şifreleri doğrudan göremez. Bu yüzden `SUBSTRING()` kullanarak karakter karakter tahmin yürütür: `AND SUBSTRING((SELECT password FROM users WHERE id=1), 1, 1) = 'a'` Eğer sonuç doğru dönerse, admin şifresinin ilk harfinin 'a' olduğu anlaşılır.

## 2. GROUP_CONCAT() ile Hızlı Veri Sızdırma

Bir SQL Injection açıklığı bulduğunuzda, her satırı tek tek çekmek yerine `GROUP_CONCAT()` kullanarak tüm tablo adlarını veya kullanıcı adlarını tek bir satırda birleştirip hızlıca çalabilirsiniz: `UNION SELECT 1, GROUP_CONCAT(username), 3 FROM users--` Bu komut, tüm kullanıcı adlarını aralarına virgül koyarak tek bir sonuç içinde döndürür.

## 3. LENGTH() ile Parola Analizi

Bir veritabanına sızarken `LENGTH()` fonksiyonu, hedef parolanın kaç karakter olduğunu bulmanıza yardımcı olur. Bu, brute-force (kaba kuvvet) saldırısının karmaşıklığını ve süresini tahmin etmek için kullanılır: `AND LENGTH((SELECT password FROM users WHERE id=1)) = 8`

## 4. Bilgi Toplama (Reconnaissance)

Saldırganlar veritabanı yapısını anlamak için toplama fonksiyonlarını kullanır. Örneğin, `COUNT(*)` ile bir tabloda ne kadar veri olduğunu anlayarak hangisinin daha değerli (örn: çok kullanıcılı tablo) olduğunu saptayabilirler.

> **Güvenlik Notu:** Veritabanı fonksiyonlarının kullanıcı girdileriyle (user input) doğrudan tetiklenmesi risklidir. Web uygulamalarınızda "Input Validation" (Girdi Doğrulaması) yaparak saldırganların bu fonksiyonları kötüye kullanmasını engelleyin.