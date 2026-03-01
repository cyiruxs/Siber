SQL ile çalışırken mantık ve karşılaştırmalarla uğraştığımızda, operatörler verileri etkili bir şekilde filtrelemek ve manipüle etmek için kullandığımız araçlardır. Bu operatörleri anlamak, daha kesin ve güçlü sorgular oluşturmanıza yardımcı olacaktır. Bir sonraki iki görevde, `thm_books2` veritabanının bir parçası olan `books` tablosunu kullanacağız. Bu tabloya `use thm_books2;` ifadesiyle erişebiliriz.

---

## Mantıksal Operatörler (Logical Operators)

Bu operatörler bir koşulun doğruluğunu test eder ve TRUE (Doğru) veya FALSE (Yanlış) şeklinde bir boolean değer döndürür. Şimdi bu operatörlerden bazılarını inceleyelim.

#### LIKE Operatörü

`LIKE` operatörü, bir sütun içindeki belirli kalıpları filtrelemek için genellikle `WHERE` gibi yancümlelerle birlikte kullanılır. Kullanımına bir örnek sorgulamak için veritabanımızı kullanmaya devam edelim.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE description LIKE "%guide%";
+----+----------------------------+----------------+--------------------------------------------------------+--------------------+
| id | name                        | published_date | description                                            | category           |
+----+----------------------------+----------------+--------------------------------------------------------+--------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture   | Defensive Security |
|  2 | Bug Bounty Bootcamp        | 2021-11-16     | The Guide to Finding and Reporting Web Vulnerabilities | Offensive Security |
|  3 | Car Hacker's Handbook      | 2016-02-25     | A Guide for the Penetration Tester                     | Offensive Security |
|  4 | Designing Secure Software  | 2021-12-21     | A Guide for Developers                                 | Defensive Security |
+----+----------------------------+----------------+--------------------------------------------------------+--------------------+

4 rows in set (0.00 sec)
```

Yukarıdaki sorgu, `books` tablosundan filtrelenmiş bir kayıt listesi döndürür; ancak bu kayıtlar `LIKE` operatörü kullanılarak içinde "guide" kelimesi geçen `WHERE` yancümlesine sahip olanlardır.

#### AND Operatörü

`AND` operatörü bir sorgu içinde birden fazla koşul kullanır ve eğer bu koşulların tamamı doğruysa TRUE döndürür.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE category = "Offensive Security" AND name = "Bug Bounty Bootcamp"; 
+----+---------------------+----------------+--------------------------------------------------------+--------------------+
| id | name                | published_date | description                                            | category           |
+----+---------------------+----------------+--------------------------------------------------------+--------------------+
|  2 | Bug Bounty Bootcamp | 2021-11-16     | The Guide to Finding and Reporting Web Vulnerabilities | Offensive Security |
+----+---------------------+----------------+--------------------------------------------------------+--------------------+
    
1 row in set (0.00 sec)
```

Yukarıdaki sorgu, "Offensive Security" kategorisi altında yer alan ve adı "Bug Bounty Bootcamp" olan kitabı döndürür.

#### OR Operatörü

`OR` operatörü, sorgular içinde birden fazla koşulu birleştirir ve bu koşullardan en az biri doğruysa TRUE döndürür.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE name LIKE "%Android%" OR name LIKE "%iOS%"; 
+----+----------------------------+----------------+------------------------------------------------------+--------------------+
| id | name                        | published_date | description                                          | category           |
+----+----------------------------+----------------+------------------------------------------------------+--------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture | Defensive Security |
+----+----------------------------+----------------+------------------------------------------------------+--------------------+

1 row in set (0.00 sec)
```

Yukarıdaki sorgu, adında "Android" veya "iOS" geçen kitapları döndürür.

#### NOT Operatörü

`NOT` operatörü bir boolean operatörün değerini tersine çevirerek belirli bir koşulu dışlamamıza olanak tanır.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE NOT description LIKE "%guide%";
+----+-----------------+----------------+----------------------------------------+--------------------+
| id | name            | published_date | description                            | category           |
+----+-----------------+----------------+----------------------------------------+--------------------+
|  5 | Ethical Hacking | 2021-11-02     | A Hands-on Introduction to Breaking In | Offensive Security |
+----+-----------------+----------------+----------------------------------------+--------------------+

1 row in set (0.00 sec)
```

Yukarıdaki sorgu, açıklama kısmında "guide" kelimesi bulunmayan sonuçları döndürür.

#### BETWEEN Operatörü

`BETWEEN` operatörü, bir değerin tanımlanmış bir aralıkta olup olmadığını test etmemizi sağlar.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE id BETWEEN 2 AND 4;
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+
| id | name                      | published_date | description                                            | category           |
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+
|  2 | Bug Bounty Bootcamp       | 2021-11-16     | The Guide to Finding and Reporting Web Vulnerabilities | Offensive Security |
|  3 | Car Hacker's Handbook      | 2016-02-25     | A Guide for the Penetration Tester                     | Offensive Security |
|  4 | Designing Secure Software | 2021-12-21     | A Guide for Developers                                 | Defensive Security |
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+

3 rows in set (0.00 sec)
```

Yukarıdaki sorgu, id'si 2 ile 4 arasında olan kitapları döndürür.

---

## Karşılaştırma Operatörleri (Comparison Operators)

Karşılaştırma operatörleri değerleri karşılaştırmak ve belirtilen kriterleri karşılayıp karşılamadıklarını kontrol etmek için kullanılır.

#### Equal To (Eşittir) Operatörü

`=` (Eşit) operatörü iki ifadeyi karşılaştırır ve eşit olup olmadıklarını belirler veya bir değerin belirli bir sütundaki başka bir değerle eşleşip eşleşmediğini kontrol edebilir.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE name = "Designing Secure Software";
+----+---------------------------+----------------+------------------------+--------------------+
| id | name                      | published_date | description            | category           |
+----+---------------------------+----------------+------------------------+--------------------+
|  4 | Designing Secure Software | 2021-12-21     | A Guide for Developers | Defensive Security |
+----+---------------------------+----------------+------------------------+--------------------+

1 row in set (0.10 sec)
```

Yukarıdaki sorgu, tam adı "Designing Secure Software" olan kitabı döndürür.

#### Not Equal To (Eşit Değildir) Operatörü

`!=` (Eşit değil) operatörü ifadeleri karşılaştırır ve eşit olup olmadıklarını test eder; ayrıca bir değerin sütun içindeki değerden farklı olup olmadığını kontrol eder.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE category != "Offensive Security";
+----+----------------------------+----------------+------------------------------------------------------+--------------------+
| id | name                        | published_date | description                                          | category           |
+----+----------------------------+----------------+------------------------------------------------------+--------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture | Defensive Security |
|  4 | Designing Secure Software  | 2021-12-21     | A Guide for Developers                               | Defensive Security |
+----+----------------------------+----------------+------------------------------------------------------+--------------------+

2 rows in set (0.00 sec)
```

Yukarıdaki sorgu, kategorisi "Offensive Security" olanlar dışındaki kitapları döndürür.

#### Less Than (Küçüktür) Operatörü

`<` (Küçüktür) operatörü, verilen bir değere sahip ifadenin sağlanan değerden daha küçük olup olmadığını karşılaştırır.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE published_date < "2020-01-01";
+----+----------------------------+----------------+------------------------------------------------------+--------------------+
| id | name                        | published_date | description                                          | category           |
+----+----------------------------+----------------+------------------------------------------------------+--------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture | Defensive Security |
|  3 | Car Hacker's Handbook      | 2016-02-25     | A Guide for the Penetration Tester                     | Offensive Security |
+----+----------------------------+----------------+------------------------------------------------------+--------------------+

2 rows in set (0.00 sec)
```

Yukarıdaki sorgu, 1 Ocak 2020'den önce yayınlanmış kitapları döndürür.

#### Greater Than (Büyüktür) Operatörü

`>` (Büyüktür) operatörü, verilen bir değere sahip ifadenin sağlanan değerden daha büyük olup olmadığını karşılaştırır.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE published_date > "2020-01-01";
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+
| id | name                      | published_date | description                                            | category           |
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+
|  2 | Bug Bounty Bootcamp       | 2021-11-16     | The Guide to Finding and Reporting Web Vulnerabilities | Offensive Security |
|  4 | Designing Secure Software | 2021-12-21     | A Guide for Developers                                 | Defensive Security |
|  5 | Ethical Hacking           | 2021-11-02     | A Hands-on Introduction to Breaking In                 | Offensive Security |
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+

3 rows in set (0.00 sec)
```

Yukarıdaki sorgu, 1 Ocak 2020'den sonra yayınlanmış kitapları döndürür.

#### Less Than or Equal To (Küçük Eşittir) ve Greater Than or Equal To (Büyük Eşittir) Operatörleri

`<=` (Küçük eşittir) operatörü, verilen bir değere sahip ifadenin sağlanan değerden küçük veya ona eşit olup olmadığını karşılaştırır. Diğer yandan, `>=` (Büyük eşittir) operatörü, verilen bir değere sahip ifadenin sağlanan değerden büyük veya ona eşit olup olmadığını karşılaştırır. Aşağıda her ikisi için de bazı örnekleri inceleyelim.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE published_date <= "2021-11-15";
+----+----------------------------+----------------+------------------------------------------------------+--------------------+
| id | name                        | published_date | description                                          | category           |
+----+----------------------------+----------------+------------------------------------------------------+--------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture | Defensive Security |
|  3 | Car Hacker's Handbook      | 2016-02-25     | A Guide for the Penetration Tester                     | Offensive Security |
|  5 | Ethical Hacking            | 2021-11-02     | A Hands-on Introduction to Breaking In                 | Offensive Security |
+----+----------------------------+----------------+------------------------------------------------------+--------------------+

3 rows in set (0.00 sec)
```

Yukarıdaki sorgu, 15 Kasım 2021 tarihinde veya bu tarihten önce yayınlanmış kitapları döndürür.

**Terminal**

SQL

```
mysql> SELECT *
    FROM books
    WHERE published_date >= "2021-11-02";
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+
| id | name                      | published_date | description                                            | category           |
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+
|  2 | Bug Bounty Bootcamp       | 2021-11-16     | The Guide to Finding and Reporting Web Vulnerabilities | Offensive Security |
|  4 | Designing Secure Software | 2021-12-21     | A Guide for Developers                                 | Defensive Security |
|  5 | Ethical Hacking           | 2021-11-02     | A Hands-on Introduction to Breaking In                 | Offensive Security |
+----+---------------------------+----------------+--------------------------------------------------------+--------------------+

3 rows in set (0.00 sec)
```

Yukarıdaki sorgu, 2 Kasım 2021 tarihinde veya bu tarihten sonra yayınlanmış kitapları döndürür.

---

## 🛠 Ek Bilgiler ve Kavramlar

Operatörler, veritabanı motorunun verileri nasıl işleyeceğini belirleyen mantıksal yapı taşlarıdır.

## Operatör Öncelik Sırası (Operator Precedence)

Sorgularda birden fazla operatör kullanıldığında, SQL bunları belirli bir sıraya göre işler. Karmaşık sorgularda `()` parantez kullanmak mantıksal hataların önüne geçer.

1. Parantezler `()`
    
2. `NOT`
    
3. `AND`
    
4. `OR`
    

## NULL Değerleri ile Karşılaştırma

SQL'de `NULL` değeri "bilinmeyen" anlamına gelir. Bu yüzden `column = NULL` veya `column != NULL` ifadeleri çalışmaz. Bunun yerine:

- `IS NULL`: Değer boşsa TRUE döndürür.
    
- `IS NOT NULL`: Değer doluysa TRUE döndürür.
    

---

## 🚩 CTF & Siber Güvenlik İpuçları

Operatörler, siber güvenlik dünyasında hem savunma hem de saldırı amaçlı çok sık kullanılır.

## 1. SQL Injection'da Mantıksal Operatörlerin Gücü

En temel SQL Injection saldırısı olan `' OR 1=1 --` ifadesi, `OR` operatörünün mantığına dayanır. Koşullardan biri (`1=1`) her zaman doğru olduğu için tüm `WHERE` filtresi TRUE döner ve giriş kontrolü atlanır.

## 2. Kör SQL Enjeksiyonu (Blind SQLi)

Veritabanı çıktısının web sayfasında görünmediği durumlarda, saldırganlar `AND` operatörü ve karşılaştırma operatörlerini kullanarak veritabanına "evet/hayır" soruları sorar: `AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='admin') = 'a'` Eğer sayfa normal yüklenirse, admin şifresinin ilk harfinin 'a' olduğunu anlarız.

## 3. Zaman Tabanlı Saldırılar

Saldırganlar bazen karşılaştırmaları zaman gecikmeleriyle birleştirir: `AND IF(1=1, SLEEP(5), 0)` Bu, eğer koşul doğruysa sunucuyu 5 saniye bekletir. Gecikmeyi ölçerek verinin doğruluğunu teyit ederler.

## 4. LIKE ve Wildcard (Joker Karakter) Sömürüsü

`LIKE` operatörü ile birlikte kullanılan `%` karakteri, büyük veri setlerinde yoğun işlem yüküne neden olabilir. Kontrolsüz sorgularda çok fazla `%` kullanımı, **ReDoS** (Regex Denial of Service) benzeri bir mantıkla veritabanını yavaşlatarak bir DoS saldırısına dönüşebilir.

> **Güvenlik İpucu:** Kullanıcıdan alınan verilerle asla doğrudan dinamik SQL sorgusu oluşturmayın. Her zaman "Prepared Statements" kullanarak operatörlerin sömürülmesini engelleyin.