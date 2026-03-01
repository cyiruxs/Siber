**Veritabanları**, kolayca erişilebilen ve üzerinde işlem yapılabilen veya analiz edilebilen organize edilmiş veri veya bilgi koleksiyonlarıdır.

İki ana veritabanı türü; **ilişkisel veritabanları** (yapılandırılmış verileri depolamak için kullanılır) ve **ilişkisel olmayan veritabanlarıdır** (verileri tablo olmayan bir formatta depolamak için kullanılır).

İlişkisel veritabanları **Tablolar, sütunlar ve satırlardan** oluşur. **Birincil anahtarlar (Primary keys)** bir kaydın tablo içinde benzersiz olmasını sağlayabilir ve **yabancı anahtarlar (foreign keys)** iki (veya daha fazla) tablo arasında bir ilişki/bağlantı kurulmasına izin verebilir.

**SQL**, ilişkisel veritabanlarıyla etkileşim kurmak için kullanılabilen, öğrenmesi kolay bir programlama dilidir.

**Veritabanı ve Tablo ifadeleri (Database and Table statements)**, veritabanlarını ve tabloları oluşturmak/yönetmek için kullanılabilir.

**CRUD İşlemleri (INSERT, SELECT, UPDATE ve DELETE)**, bir veritabanındaki verileri yönetmek için kullanılabilir.

**SQL'de**, verilerin nasıl geri çağrılacağını, filtreleneceğini, sıralanacağını veya gruplandırılacağını tanımlamak için **yancümleler (clauses)** kullanabiliriz.

**Operatörlerin** ve **fonksiyonların** verimli kullanımı, SQL'de verileri filtrelememize ve manipüle etmemize yardımcı olabilir.

---

## 🛠 Ek Bilgiler ve Kavramlar

Bu özet, modern veri yönetiminin temel direklerini kapsamaktadır.

## Veritabanı Mimarisi Görseli

## İlişkisel vs. NoSQL Karşılaştırması

|**Özellik**|**İlişkisel (SQL)**|**İlişkisel Olmayan (NoSQL)**|
|---|---|---|
|**Veri Modeli**|Tablo (Satır/Sütun)|Doküman, Graf, Anahtar-Değer|
|**Şema**|Sabit (Önceden tanımlı)|Dinamik (Esnek)|
|**İlişkiler**|Karmaşık JOIN işlemleri|Genellikle iç içe geçmiş veriler|

---

## 🚩 CTF & Siber Güvenlik İpuçları

Siber güvenlik perspektifinden, bu temel bileşenlerin her biri bir saldırı yüzeyi veya bir savunma hattıdır.

## 1. Anahtarların (Keys) Önemi

Sızma testlerinde, **Foreign Key** ilişkilerini anlamak veritabanı haritasını çıkarmak için kritiktir. Bir tablodaki `user_id` sütunu başka bir tablodaki `id` ile eşleşiyorsa, bu tabloları `JOIN` ederek yetki yükseltme veya veri sızdırma senaryoları kurgulanabilir.

## 2. CRUD Güvenliği

- **INSERT:** Kayıt formları üzerinden veritabanına zararlı scriptler (XSS) yüklenmesine neden olabilir.
    
- **SELECT:** Yanlış yapılandırılmış bir SELECT sorgusu, parolasını bilmediğiniz bir kullanıcının bilgilerini sızdırmanıza (SQLi) olanak tanır.
    
- **UPDATE/DELETE:** Koşulsuz (WHERE'siz) çalıştırılan bu komutlar tüm veritabanını felç edebilir (DoS).
    

## 3. Fonksiyonların Sömürülmesi

Özellikle `GROUP_CONCAT()` veya `SUBSTRING()` gibi fonksiyonlar, sızdırılan verileri saldırganın terminaline uygun formatta getirmek için en sık kullanılan "silahlaştırılmış" araçlardır.

> **Son İpucu:** Siber güvenlikte "Veritabanı Keşfi" (Database Enumeration), sistemin beynini okumak gibidir. SQL temellerine ne kadar hakimseniz, bir zafiyeti bulup sömürmeniz (veya o zafiyeti kapatmanız) o kadar hızlı olur.