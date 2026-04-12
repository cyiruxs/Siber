**CRUD**, veri yöneten her sistemdeki temel işlemler olarak kabul edilen **Create (Oluştur)**, **Read (Oku)**, **Update (Güncelle)** ve **Delete (Sil)** kelimelerinin baş harflerinden oluşur.

MySQL ile çalışırken bu farklı işlemlerin tümünü keşfedelim. Sonraki iki görevde, `thm_books` veritabanının bir parçası olan `books` tablosunu kullanacağız. Bu tabloya `USE thm_books;` ifadesi ile erişebiliriz.

## Oluşturma İşlemi (INSERT)

**Create (Oluşturma)** işlemi, bir tabloda yeni kayıtlar oluşturur. MySQL'de bu, aşağıda gösterildiği gibi `INSERT INTO` ifadesi kullanılarak gerçekleştirilebilir.

**Terminal**

SQL

```
mysql> INSERT INTO books (id, name, published_date, description)
    VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");

Query OK, 1 row affected (0.01 sec)
```

Gözlemleyebileceğimiz gibi, `INSERT INTO` ifadesi yeni bir kayıt ekleyebileceğiniz bir tabloyu (bu durumda `books`) belirtir; `id`, `name`, `published_date` ve `description` sütunları tablodaki kayıtlardır. Bu örnekte; `id` değeri `1`, `name` değeri `"Android Security Internals"`, `published_date` değeri `"2014-10-14"` ve `description` değeri `"Android Security Internals provides a complete understanding of the security internals of Android devices"` olan yeni bir kayıt eklenmiştir.

**Not:** Bu işlem veritabanında zaten mevcuttur, bu nedenle sorguyu çalıştırmanıza gerek yoktur.

---

## Okuma İşlemi (SELECT)

**Read (Okuma)** işlemi, adından da anlaşılacağı üzere bir tablodan bilgi okumak veya geri çağırmak için kullanılır. Bir tablodan belirli bir sütunu veya tüm sütunları, sonraki örnekte gösterildiği gibi `SELECT` ifadesiyle çekebiliriz.

**Terminal**

SQL

```
mysql> SELECT * FROM books;
+----+----------------------------+----------------+------------------------------------------------------+
| id | name                       | published_date | description                                          |
+----+----------------------------+----------------+------------------------------------------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture |
+----+----------------------------+----------------+------------------------------------------------------+

1 row in set (0.00 sec)
```

Yukarıdaki çıktıda `SELECT` ifadesini, tüm sütunların geri çağrılması gerektiğini belirten `*` sembolü takip eder; ardından `FROM` yan tümcesi ve tablo adı (bu durumda `books`) gelir.

Eğer `name` ve `description` gibi belirli bir sütunu seçmek istiyorsak, aşağıda gösterildiği gibi `*` sembolü yerine bunları belirtmelisiniz.

**Terminal**

SQL

```
mysql> SELECT name, description FROM books;
+----------------------------+------------------------------------------------------+
| name                       | description                                          |
+----------------------------+------------------------------------------------------+
| Android Security Internals | An In-Depth Guide to Android's Security Architecture |
+----------------------------+------------------------------------------------------+

1 row in set (0.00 sec)
```

---

## Güncelleme İşlemi (UPDATE)

**Update (Güncelleme)** işlemi, tablo içindeki mevcut bir kaydı değiştirir ve bunun için aynı isimdeki `UPDATE` ifadesi kullanılabilir.

**Terminal**

SQL

```
mysql> UPDATE books
    SET description = "An In-Depth Guide to Android's Security Architecture."
    WHERE id = 1;

Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

`UPDATE` ifadesi tabloyu (bu durumda `books`) belirtir ve ardından güncelleyeceğimiz sütun adını takip eden `SET` ifadesini kullanabiliriz. `WHERE` yan tümcesi, koşul karşılandığında hangi satırın güncelleneceğini belirtir; bu durumda `id` değeri `1` olan satırdır.

---

## Silme İşlemi (DELETE)

**Delete (Silme)** işlemi, bir tablodan kayıtları kaldırır. Bunu `DELETE` ifadesiyle başarabiliriz.

**Not:** Bu sorguyu çalıştırmanıza gerek yoktur. Bu girişin silinmesi, gelecek görevlerdeki örneklerin geri kalanını etkileyecektir.

**Terminal**

SQL

```
mysql> DELETE FROM books WHERE id = 1;

Query OK, 1 row affected (0.00 sec)
```

Yukarıda, kaydın kaldırılacağı tabloyu (bu durumda `books`) belirtmemize olanak tanıyan `FROM` yan tümcesinin takip ettiği `DELETE` ifadesini ve ardından `id` değerinin `1` olduğu satırı işaret eden `WHERE` yan tümcesini gözlemleyebiliriz.

---

## Özet

Özetle, **CRUD** işlemleri veri operasyonları ve veritabanlarıyla etkileşim kurarken temeldir. Bunlarla ilişkili ifadeler aşağıda listelenmiştir:

- **Create (INSERT ifadesi):** Tabloya yeni bir kayıt ekler.
    
- **Read (SELECT ifadesi):** Tablodan kayıtları geri çağırır.
    
- **Update (UPDATE ifadesi):** Tablodaki mevcut veriyi değiştirir.
    
- **Delete (DELETE ifadesi):** Tablodan kaydı kaldırır.
    

Bu işlemler, bir veritabanı içindeki verileri etkili bir şekilde yönetmemizi ve manipüle etmemizi sağlar.

---

## 🛠 Ek Bilgiler ve Kavramlar

CRUD döngüsü, modern uygulama geliştirmenin kalbidir.

## SQL İşlemlerinin Görsel Karşılığı

|**İşlem**|**SQL Komutu**|**HTTP Metodu (API)**|**Açıklama**|
|---|---|---|---|
|**C**reate|`INSERT`|POST|Yeni veri girişi.|
|**R**ead|`SELECT`|GET|Mevcut veriyi görüntüleme.|
|**U**pdate|`UPDATE`|PUT/PATCH|Veri üzerinde değişiklik yapma.|
|**D**elete|`DELETE`|DELETE|Veriyi kalıcı olarak kaldırma.|

---

## 🚩 CTF & Siber Güvenlik İpuçları

Güvenlik perspektifinden bakıldığında, her CRUD işlemi farklı riskler ve fırsatlar taşır.

## 1. SELECT: Hassas Veri Sızıntısı (Insecure Direct Object Reference - IDOR)

Bir web uygulamasında `SELECT * FROM users WHERE id = [USER_ID]` şeklinde bir sorgu olduğunu düşünün. Eğer uygulama `USER_ID` kısmını yetkilendirme kontrolü yapmadan kullanıcıdan alıyorsa, bir kullanıcı kendi ID'si yerine başkasınınkini yazarak (IDOR saldırısı) tüm kullanıcı verilerini okuyabilir (`Read`).

## 2. INSERT: İkinci Derece SQL Enjeksiyonu (Second-Order SQLi)

Bir saldırgan, `INSERT` işlemi sırasında veritabanına zararlı bir payload yükleyebilir (örneğin kullanıcı adı olarak `' OR 1=1 --`). Bu veri kaydedilirken bir sorun çıkarmaz, ancak uygulama daha sonra bu veriyi bir `SELECT` veya `UPDATE` sorgusunda kullandığında zararlı kod tetiklenir.

## 3. UPDATE: Toplu Veri Değiştirme Riski

`UPDATE` sorgularında `WHERE` yan tümcesini unutmak veya yanlış yapılandırmak siber güvenlikte felakete yol açabilir.

> **Saldırı Senaryosu:** `UPDATE users SET password = 'hacked_password'` (Eğer `WHERE` yoksa tüm kullanıcıların şifresi değişir!)
> 
> CTF'lerde admin şifresini bilmediğiniz bir sistemde, kendi yetkinizle admin tablosunu güncelleyip güncelleyemediğinizi test etmek (`Update`) kritik bir adımdır.

## 4. DELETE: Hizmet Dışı Bırakma (DoS)

Yetkisiz bir `DELETE` işlemi, sistemin çalışması için kritik olan verilerin silinmesine ve uygulamanın çökmesine neden olabilir. Bir CTF senaryosunda, log tablolarını silerek izlerinizi yok etmek (`Delete`) sızma sonrası (post-exploitation) aşaması için önemlidir.

> **Güvenlik Altın Kuralı:** SQL sorgularında her zaman en kısıtlayıcı `WHERE` koşullarını kullanın ve kullanıcıdan gelen veriye asla güvenmeyin.