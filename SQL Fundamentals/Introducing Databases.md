# 🗄️ Veritabanlarına Giriş

Veritabanlarının ne kadar önemli olduğunu biliyorsunuz; şimdi bunların tam olarak ne olduğunu anlama zamanı. Giriş bölümünde belirtildiği gibi, veritabanları o kadar yaygındır ki, muhtemelen onlarla çalışan sistemlerle sürekli etkileşim halindesinizdir. **Databases** (veritabanları), kolayca erişilebilen, manipüle edilebilen veya analiz edilebilen, organize edilmiş yapılandırılmış bilgi veya veri koleksiyonudur.

Bu veriler birçok formda olabilir:

- **User Authentication Data:** Bir uygulamaya veya siteye (örneğin TryHackMe) giriş yaparken doğrulanan kullanıcı adları ve şifreler.
    
- **User-generated Data:** Instagram ve Facebook gibi sosyal medyalarda toplanan gönderiler, yorumlar ve beğeniler.
    
- **Usage History:** Netflix gibi yayın servisleri tarafından öneriler oluşturmak için saklanan izleme geçmişi.
    

Veritabanları sadece devasa ölçekli işletmeler tarafından değil, kurulum aşamasındaki küçük ölçekli işletmeler tarafından da verilerini depolamak için mutlaka yapılandırılır.

---

## 🏗️ Farklı Veritabanı Türleri (Different Types of Databases)

Bu kadar uzun süredir ve bu kadar çok kişi tarafından kullanılması, birden fazla uygulama türünün ortaya çıkmasına neden olmuştur. Birçok farklı tür olsa da, bu giriş seviyesindeki odada iki ana türe odaklanacağız: **Relational Databases (aka SQL)** ve **Non-relational Databases (aka NoSQL)**.

### 1. Relational Databases (İlişkisel Veritabanları)

Yapılandırılmış verileri (**structured data**) saklar; yani bu veritabanına eklenen veriler belirli bir yapıyı takip eder. Örneğin; bir kullanıcı için toplanan veriler `first_name`, `last_name`, `email_address`, `username` ve `password` bilgilerinden oluşur. Yeni bir kullanıcı katıldığında, veritabanında bu yapıya uygun bir girdi oluşturulur.

- Veriler bir tablodaki **rows** (satırlar) ve **columns** (sütunlar) şeklinde saklanır.
    
- İki veya daha fazla tablo arasında (örneğin `user` ve `order_history`) ilişkiler kurulabilir.
    

### 2. Non-relational Databases (İlişkisel Olmayan Veritabanları)

Verileri yukarıdaki yöntemin aksine, tablo olmayan (**non-tabular**) bir formatta saklar. Örneğin, farklı türde ve miktarda veri içerebilen taranmış belgeler bu formatta saklanır. İşte bir örnek:

> **Hangi Veritabanı Seçilmeli?** Bu, verinin kullanılacağı bağlama bağlıdır. **Relational Databases**, e-ticaret işlemleri gibi doğruluğun kritik olduğu ve verinin tutarlı bir formatta geldiği durumlarda tercih edilir. **Non-relational Databases** ise sosyal medya platformlarındaki kullanıcı içerikleri gibi, formatı büyük ölçüde değişebilen verilerin aynı yerde toplanması gerektiğinde daha uygundur.

---

## 📊 Tablolar, Satırlar ve Sütunlar (Tables, Rows and Columns)

İlişkisel veritabanlarında tüm veriler bir **table** (tablo) içinde saklanır. Örneğin bir kitapçıdaki kitap koleksiyonu "Books" adlı bir tabloda tutulabilir.

- **Columns (Sütunlar):** Tabloyu oluştururken bir kitap kaydını tanımlamak için hangi bilgilere ihtiyacınız olduğunu belirlemeniz gerekir (örneğin: `id`, `Name`, `Published_date`).
    
- **Data Types:** Sütunlar tanımlanırken, içerecekleri veri tipi de belirlenir (**Strings**, **Integers**, **Floats/Decimals**, **Times/Dates**). Eğer veri tipi eşleşmeyen bir kayıt eklenmeye çalışılırsa, veritabanı bunu reddeder.
    
- **Rows (Satırlar):** Tablo oluşturulduktan sonra eklenen her bir tam kayıt (örneğin: id="1", Name="Android Security Internals", Date="2014-10-14") bir satır olarak temsil edilir.
    

---

## 🔑 Primary ve Foreign Keys (Birincil ve Yabancı Anahtarlar)

Veriler arasındaki ilişkileri kurmak için "anahtarlar" kullanılır:

1. **Primary Keys (Birincil Anahtarlar):** Belirli bir sütundaki verilerin benzersiz (**unique**) olmasını sağlar. Tablodaki her kaydı tek başına tanımlayan, başka hiçbir kayıtta tekrar etmeyen bir değerdir (Üniversite öğrenci numaraları gibi). Bir tabloda yalnızca **bir adet** Primary Key olabilir. Örneğimizde `id` sütunu en mantıklı seçimdir.
    
2. **Foreign Keys (Yabancı Anahtarlar):** Bir tabloda bulunan ve başka bir tablodaki sütunla eşleşen, dolayısıyla iki tablo arasında bağlantı sağlayan sütunlardır.
    
    - _Örnek:_ "Books" tablosuna bir `author_id` alanı eklersek, bu alan "Authors" tablosundaki `id` sütununa karşılık geldiği için bir **Foreign Key** görevi görür. İlişkisel veritabanlarında tablolar arası bağlantıyı bu sağlar.
        

---

## 🛡️ Siber Güvenlik ve CTF İpuçları: Veritabanı Güvenliği

### 1. SQL Injection (SQLi) Nedir?

İlişkisel veritabanlarının en büyük düşmanı **SQL Injection**'dır. Eğer bir uygulama kullanıcıdan aldığı veriyi doğrudan SQL sorgusuna dahil ederse, saldırgan veritabanı üzerinde yetkisiz işlemler yapabilir.

### 💡 CTF İpucu: Anahtarların Takibi

Bir CTF senaryosunda birden fazla tablo bulduğunuzda, aralarındaki ilişkiyi çözmek için **Foreign Key**'leri takip edin. Örneğin `Orders` tablosunda `user_id` varsa, bu sizi kullanıcıların bilgilerinin (belki de şifrelerinin) olduğu `Users` tablosuna götürecektir.

> **Güvenlik Notu:** Veritabanı şemalarınızı tasarlarken "Least Privilege" (En Az Yetki) prensibini uygulayın. Uygulamanızın veritabanı kullanıcısı, asla tüm veritabanını silme (`DROP`) yetkisine sahip olmamalıdır.