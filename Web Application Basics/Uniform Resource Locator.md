# Uniform Resource Locator (URL)

Bir **Uniform Resource Locator (URL)**, ister bir web sayfası, ister bir video, bir fotoğraf veya başka bir medya olsun, her türlü çevrimiçi içeriğe erişmenizi sağlayan bir web adresidir. Tarayıcınızı İnternet üzerindeki doğru yere yönlendirir.

## Anatomy of a URL

Bir **URL**'yi, her biri doğru kaynağı bulmanıza yardımcı olmak için farklı bir rol oynayan birkaç parçadan oluşmuş olarak düşünün. Bu parçaların birbirine nasıl uyduğunu anlamak; web'de gezinmek, web uygulamaları geliştirmek ve hatta sorunları gidermek (troubleshooting) için önemlidir.

İşte temel bileşenlerin dökümü:

### Scheme

**Scheme**, web sitesine erişmek için kullanılan protokoldür. En yaygın olanları **HTTP** (HyperText Transfer Protocol) ve **HTTPS** (Hypertext Transfer Protocol Secure) protokolleridir. **HTTPS**, bağlantıyı şifrelediği için daha güvenlidir; bu yüzden tarayıcılar ve siber güvenlik uzmanları bunu önerir. Web siteleri genellikle ek koruma için **HTTPS** kullanımını zorunlu kılar.

### User

Bazı **URL**'ler, kimlik doğrulaması gerektiren siteler için bir kullanıcının oturum açma ayrıntılarını (genellikle bir kullanıcı adı) içerebilir. Bu, çoğunlukla belirli kaynaklara erişmek için kimlik bilgilerine ihtiyaç duyan **URL**'lerde gerçekleşir. Ancak, oturum açma ayrıntılarını **URL**'ye koymak pek güvenli olmadığından (hassas bilgileri ifşa edebilir ve bu bir güvenlik riskidir) günümüzde bu durum nadirdir.

### Host/Domain

**Host** veya **Domain**, **URL**'nin en önemli parçasıdır çünkü hangi web sitesine eriştiğinizi söyler. Her alan adının (domain name) benzersiz olması gerekir ve alan adı kayıt kuruluşları (domain registrars) aracılığıyla kaydedilir. Güvenlik açısından, gerçek olanlara çok benzeyen ancak küçük farkları olan alan adlarına dikkat edin (buna **typosquatting** denir). Bu sahte alan adları, genellikle insanları hassas bilgilerini vermeleri için kandırmak amacıyla **phishing** saldırılarında kullanılır.

### Port

**Port number**, tarayıcınızı web sunucusundaki doğru servise yönlendirmeye yardımcı olur. Sunucuya iletişim için hangi kapıyı kullanacağını söylemek gibidir. **Port** numaraları 1 ile 65.535 arasında değişir, ancak en yaygın olanları **HTTP** için **80** ve **HTTPS** için **443**'tür.

### Path

**Path**, sunucu üzerinde erişmeye çalıştığınız belirli dosya veya sayfayı işaret eder. Tarayıcıya nereye gideceğini gösteren bir yol haritası gibidir. Web sitelerinin, yalnızca yetkili kullanıcıların hassas kaynaklara erişebildiğinden emin olmak için bu yolları güvenli hale getirmesi gerekir.

### Query String

**Query string**, **URL**'nin soru işareti (`?`) ile başlayan kısmıdır. Genellikle arama terimleri veya form girdileri gibi şeyler için kullanılır. Kullanıcılar bu **query string**'leri değiştirebildiği için, kötü amaçlı kodların eklenebileceği **injections** gibi saldırıları önlemek adına bunların güvenli bir şekilde işlenmesi önemlidir.

### Fragment

**Fragment**, bir kare sembolü (`#`) ile başlar ve bir web sayfasının belirli bir bölümüne işaret etmeye yardımcı olur (belirli bir başlığa veya tabloya doğrudan atlamak gibi). Kullanıcılar bunu da değiştirebilir, bu nedenle **query string**'lerde olduğu gibi, **injection** saldırıları gibi sorunlardan kaçınmak için buradaki verileri kontrol etmek ve temizlemek önemlidir.

---

## 🛠 URL Bileşenleri ve Güvenlik Özeti

|**Bileşen**|**Örnek**|**Açıklama**|**Güvenlik Riski**|
|---|---|---|---|
|**Scheme**|`https://`|Kullanılan iletişim protokolü.|`http` kullanımı (şifresiz veri).|
|**User**|`admin:`|Kimlik bilgileri (opsiyonel).|Bilgilerin loglarda açıkça görünmesi.|
|**Host**|`google.com`|Sunucunun adresi/kimliği.|**Typosquatting** (örn: `g00gle.com`).|
|**Port**|`:443`|Servis kapı numarası.|Standart dışı portlarda açık servisler.|
|**Path**|`/search`|Dosya veya dizin yolu.|**Path Traversal** (örn: `../../etc/passwd`).|
|**Query**|`?q=test`|Parametreler ve veriler.|**SQLi**, **XSS**, **Open Redirect**.|
|**Fragment**|`#top`|Sayfa içi çapa (anchor).|**DOM-based XSS**.|

---

## 🚩 CTF & Siber Güvenlik İpuçları

> [!IMPORTANT] **1. URL Encoding (Yüzde Kodlama)**
> 
> Tarayıcılar, URL içindeki özel karakterleri (boşluk, ?, #, & vb.) iletmek için **URL Encoding** kullanır. Örneğin boşluk karakteri `%20` olarak kodlanır. CTF'lerde, filtreleri atlatmak (bypass) için saldırı payload'larınızı (örneğin bir `<script>` etiketi) URL encode etmeniz gerekebilir.

> [!CAUTION] **2. SSRF (Server-Side Request Forgery)**
> 
> Bir web uygulaması, kullanıcıdan aldığı bir URL'yi sunucu tarafında işleyip o adrese istek atıyorsa bu büyük bir risktir. Saldırgan, URL'yi `http://localhost:80` veya `http://169.254.169.254` (cloud metadata) şeklinde değiştirerek sunucunun iç ağına sızabilir.

> [!TIP] **3. Open Redirect (Açık Yönlendirme)**
> 
> `?next=dashboard` gibi parametreler içeren URL'lere dikkat edin. Eğer uygulama bu parametreyi kontrol etmeden yönlendirme yapıyorsa, bir saldırgan kurbanı `?next=https://malicious-site.com` adresine göndererek kimlik bilgilerini çalabilir.

> [!NOTE] **4. Burp Suite ile Manipülasyon**
> 
> Gerçek bir sızma testinde URL'deki **Query String** veya **Path** kısımlarını tarayıcıdan değiştirmek yerine **Burp Suite Proxy** kullanarak istekleri yakalayıp manipüle etmek çok daha profesyonel ve etkili bir yöntemdir.