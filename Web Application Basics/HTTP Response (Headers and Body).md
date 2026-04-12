## HTTP Yanıt Başlıkları (Response Headers)
 
Bir web sunucusu bir **HTTP** isteğine yanıt verdiğinde, yanıtın içine anahtar-değer çiftlerinden oluşan **HTTP yanıt başlıklarını** ekler. Bu başlıklar, yanıt hakkında kritik bilgiler sağlar ve istemciye (genellikle tarayıcıya) bu yanıtı nasıl işlemesi gerektiğini söyler.

Aşağıdaki tabloda, bir HTTP yanıtında yer alan temel başlıkları ve görevlerini görebilirsiniz:

| **Başlık (Header)** | **Örnek Kullanım**                       | **Açıklama**                                                                                  |
| ------------------- | ---------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Date**            | `Date: Mon, 09 Feb 2026 18:43:21 GMT`    | Yanıtın sunucu tarafından oluşturulduğu tam tarih ve saat.                                    |
| **Content-Type**    | `Content-Type: text/html; charset=utf-8` | İçeriğin türünü (HTML, JSON, vb.) ve karakter setini belirtir.                                |
| **Server**          | `Server: nginx`                          | İsteği işleyen sunucu yazılımı hakkında bilgi verir.                                          |
| **Set-Cookie**      | `Set-Cookie: sessionId=38af1337es7a8`    | Sunucudan istemciye çerez gönderir; tarayıcı bunu saklar ve sonraki isteklerde geri gönderir. |
| **Cache-Control**   | `Cache-Control: max-age=600`             | Yanıtın ne kadar süre önbelleğe alınacağını belirler.                                         |
| **Location**        | `Location: /index.html`                  | Yönlendirme (3xx) durumlarında istemcinin gitmesi gereken yeni adresi belirtir.               |

---

### Temel Yanıt Başlıkları

Bazı başlıklar, HTTP protokolünün düzgün çalışması ve hem istemcinin hem de sunucunun süreci doğru yönetebilmesi için hayati öneme sahiptir:

- **Date:** Sunucunun zaman damgasıdır. Önbellek geçerliliği ve senkronizasyon için kullanılır.
    
- **Content-Type:** Tarayıcının gelen veriyi nasıl yorumlayacağını belirler. Eğer bu başlık yanlış yapılandırılırsa, tarayıcı bir HTML sayfasını düz metin olarak gösterebilir veya bir dosyayı indirmeye çalışabilir.
    
- **Server:** Hata ayıklama (debugging) için yararlıdır. Ancak, saldırganlara sunucu hakkında bilgi sızdırmamak adına genellikle gizlenmesi veya değiştirilmesi (obfuscation) önerilir.
    

---

### Diğer Yaygın Yanıt Başlıkları

Bu başlıklar, istemciye ek talimatlar vererek yanıtın nasıl yönetileceğini kontrol eder:

- **Set-Cookie:** Oturum yönetimi için kullanılır. Güvenlik için **HttpOnly** (JavaScript erişimini engellemek için) ve **Secure** (yalnızca HTTPS üzerinden gönderilmesi için) bayrakları ile birlikte kullanılmalıdır.
    
- **Cache-Control:** Performansı artırmak için kullanılır. Hassas verilerin kaydedilmesini önlemek için `no-cache` veya `no-store` değerleri tercih edilebilir.
    
- **Location:** 301 veya 302 gibi yönlendirme kodlarıyla kullanılır. Kullanıcı tarafından manipüle edilebildiği durumlarda dikkatle sanitize edilmelidir.
    

---

### Yanıt Gövdesi (Response Body)

**HTTP yanıt gövdesi**, sunucunun istemciye gönderdiği asıl verilerin (HTML, JSON, görüntüler vb.) bulunduğu yerdir. Başlıklar verinin "nasıl" işleneceğini söylerken, gövde verinin "kendisini" içerir.

---

### 🛡️ Siber Güvenlik İpuçları ve CTF Notları

Siber güvenlik perspektifinden bakıldığında, yanıt başlıkları hem bir bilgi toplama (reconnaissance) kaynağı hem de bir saldırı yüzeyidir:

- **Information Leakage (Bilgi Sızıntısı):** `Server` veya `X-Powered-By` gibi başlıklar, kullanılan yazılımın versiyonunu sızdırabilir. Bir saldırgan bu versiyona yönelik bilinen açıkları (CVE) araştırabilir.
    
- **Open Redirect (Açık Yönlendirme):** Eğer bir uygulama `Location` başlığını kullanıcıdan aldığı girdiyle (örneğin: `?next=/dashboard`) oluşturuyorsa ve bu girdiyi doğrulamıyorsa, saldırgan kullanıcıları zararlı bir siteye (`?next=https://malicious.com`) yönlendirebilir.
    
- **XSS ve Sanitization:** Yanıt gövdesine kullanıcıdan gelen veriler (örneğin bir arama terimi) doğrudan ekleniyorsa, Cross-Site Scripting (XSS) saldırısı gerçekleşebilir. Veriler her zaman **escape** edilmelidir.
    
- **Güvenlik Başlıkları:** Yukarıdakilere ek olarak, `Content-Security-Policy` (CSP), `X-Frame-Options` ve `Strict-Transport-Security` (HSTS) gibi modern güvenlik başlıklarını kullanmak, uygulamanın güvenlik seviyesini önemli ölçüde artırır.
    

> **CTF İpucu:** Bir web sorusuyla karşılaştığında, tarayıcının "Network" sekmesinden veya `curl -I <URL>` komutuyla yanıt başlıklarını mutlaka incele. Bazen flag veya bir ipucu, standart dışı bir başlık içerisine gizlenmiş olabilir!