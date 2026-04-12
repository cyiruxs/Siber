# Veritabanlarına Giriş (Introducing Databases)

Veritabanlarının ne kadar önemli olduğu size zaten söylenmişti. Şimdi, en başta ne olduklarını anlama zamanı. Giriş bölümünde belirtildiği gibi, veritabanları o kadar yaygındır ki, büyük olasılıkla onları kullanan sistemlerle sürekli etkileşim halindesinizdir. **Veritabanları, kolayca erişilebilen, üzerinde işlem yapılabilen veya analiz edilebilen yapılandırılmış bilgi veya verilerin düzenli bir koleksiyonudur.**

Bu veriler birçok formda olabilir:

- **Kullanıcı Kimlik Doğrulama Verileri:** Bir uygulamaya veya siteye (örneğin TryHackMe) giriş yaparken saklanan ve kontrol edilen kullanıcı adları ve şifreler.
    
- **Kullanıcı Tarafından Oluşturulan Veriler:** Instagram ve Facebook gibi sosyal medyalarda toplanan ve saklanan kullanıcı gönderileri, yorumlar, beğeniler vb.
    
- **İzleme Geçmişi Bilgileri:** Netflix gibi yayın servisleri tarafından saklanan ve öneriler oluşturmak için kullanılan veriler.
    

Meseleyi anladığınızdan eminim: Veritabanları yaygın olarak kullanılır ve birçok farklı şeyi içerebilir. Sadece devasa ölçekli işletmeler veritabanı kullanmaz. Küçük ölçekli işletmeler bile kurulum aşamasında verilerini saklamak için neredeyse kesinlikle bir veritabanı yapılandırmak zorunda kalacaktır. Veritabanı türlerinden bahsetmişken, şimdi bunların neler olduğuna bir göz atalım.

---

## Farklı Veritabanı Türleri (Different Types of Databases)

Bu kadar çok kişi tarafından ve (nispeten) bu kadar uzun süredir kullanılan bir şeyin birden fazla uygulama türü olması mantıklıdır. Oluşturulabilecek pek çok farklı veritabanı türü vardır, ancak bu giriş odasında iki ana türe odaklanacağız: **İlişkisel Veritabanları (Relational Databases - SQL)** ve **İlişkisel Olmayan Veritabanları (Non-relational Databases - NoSQL)**.

## 1. İlişkisel Veritabanları (Relational Databases - SQL)

Yapılandırılmış verileri saklarlar; yani bu veritabanına eklenen veriler belirli bir yapıyı takip eder. Örneğin, bir kullanıcı hakkında toplanan veriler `first_name`, `last_name`, `email_address`, `username` ve `password` alanlarından oluşur. Yeni bir kullanıcı katıldığında, bu yapıyı takip eden bir kayıt oluşturulur. Bu yapılandırılmış veriler bir tablodaki **satırlarda (rows)** ve **sütunlarda (columns)** saklanır; daha sonra iki veya daha fazla tablo (örneğin `user` ve `order_history`) arasında ilişkiler kurulabilir, bu yüzden "ilişkisel veritabanı" terimi kullanılır.

## 2. İlişkisel Olmayan Veritabanları (Non-relational Databases - NoSQL)

Verileri yukarıdaki yöntemin aksine, tablo olmayan (non-tabular) bir formatta saklarlar. Örneğin, değişen türde ve miktarda veri içerebilen taranmış belgeler, tablo dışı bir format gerektiren bir veritabanında saklanıyorsa bu yöntem kullanılır. İşte bunun nasıl görünebileceğine dair bir örnek:

JSON

```
 {
    _id: ObjectId("4556712cd2b2397ce1b47661"),
    name: { first: "Thomas", last: "Anderson" },
    date_of_birth: new Date('Sep 2, 1964'),
    occupation: [ "The One"],
    steps_taken : NumberLong(4738947387743977493)
 }
```

**Hangi veritabanı seçilmeli?** Bu her zaman veritabanının hangi bağlamda kullanılacağına bağlıdır:

- **İlişkisel (SQL):** Saklanan verilerin güvenilir bir şekilde tutarlı bir formatta alınacağı ve e-ticaret işlemleri gibi doğruluğun önemli olduğu durumlarda tercih edilir.
    
- **İlişkisel Olmayan (NoSQL):** Alınan verilerin formatı büyük ölçüde değişebiliyorsa ancak aynı yerde toplanıp düzenlenmesi gerekiyorsa (sosyal medya platformlarındaki kullanıcı içerikleri gibi) daha iyi bir seçimdir.
    

---

## Tablolar, Satırlar ve Sütunlar (Tables, Rows and Columns)

İki ana veritabanı türünü tanımladığımıza göre, ilişkisel veritabanlarına odaklanacağız. **Tablolar (tables)**, **satırlar (rows)** ve **sütunlar (columns)** kavramlarını açıklayarak başlayalım.

İlişkisel bir veritabanında saklanan tüm veriler bir **tabloda** tutulur; örneğin, bir kitapçıdaki stokta bulunan kitap koleksiyonu "Books" adlı bir tabloda saklanabilir.

1. **Sütunlar (Columns):** Bu tabloyu oluştururken, bir kitap kaydını tanımlamak için hangi bilgilerin gerektiğini belirlemeniz gerekir (örneğin: `id`, `Name`, `Published_date`). Bunlar sizin sütunlarınız olur. Sütunlar tanımlanırken, o sütunun hangi veri tipini içereceği de belirlenir. Eğer veri tipiyle eşleşmeyen bir kayıt eklenmeye çalışılırsa, bu reddedilir.
    
    - **Yaygın Veri Tipleri:** Strings (metinler), Integers (tam sayılar), Floats/Decimals (ondalıklı sayılar) ve Times/Dates (tarih/saat).
        
2. **Satırlar (Rows):** Sütunları tanımlanmış bir tablo oluşturulduktan sonra, veritabanına ilk kayıt eklenir. Örneğin; "id" değeri "1", ismi "Android Security Internals" ve yayın tarihi "2014-10-14" olan bir kitap. Bu kayıt, veritabanında bir **satır** olarak temsil edilir.
    

---

## Birincil ve Yabancı Anahtarlar (Primary and Foreign Keys)

Bir tablo tanımlanıp doldurulduktan sonra daha fazla veri saklanması gerekebilir. Örneğin, mağazada satılan kitapların yazarlarını saklayan "Authors" adlı bir tablo oluşturmak istiyoruz. Burada çok net bir ilişki vardır: Bir kitap (Books tablosunda saklanır), bir yazar (Authors tablosunda saklanır) tarafından yazılmıştır.

Veritabanında bir kitabı sorguladığımızda aynı zamanda o kitabın yazarının da dönmesini istiyorsak, verilerimizin bir şekilde ilişkilendirilmiş olması gerekir. Bunu **anahtarlar (keys)** ile yaparız:

|**Anahtar Türü**|**Açıklama**|
|---|---|
|**Birincil Anahtar (Primary Key)**|Belirli bir sütundaki verilerin **benzersiz (unique)** olmasını sağlar. Her kaydı tanımlayan eşsiz bir değerdir. Bir tabloda sadece bir tane olabilir.|
|**Yabancı Anahtar (Foreign Key)**|Bir tablodaki, başka bir tablonun birincil anahtarına karşılık gelen sütundur. Tablolar arasında **bağlantı/ilişki** kurmayı sağlar.|

- **Primary Key Örneği:** Üniversitedeki öğrenci numaralarını düşünün; bunlar öğrencileri benzersiz şekilde tanımlamak için atanır (çünkü bazen öğrencilerin isimleri aynı olabilir). Örneğimizde "id" sütunu birincil anahtar olarak en mantıklı seçimdir.
    
- **Foreign Key Örneği:** "Books" tablomuza bir "author_id" alanı eklediğimizi düşünün. Bu alan, "Authors" tablosundaki "id" sütununa karşılık geldiği için bir yabancı anahtar görevi görür. İlişkisel veritabanlarında tablolar arasındaki ilişkileri sağlayan şey budur. Bir tabloda birden fazla yabancı anahtar olabilir.
    

---

## 🚩 Siber Güvenlik Notları ve CTF İpuçları

Veritabanlarını anlamak, web güvenliği ve sızma testleri için kritiktir. İşte bu konuyla ilgili bilmeniz gereken bazı önemli noktalar:

## 💉 SQL Injection (SQLi) Nedir?

İlişkisel veritabanlarının en büyük düşmanı SQL Injection'dır. Eğer bir uygulama, kullanıcıdan aldığı veriyi doğrudan SQL sorgusuna dahil ederse, saldırgan kendi SQL komutlarını çalıştırabilir.

- **Örnek:** Giriş formuna `' OR 1=1 --` yazarak şifre bilmeden sisteme sızmak.
    
- **Savunma:** Her zaman "Parameterized Queries" (Parametreli Sorgular) veya "Prepared Statements" kullanın.
    

## 🔍 CTF İpucu: Veritabanı Keşfi

Bir sızma testi veya CTF sırasında, veritabanına erişim sağladığınızda ilk yapmanız gereken şey yapıyı anlamaktır:

1. **Tablo İsimlerini Listele:** Mevcut tabloları gör (`users`, `config`, `admin_credentials` gibi ilginç isimler ara).
    
2. **Sütunları İncele:** Hangi tabloda `password`, `hash` veya `token` sütunu olduğunu bul.
    
3. **İlişkileri Takip Et:** Foreign Key'leri kullanarak kullanıcıların rollerini (admin, user vb.) hangi tabloların belirlediğini çöz.
    

## 🛡️ Veritabanı Sıkılaştırma (Hardening)

- **Default Şifreler:** Veritabanı kurulduğunda gelen varsayılan (default) kullanıcı adlarını (örn: `sa`, `root`, `postgres`) ve şifreleri mutlaka değiştirin.
    
- **En Az Yetki İlkesi (Principle of Least Privilege):** Uygulamanın veritabanı kullanıcısı sadece ihtiyacı olan tablolara erişebilmeli; `DROP TABLE` gibi yetkileri olmamalıdır.