Şimdi işin eğlenceli kısmı! SQL öğrenmeye ve veritabanlarıyla etkileşim kurmak için onu nasıl kullanacağımıza başlama zamanı. Bu görevde, veritabanı ve tablo ifadelerini öğrenerek başlayacağız. Ne de olsa, veritabanlarımızı/tablolarımızı başlangıçta oluşturmak ve işe koyulmak için bu ifadelere ihtiyacımız var.

## Veritabanı İfadeleri (Database Statements)

#### CREATE DATABASE

Eğer yeni bir veritabanına ihtiyaç duyulursa, atacağınız ilk adım onu oluşturmaktır. Bu, SQL'de `CREATE DATABASE` ifadesi kullanılarak yapılabilir. Bu işlem şu sözdizimi (syntax) kullanılarak yapılır:

**Terminal**

`mysql> CREATE DATABASE veritabanı_adı;`

`thm_bookmarket_db` adında bir veritabanı oluşturmak için aşağıdaki komutu çalıştırın:

**Terminal**

`mysql> CREATE DATABASE thm_bookmarket_db;`

#### SHOW DATABASES

Bir veritabanı oluşturduğumuza göre, `SHOW DATABASES` ifadesini kullanarak onu görüntüleyebiliriz. `SHOW DATABASES` ifadesi mevcut veritabanlarının bir listesini döndürecektir. İfadeyi şu şekilde çalıştırın:

**Terminal**

`mysql> SHOW DATABASES;`

Dönen listede, az önce oluşturduğunuz veritabanını ve MySQL'in çalışmasını sağlayan çeşitli amaçlar için kullanılan, varsayılan olarak dahil edilmiş bazı veritabanlarını (`mysql`, `information_schema`, `performance_schema` ve `sys`) görmelisiniz. Ayrıca bu ders için gerekli olan çeşitli tablolar da mevcuttur.

#### USE DATABASE

Bir veritabanı oluşturulduktan sonra onunla etkileşime girmek isteyebilirsiniz. Etkileşime girmeden önce, MySQL'e hangi veritabanı ile etkileşime girmek istediğimizi söylememiz gerekir (böylece sonraki sorguları hangi veritabanına karşı çalıştıracağını bilir). Az önce oluşturduğumuz veritabanını aktif veritabanı olarak ayarlamak için `USE` ifadesini şu şekilde çalıştırırız (bunu kendi makinenizde çalıştırdığınızdan emin olun):

**Terminal**

`mysql> USE thm_bookmarket_db;`

#### DROP DATABASE

Bir veritabanına artık ihtiyaç duyulmadığında (belki test amaçlı oluşturulmuştur veya artık gerekli değildir), `DROP` ifadesi kullanılarak kaldırılabilir. Bir veritabanını kaldırmak için aşağıdaki ifade sözdizimini kullanırız (ancak bizim durumumuzda veritabanımızı tutmak istiyoruz, bu yüzden bunu kendiniz çalıştırmanıza gerek yok!):

**Terminal**

`mysql> DROP DATABASE veritabanı_adı;`

---

## Tablo İfadeleri (Table Statements)

Artık veritabanlarını oluşturabildiğinize, listeleyebildiğinize, kullanabildiğinize ve kaldırabildiğinize göre, bu veritabanlarını tablolarla nasıl dolduracağımızı ve bu tablolarla nasıl etkileşim kuracağımızı inceleme zamanı.

#### CREATE TABLE

Veritabanı ifadelerinin mantığını takip ederek, tablolar oluşturmak da bir `CREATE` ifadesi kullanır. Bir veritabanı aktif olduğunda (üzerinde `USE` ifadesini çalıştırdığınızda), içinde aşağıdaki ifade sözdizimi kullanılarak bir tablo oluşturulabilir:

**Terminal**

SQL

```
mysql> CREATE TABLE ornek_tablo_adi (
    ornek_sutun1 veri_tipi,
    ornek_sutun2 veri_tipi,
    ornek_sutun3 veri_tipi
);
```

Gördüğünüz gibi, burada biraz daha fazla detay var. "Databases 101" görevinde bir tablonun nasıl ve ne zaman oluşturulduğunu ele almıştık; o tablodaki bir kaydı hangi sütunların oluşturacağına ve o sütunda hangi veri tipinin bulunmasının beklendiğine karar verilmelidir. Bu sözdiziminin burada temsil ettiği şey budur. Örnekte 3 örnek sütun vardır, ancak SQL çok daha fazlasını (1000'den fazla) destekler. `thm_bookmarket_db` veritabanımızı aşağıdaki ifadeyi kullanarak bir tablo ile doldurmayı deneyelim:

**Terminal**

SQL

```
mysql> CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);
```

Bu ifade, üç sütunlu bir `book_inventory` tablosu oluşturacaktır: `book_id`, `book_name` ve `publication_date`. `book_id` bir `INT` (Tam Sayı) türündedir çünkü her zaman sadece bir sayı olmalıdır; `AUTO_INCREMENT` mevcuttur, yani eklenen ilk kitaba 1, ikinci kitaba 2 vb. `book_id` atanacaktır. Son olarak `book_id`, tablomuzdaki bir kitap kaydını benzersiz bir şekilde tanımlama yolumuz olacağı için `PRIMARY KEY` (Birincil Anahtar) olarak ayarlanmıştır (ve bir tabloda bir birincil anahtar bulunmalıdır).

`book_name`, `VARCHAR(255)` veri tipine sahiptir, yani değişken karakterler (metin/sayılar/noktalama işaretleri) kullanabilir ve 255 karakterlik bir sınır belirlenmiştir; ayrıca `NOT NULL` olarak ayarlanmıştır, yani boş olamaz (bu nedenle birisi bu tabloya bir kayıt eklemeye çalışırsa ancak `book_name` boşsa bu reddedilir). `publication_date` ise `DATE` veri tipi olarak ayarlanmıştır.

#### SHOW TABLES

Veritabanlarını bir `SHOW` ifadesi kullanarak listeleyebildiğimiz gibi, şu anda aktif olan veritabanındaki (en son üzerinde `USE` ifadesini kullandığımız veritabanı) tabloları da listeleyebiliriz. Aşağıdaki komutu çalıştırın; az önce oluşturduğunuz tabloyu görmelisiniz:

**Terminal**

`mysql> SHOW TABLES;`

#### DESCRIBE

Bir tablonun hangi sütunları içerdiğini (ve veri tiplerini) bilmek istersek, onları `DESCRIBE` komutunu (ayrıca `DESC` olarak da kısaltılabilir) kullanarak tanımlayabiliriz. Az önce oluşturduğunuz tabloyu aşağıdaki komutu kullanarak tanımlayın:

**Terminal**

`mysql> DESCRIBE book_inventory;`

Bu size tablonun detaylı bir görünümünü şu şekilde verecektir:

**DROP Sözdizimi**

SQL

```
mysql> DESCRIBE book_inventory;
+------------------+--------------+------+-----+---------+----------------+
| Field            | Type         | Null | Key | Default | Extra          |
+------------------+--------------+------+-----+---------+----------------+
| book_id          | int          | NO   | PRI | NULL    | auto_increment |
| book_name        | varchar(255) | NO   |     | NULL    |                |
| publication_date | date         | YES  |     | NULL    |                |
+------------------+--------------+------+-----+---------+----------------+
3 rows in set (0.02 sec)
```

#### ALTER

Bir tablo oluşturduktan sonra, veri seti ihtiyacınızın değiştiği ve tabloyu değiştirmeniz gereken bir zaman gelebilir. Bu, `ALTER` ifadesi kullanılarak yapılabilir. Şimdi, kitap envanterimizde her kitap için sayfa sayısının yer aldığı bir sütun olmasını istediğimize karar verdiğimizi düşünelim. Bunu aşağıdaki ifadeyi kullanarak tablomuza ekleyin:

**Terminal**

SQL

```
mysql> ALTER TABLE book_inventory
ADD page_count INT;
```

`ALTER` ifadesi; sütunları yeniden adlandırmak, bir sütundaki veri tipini değiştirmek veya bir sütunu kaldırmak gibi tablo üzerinde değişiklikler yapmak için kullanılabilir.

#### DROP

Bir veritabanını kaldırmaya benzer şekilde, `DROP` ifadesini kullanarak tabloları da kaldırabilirsiniz. Bunu yapmamıza gerek yok, ancak bunun için kullanacağınız sözdizimi şudur:

**Terminal**

`mysql> DROP TABLE tablo_adı;`

---

## 🛠 Ek Bilgiler ve Kavramlar

SQL veritabanı yönetiminde veri tiplerini anlamak, veritabanı mimarisinin temelidir.

## Sık Kullanılan Veri Tipleri (Data Types)

|**Veri Tipi**|**Açıklama**|**Örnek Kullanım**|
|---|---|---|
|**INT**|Tam sayılar için kullanılır.|`yaş`, `stok_miktarı`|
|**VARCHAR(n)**|Belirtilen `n` uzunluğuna kadar değişken metinler.|`isim`, `e_posta`|
|**TEXT**|Çok uzun metin verileri için kullanılır.|`blog_yazısı`, `ürün_açıklaması`|
|**DATE**|YYYY-MM-DD formatında tarihler.|`doğum_tarihi`|
|**BOOLEAN**|Doğru (1) veya Yanlış (0) değerleri.|`aktif_mi`, `ödendi_mi`|

---

## 🚩 CTF & Siber Güvenlik İpuçları

Veritabanı keşfi (Enumeration), bir sızma testinin veya CTF çözümünün en kritik aşamalarından biridir.

## 1. Veritabanı Parmak İzi Alma (Fingerprinting)

`SHOW DATABASES;` komutunu kullandığınızda, varsayılan tablolar size hangi DBMS'in kullanıldığına dair ipucu verir:

- **`information_schema`**: Neredeyse tüm modern ilişkisel veritabanlarında bulunur (MySQL, MariaDB, PostgreSQL).
    
- **`msdb` veya `tempdb`**: Microsoft SQL Server (MSSQL) belirtisidir.
    
- **`dual` tablosu**: Genellikle Oracle Database ile ilişkilendirilir.
    

## 2. Tablo Yapısı Neden Önemlidir?

Siber güvenlik açısından `DESCRIBE` komutu hayati önem taşır. Bir saldırgan tablo yapısını öğrendiğinde:

- Hangi sütunların `NOT NULL` olduğunu bilerek "SQL Injection" ile veri girişi yaparken hata almamayı sağlar.
    
- `PRIMARY KEY` olan sütunları hedef alarak veri sızıntısını (Data Leakage) sistematik hale getirir.
    

## 3. Kritik Sütunları Aramak

Tabloları listeledikten sonra (`SHOW TABLES;`), şu isimlere sahip tablolar her zaman önceliklidir:

- `users`, `admin`, `config`, `credentials`, `backups`.
    
    Bu tablolarda genellikle `password`, `hash`, `email` veya `session_id` gibi hassas sütunlar aranır.
    

## 4. Bilgi Sızdırma (Extraction) Pratiği

Eğer bir SQL enjeksiyonu üzerinden veritabanı adını öğrenmek isterseniz, SQL şu fonksiyonları sağlar:

- `SELECT DATABASE();` -> Mevcut kullanılan veritabanı adını döndürür.
    
- `SELECT USER();` -> Veritabanına bağlanan mevcut kullanıcıyı döndürür (Örn: `root@localhost`).
    

> **İpucu:** Gerçek dünya senaryolarında, veritabanı şemasını görselleştirmek saldırı yüzeyini anlamanızı kolaylaştırır.