## SQL Yancümleleri (Clauses)

Bir **clause (yancümle)**, genellikle bir başlangıç ifadesi tarafından manipüle edilen verilerin kriterlerini belirten ifadenin bir parçasıdır. Yancümleler, veri tipini tanımlamamıza ve verilerin nasıl getirilmesi veya sıralanması gerektiğini belirlememize yardımcı olur.

Önceki görevlerde, hangi tabloya eriştiğimizi belirten `FROM` ve hangi kayıtların kullanılacağını belirten `WHERE` gibi bazı yancümleleri zaten kullanmıştık. Bu görev şu yancümlelere odaklanacaktır: **DISTINCT, GROUP BY, ORDER BY ve HAVING.**

`thm_books` veritabanını kullanmak için: `USE thm_books;`

---

## 1. DISTINCT Yancümlesi

`DISTINCT` yancümlesi, bir sorgu yaparken yinelenen kayıtları önlemek ve yalnızca benzersiz (unique) değerleri döndürmek için kullanılır.

**Normal Sorgu:**

SQL

```
mysql> SELECT * FROM books;
+----+----------------------------+----------------+--------------------------------------------------------+
| id | name                       | published_date | description                                            |
+----+----------------------------+----------------+--------------------------------------------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture   |
|  5 | Ethical Hacking            | 2021-11-02     | A Hands-on Introduction to Breaking In                 |
|  6 | Ethical Hacking            | 2021-11-02     |                                                        |
+----+----------------------------+----------------+--------------------------------------------------------+
```

_Not: `Ethical Hacking` kaydı iki kez görüntülenir._

**DISTINCT Kullanımı:**

SQL

```
mysql> SELECT DISTINCT name FROM books;
+----------------------------+
| name                       |
+----------------------------+
| Android Security Internals |
| Ethical Hacking            |
+----------------------------+
```

Çıktı, `Ethical Hacking` kaydının sadece bir örneğini görüntüler.

---

## 2. GROUP BY Yancümlesi

`GROUP BY` yancümlesi, birden fazla kayıttan gelen verileri bir araya getirir (toplar) ve sorgu sonuçlarını sütunlar halinde gruplandırır. Toplama (aggregate) fonksiyonları ile kullanılır.

SQL

```
mysql> SELECT name, COUNT(*)
    FROM books
    GROUP BY name;
+----------------------------+----------+
| name                       | COUNT(*) |
+----------------------------+----------+
| Ethical Hacking            |        2 |
+----------------------------+----------+
```

Burada `Ethical Hacking` ismiyle gruplandırma yapılmış ve bu isimden 2 adet olduğu `COUNT(*)` ile sayılmıştır.

---

## 3. ORDER BY Yancümlesi

Kayıtları artan (`ASC`) veya azalan (`DESC`) düzende sıralamak için kullanılır.

- **ASC (Artan):** `ORDER BY published_date ASC;` (Eskiden yeniye)
    
- **DESC (Azalan):** `ORDER BY published_date DESC;` (Yeniden eskiye)
    

---

## 4. HAVING Yancümlesi

`HAVING`, gruplandırılmış verileri filtrelemek için kullanılır. `WHERE` satırları filtrelerken, `HAVING` toplama işlemi yapıldıktan sonraki sonuçları filtreler.

SQL

```
mysql> SELECT name, COUNT(*)
    FROM books
    GROUP BY name
    HAVING name LIKE '%Hack%';
```

---

## 🛠 Ek Bilgiler ve Kavramlar

SQL sorgularında yancümlelerin yazım sırası ile arka planda işlenme sırası farklıdır. Bu durum "Logical Query Processing" olarak bilinir.

## SQL Sorgu Yürütme Sırası

|**Sıra**|**Komut**|**İşlem**|
|---|---|---|
|1|**FROM**|Hedef tablo belirlenir.|
|2|**WHERE**|Satırlar filtrelenir (Ham veri).|
|3|**GROUP BY**|Veriler gruplara ayrılır.|
|4|**HAVING**|Gruplanmış sonuçlar filtrelenir.|
|5|**SELECT**|Hangi sütunların görüneceği seçilir.|
|6|**ORDER BY**|Sonuçlar sıralanır.|

## Toplama Fonksiyonları (Aggregate Functions)

- **COUNT():** Satır sayısı.
    
- **SUM():** Toplam değer.
    
- **AVG():** Ortalama.
    
- **MAX() / MIN():** En yüksek / En düşük değer.
    

---

## 🚩 CTF & Siber Güvenlik İpuçları

Yancümleler, sızma testlerinde veritabanı yapısını anlamak (enumeration) için kritik araçlardır.

## 1. Keşif: DISTINCT ve Veri Gizliliği

Bir saldırgan, `DISTINCT` kullanarak sistemdeki benzersiz yetki seviyelerini veya gizli departmanları keşfedebilir:

`SELECT DISTINCT role FROM users;`

Bu, hangi kullanıcıların "admin" veya "superuser" yetkisine sahip olabileceğini anlamanızı sağlar.

## 2. Sızma: ORDER BY ile Sütun Sayısı Tespiti

**SQL Injection (SQLi)** saldırılarında en yaygın tekniklerden biri `ORDER BY` kullanmaktır.

- `ORDER BY 1`, `ORDER BY 2` derken hata alana kadar devam edilir.
    
- Eğer `ORDER BY 5` çalışıyor ama `ORDER BY 6` hata veriyorsa, tablonun **5 sütunu** olduğunu anlarsınız. Bu bilgi `UNION SELECT` saldırısı için gereklidir.
    

## 3. Analiz: GROUP BY ve HAVING ile Anomali Tespiti

Siber güvenlik analistleri Brute Force saldırılarını bu şekilde yakalar:

`SELECT IP_Address, COUNT(*) FROM logins GROUP BY IP_Address HAVING COUNT(*) > 50;`

Bu sorgu, tek bir IP'den gelen 50'den fazla başarısız giriş denemesini anında raporlar.

## 4. LIKE Operatörü ve Joker Karakterler

`%` karakteri jokerdir:

- `Hack%`: "Hack" ile başlayanlar.
    
- `%Hack%`: İçinde "Hack" geçen her şey.
    
    **CTF İpucu:** Eğer bayrak formatını biliyorsanız, veritabanında şöyle arama yapabilirsiniz:
    
    `SELECT flag FROM secrets WHERE flag LIKE 'THM{%';`