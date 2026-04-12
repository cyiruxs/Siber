## SQL Nedir?

Şu ana kadar anlatılanların tamamı teorik olarak kulağa harika geliyor, peki pratikte veritabanları nasıl çalışır? İlk tablonuzu nasıl oluşturur ve onu verilerle nasıl doldurursunuz? Ne kullanırdınız? Veritabanları genellikle bir **Veritabanı Yönetim Sistemi (DBMS)** kullanılarak kontrol edilir. Son kullanıcı ile veritabanı arasında bir arayüz görevi gören DBMS; kullanıcıların depolanan verileri geri çağırmasına, güncellemesine ve yönetmesine olanak tanıyan bir yazılım programıdır. Bazı DBMS örnekleri arasında **MySQL, MongoDB, Oracle Database ve MariaDB** bulunur.

Son kullanıcı ile veritabanı arasındaki etkileşim **SQL (Structured Query Language - Yapılandırılmış Sorgu Dili)** kullanılarak yapılabilir. SQL, ilişkisel bir veritabanında depolanan verileri sorgulamak, tanımlamak ve işlemek için kullanılabilen bir programlama dilidir.

## SQL ve İlişkisel Veritabanlarının Avantajları

SQL, veritabanlarının kendisi kadar yaygındır ve bunun iyi bir sebebi vardır. İşte SQL öğrenmenin ve kullanmanın getirdiği bazı avantajlar:

- **Hızlıdır:** İlişkisel veritabanları (SQL'in kullanıldığı veritabanları), düşük depolama alanı kullanımı ve yüksek işlem hızları sayesinde devasa veri gruplarını neredeyse anında döndürebilir.
    
- **Öğrenmesi Kolaydır:** Birçok programlama dilinin aksine SQL, sade İngilizce ile yazılır ve bu da öğrenilmesini çok daha kolay hale getirir. Dilin yüksek okunabilirliği, kullanıcıların fonksiyonları ve sözdizimini (syntax) öğrenmeye odaklanabileceği anlamına gelir.
    
- **Güvenilirdir:** Daha önce belirtildiği gibi, ilişkisel veritabanları, veri setlerinin yerleştirilebilmesi için uyması gereken katı bir yapı tanımlayarak veri doğruluğunu garanti edebilir.
    
- **Esnektir:** SQL, bir veritabanını sorgulama konusunda her türlü yeteneği sağlar; bu da kullanıcıların geniş kapsamlı veri analizi görevlerini çok verimli bir şekilde gerçekleştirmesine olanak tanır.
    

---

## Uygulamaya Geçiş

SQL'in ne olduğunu ele aldığımıza göre, şimdi elleri kirletme ve SQL'i kendiniz kullanmaya başlama zamanı! Yeşil "Start Machine" butonuna tıklayın. Makine "Split-Screen" (Bölünmüş Ekran) görünümünde başlayacaktır. Sanal makine (VM) görünmüyorsa, sayfanın üst kısmındaki mavi "Show Split View" butonunu kullanın. Makine açılmayı bitirdiğinde terminali açın ve aşağıdaki komutu çalıştırın:

**MySQL Kurulumu**

`user@tryhackme$ mysql -u root -p`

Şifre istendiğinde şunu girin:

`tryhackme`

Çıktı aşağıdaki gibi görünmelidir:

SQL

```
user@tryhackme$ mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.39-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

Bunu da hallettiğimize göre, SQL kullanmaya (ve öğrenmeye) hazırsınız!

---

## 🛠 Ek Bilgiler ve Kavramlar

SQL öğrenirken veritabanı türlerini ve temel bileşenleri anlamak önemlidir.

## DBMS Türleri: İlişkisel (SQL) vs. İlişkisel Olmayan (NoSQL)

|**Özellik**|**İlişkisel (SQL)**|**İlişkisel Olmayan (NoSQL)**|
|---|---|---|
|**Veri Yapısı**|Tablo tabanlı (Satır & Sütun)|Doküman, Anahtar-Değer, Grafik|
|**Şema**|Sabit / Önceden Tanımlı|Dinamik / Esnek|
|**Örnekler**|MySQL, PostgreSQL, MSSQL|MongoDB, Cassandra, Redis|
|**Ölçeklenebilirlik**|Dikey (Donanımı artırma)|Yatay (Sunucu sayısını artırma)|

## Temel SQL Komut Grupları

SQL komutları genellikle işlevlerine göre dört ana gruba ayrılır:

1. **DDL (Data Definition Language):** Tablo ve veritabanı yapısını oluşturur (`CREATE`, `DROP`, `ALTER`).
    
2. **DML (Data Manipulation Language):** Veri üzerinde işlem yapar (`INSERT`, `UPDATE`, `DELETE`).
    
3. **DQL (Data Query Language):** Veri sorgulamak için kullanılır (`SELECT`).
    
4. **DCL (Data Control Language):** İzinleri yönetir (`GRANT`, `REVOKE`).
    

---

## 🚩 CTF & Siber Güvenlik İpuçları

SQL, siber güvenlik dünyasında en çok suistimal edilen alanlardan biridir. CTF (Capture The Flag) yarışmalarında ve sızma testlerinde şu noktalara dikkat etmelisiniz:

## 1. SQL Injection (SQLi) Nedir?

SQL Injection, bir saldırganın web uygulaması üzerinden veritabanı sorgularına müdahale etmesidir. Eğer uygulama kullanıcıdan aldığı veriyi temizlemeden (sanitizing) doğrudan SQL sorgusuna ekliyorsa, saldırgan veritabanındaki tüm bilgilere erişebilir.

**Örnek Açıklı Sorgu:**

`SELECT * FROM users WHERE username = '$user_input' AND password = '$password'`;

**Saldırı Senaryosu:**

Kullanıcı adı kısmına `' OR 1=1 --` yazılırsa, sorgu şuna dönüşür:

`SELECT * FROM users WHERE username = '' OR 1=1 --' AND password = '...'`;

`1=1` her zaman doğru olduğu için şifre kontrolü atlanır ve saldırgan giriş yapar.

## 2. Keşif (Enumeration) İpucu

Bir SQL terminaline eriştiğinizde (yukarıdaki gibi), veritabanlarını listelemek ve versiyon öğrenmek ilk adımınız olmalıdır:

- `SELECT version();` -> Veritabanı versiyonunu öğrenmek (Bilinen açıklıkları aramak için).
    
- `SHOW DATABASES;` -> Mevcut veritabanlarını listelemek.
    
- `SELECT user();` -> Hangi yetkilerle bağlı olduğunuzu görmek.
    

## 3. Bilgi Sızdırma (Data Exfiltration)

Sızma testlerinde `information_schema` veritabanı altın değerindedir. Bu veritabanı, diğer tüm tabloların ve sütunların isimlerini barındıran bir "metadata" deposudur.

> **Güvenlik Notu:** SQL enjeksiyonlarından korunmanın en etkili yolu **"Prepared Statements" (Parametreli Sorgular)** kullanmaktır.