Bir HTTP isteği, bir kullanıcının bir web uygulamasıyla etkileşime girmek ve bir eylemi tetiklemek için bir web sunucusuna gönderdiği mesajdır. Bu istekler genellikle kullanıcı ile web sunucusu arasındaki ilk temas noktası olduğundan, nasıl çalıştıklarını bilmek —özellikle siber güvenlikle ilgileniyorsanız— son derece önemlidir.

Bir HTTP isteğinin metot (örn. GET veya POST), yol (örn. /login) ve versiyon (örn. HTTP/1.1) gibi ana bölümlerini anlamak, bir istemcinin (kullanıcı) bir sunucu ile nasıl iletişim kurduğunun temelini oluşturur.

---

## 1. İstek Satırı (Request Line)

**İstek satırı** (veya start line), bir HTTP isteğinin ilk bölümüdür ve sunucuya ne tür bir istekle karşı karşıya olduğunu bildirir. Üç ana bölümden oluşur: **HTTP metodu**, **URL yolu** ve **HTTP versiyonu**.

> [!abstract] Formül
> 
> `METHOD /path HTTP/version`

---

## 2. HTTP Metotları (HTTP Methods)

**HTTP metodu**, kullanıcının URL yolu ile tanımlanan kaynak üzerinde hangi eylemi gerçekleştirmek istediğini sunucuya söyler. Aşağıda en yaygın metotlar ve beraberinde getirdikleri güvenlik riskleri yer almaktadır:

|**Metot**|**Açıklama**|**Güvenlik Uyarısı (Security Reminder)**|
|---|---|---|
|**GET**|Sunucudan veri çekmek (fetch) için kullanılır.|Hassas verileri (token, şifre) asla GET ile göndermeyin; URL'de düz metin olarak görünürler ve loglara düşerler.|
|**POST**|Sunucuya veri gönderir (oluşturma veya güncelleme).|**SQL Injection** veya **XSS**'i önlemek için girdileri her zaman valide edin ve temizleyin (sanitize).|
|**PUT**|Sunucudaki bir kaynağı değiştirir veya günceller.|Değişikliği kabul etmeden önce kullanıcının yetkili olduğunu (Authorization) mutlaka kontrol edin.|
|**DELETE**|Sunucudan bir kaynağı siler.|Sadece yetkili kullanıcıların silme işlemi yapabildiğinden emin olun; **IDOR** riskine dikkat edin.|

### Diğer Spesifik Metotlar

- **PATCH:** Bir kaynağın sadece bir kısmını günceller. Küçük değişiklikler için kullanışlıdır ancak veri tutarsızlığını önlemek için girdi doğrulaması şarttır.
    
- **HEAD:** GET gibi çalışır ancak sadece başlıkları (headers) getirir, içeriği getirmez. Yanıtın boyutunu veya meta verilerini kontrol etmek için idealdir.
    
- **OPTIONS:** Belirli bir kaynak için hangi metotların mevcut olduğunu söyler. İstemcinin sunucuyla ne yapabileceğini anlamasına yardımcı olur.
    
- **TRACE:** İsteğin sunucuya ulaşana kadar geçtiği yolu izlemek için kullanılır (genellikle hata ayıklama/debugging için). Çoğu sunucu güvenlik nedeniyle bunu devre dışı bırakır (**Cross-Site Tracing** riskine karşı).
    
- **CONNECT:** HTTPS gibi güvenli bir bağlantı (tünel) oluşturmak için kullanılır.
    

---

## 3. URL Yolu (URL Path)

**URL yolu**, sunucuya kullanıcının istediği kaynağın nerede olduğunu söyler. Örneğin; `https://tryhackme.com/api/users/123` adresinde `/api/users/123` yolu belirli bir kullanıcıyı tanımlar.

Saldırganlar, zafiyetleri istismar etmek için genellikle URL yolunu manipüle ederler. Bu nedenle şunlar hayati önem taşır:

- Yetkisiz erişimi önlemek için URL yolunu **doğrulayın**.
    
- Enjeksiyon saldırılarını önlemek için yolu **temizleyin (sanitize)**.
    
- Gizlilik ve risk değerlendirmeleri yaparak hassas verileri koruyun.
    

---

## 4. HTTP Versiyonları

**HTTP versiyonu**, istemci ve sunucu arasında iletişim kurmak için kullanılan protokol sürümünü gösterir:

- **HTTP/0.9 (1991):** İlk versiyon, sadece GET isteklerini destekliyordu.
    
- **HTTP/1.0 (1996):** Başlıklar (headers) ve farklı içerik türleri için destek eklendi, önbellekleme (caching) iyileştirildi.
    
- **HTTP/1.1 (1997):** Kalıcı bağlantılar (persistent connections), **chunked transfer encoding** ve gelişmiş önbellekleme getirdi. Günümüzde hala yaygın olarak kullanılmaktadır.
    
- **HTTP/2 (2015):** Daha hızlı performans için **multiplexing**, başlık sıkıştırma ve önceliklendirme özelliklerini sundu.
    
- **HTTP/3 (2022):** HTTP/2 üzerine inşa edilmiştir ancak daha hızlı ve güvenli bağlantılar için yeni bir protokol olan **QUIC** kullanır.
    

---

## 🚩 CTF & Siber Güvenlik İpuçları

> [!tip] Metot Manipülasyonu (Verb Tampering)
> 
> Bir web uygulamasında bir sayfaya erişiminiz kısıtlanmışsa, isteği `GET` yerine `POST` veya `OPTIONS` olarak değiştirmeyi deneyin. Bazen zayıf yapılandırılmış erişim kontrol listeleri (ACL), sadece belirli metotları kısıtlar ve diğerlerine izin verir.

> [!danger] Bilgi İfşası (Information Disclosure)
> 
> `OPTIONS` metodunu kullanarak sunucunun desteklediği metotları kontrol edin. Eğer `PUT` veya `DELETE` gibi metotlar aktifse ve kimlik doğrulaması zayıfsa, sunucuya dosya yükleyebilir veya mevcut dosyaları silebilirsiniz.

> [!bug] Path Traversal (Dizin Gezginliği)
> 
> URL yolunda `../` gibi ifadeler kullanarak sunucunun kök dizinine erişmeye çalışmak siber güvenlik testlerinde temel bir adımdır. Örneğin: `/api/users/../../etc/passwd`. 