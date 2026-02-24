    
    ## HTTP Güvenlik Başlıkları (Security Headers)

**HTTP Güvenlik Başlıkları**, Cross-Site Scripting (XSS), clickjacking ve diğer saldırılara karşı koruma sağlayarak web uygulamasının genel güvenliğini artırmaya yardımcı olur. Bu bölümde aşağıdaki güvenlik başlıklarını derinlemesine inceleyeceğiz:

- **Content-Security-Policy (CSP)**
    
- **Strict-Transport-Security (HSTS)**
    
- **X-Content-Type-Options**
    
- **Referrer-Policy**
    

Herhangi bir web sitesinin güvenlik başlıklarını analiz etmek için [securityheaders.com](https://securityheaders.com/) gibi siteleri kullanabilirsiniz. Bu görevdeki tartışmadan sonra, bu sitelerin raporladığı sonuçları çok daha iyi anlayacaksınız.

---

### Content-Security-Policy (CSP)

Bir **CSP** başlığı, Cross-Site Scripting (XSS) gibi yaygın saldırıları hafifletmeye yardımcı olabilecek ek bir güvenlik katmanıdır. Zararlı kodlar ayrı bir web sitesinde veya alan adında barındırılabilir ve savunmasız web sitesine enjekte edilebilir. CSP, yöneticilerin hangi alan adlarının veya kaynakların güvenli kabul edildiğini bildirmesine olanak tanır ve bu tür saldırılara karşı bir hafifletme katmanı sağlar.

Başlığın kendi içinde `default-src` veya `script-src` gibi tanımlanmış özellikler ve daha fazlasını görebilirsiniz. Bunların her biri, bir yöneticiye hangi içerik türü için hangi alan adlarına izin verildiğini çeşitli ayrıntı düzeylerinde tanımlama seçeneği sunar. `'self'` anahtar kelimesi, web sitesinin barındırıldığı alan adının kendisini temsil eden özel bir ifadedir.

**Örnek bir CSP başlığına bakalım:**

`Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'`

Buradaki direktiflerin açıklaması:

- **default-src:** Varsayılan politikanın `'self'` (yani sadece mevcut web sitesi) olduğunu belirtir.
    
- **script-src:** Komut dosyalarının (scripts) neredeyse yüklenebileceğine dair politikayı belirler; burada `'self'` ile birlikte `https://cdn.tryhackme.com` adresinde barındırılan script'lere izin verilmiştir.
    
- **style-src:** CSS stil dosyalarının yalnızca mevcut web sitesinden (`'self'`) yüklenebileceğini belirtir.
    

---

### Strict-Transport-Security (HSTS)

**HSTS** başlığı, web tarayıcılarının her zaman HTTPS üzerinden bağlanmasını sağlar. Bir HSTS örneğine bakalım:

`Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`

HSTS başlığının direktiflerine göre dökümü şöyledir:

- **max-age:** Bu ayarın saniye cinsinden geçerlilik süresidir (Örnekte 2 yıl).
    
- **includeSubDomains:** Tarayıcıya bu ayarı tüm alt alan adlarına (subdomains) da uygulamasını talimatını veren isteğe bağlı bir ayardır.
    
- **preload:** Web sitesinin "preload" (ön yükleme) listelerine dahil edilmesine izin veren isteğe bağlı bir ayardır. Tarayıcılar, bir web sitesine ilk ziyaret gerçekleşmeden bile HSTS'yi zorunlu kılmak için bu listeleri kullanabilir.
    

---

### X-Content-Type-Options

**X-Content-Type-Options** başlığı, tarayıcılara bir kaynağın MIME türünü tahmin etmemelerini (guess), yalnızca `Content-Type` başlığında belirtilen türü kullanmalarını söylemek için kullanılır.

`X-Content-Type-Options: nosniff`

- **nosniff:** Bu direktif, tarayıcıya MIME türünü koklamamasını (sniff) veya tahmin etmemesini söyler.
    

---

### Referrer-Policy

Bu başlık, bir kullanıcı bir bağlantıya tıkladığında kaynak web sunucusundan hedef web sunucusuna ne kadar bilgi gönderileceğini kontrol eder. Web yöneticisinin hangi bilgilerin paylaşıldığını kontrol etmesine olanak tanır. İşte bazı **Referrer-Policy** örnekleri:

- `Referrer-Policy: no-referrer`
    
- `Referrer-Policy: same-origin`
    
- `Referrer-Policy: strict-origin`
    
- `Referrer-Policy: strict-origin-when-cross-origin`
    

Direktiflerin açıklamaları:

- **no-referrer:** Yönlendiren (referrer) hakkında gönderilen tüm bilgileri tamamen devre dışı bırakır.
    
- **same-origin:** Yalnızca hedef, aynı kökenin (origin) bir parçası olduğunda yönlendiren bilgisini gönderir. Dahili bağlantılarda bilgi aktarımı isteyip harici sitelere bilgi gitmesini istemediğinizde yararlıdır.
    
- **strict-origin:** Yalnızca protokol aynı kaldığında (HTTPS -> HTTPS) yönlendireni gönderir.
    
- **strict-origin-when-cross-origin:** `strict-origin` ile benzerdir, ancak aynı kökenli istekler için tam URL yolunu gönderir.
    

---

### 💡 Güvenlik Başlıkları Özet Tablosu

| **Başlık**                 | **Temel Amaç**                     | **Kritik Direktif**          |
| -------------------------- | ---------------------------------- | ---------------------------- |
| **CSP**                    | XSS ve Veri Enjeksiyonunu Önleme   | `script-src`, `object-src`   |
| **HSTS**                   | HTTPS'i Zorunlu Kılma              | `max-age`, `preload`         |
| **X-Content-Type-Options** | MIME Sniffing Saldırılarını Önleme | `nosniff`                    |
| **Referrer-Policy**        | Hassas Bilgi Sızıntısını Önleme    | `no-referrer`, `same-origin` |

---

### 🚩 CTF & Siber Güvenlik İpuçları

1. **CSP Bypass (Atlatma):** CTF'lerde katı bir CSP varsa ancak `script-src` içerisinde güvenilir bir CDN (örneğin Google veya Cloudflare) tanımlanmışsa, bu CDN'ler üzerinde barındırılan ve XSS yapmanıza olanak tanıyan kütüphaneleri (örneğin eski bir AngularJS versiyonu) kullanarak CSP'yi bypass edebilirsiniz. [CSP Evaluator](https://csp-evaluator.withgoogle.com/) aracını kullanarak CSP açıklarını analiz edin.
    
2. **MIME Sniffing:** Eğer bir web sitesi kullanıcıların dosya yüklemesine izin veriyorsa ve `X-Content-Type-Options: nosniff` başlığı eksikse, bir `.jpg` dosyası gibi görünen ancak aslında içinde JavaScript kodu barındıran bir dosyayı tarayıcıya "script" olarak işletebilirsiniz.
    
3. **Clickjacking Kontrolü:** İncelediğimiz listede yok ancak `X-Frame-Options` (DENY veya SAMEORIGIN) başlığının eksikliği, sitenizin bir `<iframe>` içine gömülerek clickjacking saldırısına maruz kalmasına neden olabilir.
    
  4. **HSTS ve Kurulum:** Bir sızma testinde HSTS başlığının eksikliği "Low" veya "Informational" bir bulgu olarak raporlanır. Ancak bu, "Man-in-the-Middle" (MitM) saldırılarını kolaylaştıran bir eksikliktir.