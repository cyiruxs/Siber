 HTTP isteklerinin detaylarına indiğimizde, sadece ne istediğimizi değil, bu isteğin nasıl taşındığını ve sunucunun bunu nasıl anlamlandırdığını belirleyen katmanlarla karşılaşırız. Özellikle **Request Headers** (İstek Başlıkları) ve **Request Body** (İstek Gövdesi), bir web uygulamasının güvenlik mekanizmalarını test ederken en çok manipüle ettiğimiz alanlardır.

---

## 1. Request Headers (İstek Başlıkları)

**Request Headers**, web sunucusuna istek hakkında ek bilgiler iletilmesini sağlar. Bu başlıklar, istemcinin kimliği, beklenen içerik türü ve oturum yönetimi gibi kritik verileri taşır.

### Yaygın Kullanılan Request Başlıkları

|**Request Header**|**Örnek**|**Açıklama**|
|---|---|---|
|**Host**|`Host: tryhackme.com`|İsteğin hangi web sunucusu için olduğunu belirtir.|
|**User-Agent**|`User-Agent: Mozilla/5.0`|İsteğin geldiği web tarayıcısı ve işletim sistemi hakkında bilgi paylaşır.|
|**Referer**|`Referer: https://google.com/`|İsteğin hangi URL üzerinden yönlendirildiğini gösterir.|
|**Cookie**|`Cookie: session=xyz123; user_type=student`|Sunucunun daha önce tarayıcıya kaydetmesini istediği verileri taşır (Oturum yönetimi için kritiktir).|
|**Content-Type**|`Content-Type: application/json`|İstek gövdesindeki verinin formatını (türünü) tanımlar.|

---

## 2. Request Body (İstek Gövdesi)

`POST` ve `PUT` gibi HTTP metotlarında, veri sadece istenmez; sunucuya gönderilir. Bu gönderilen veri **HTTP Request Body** (İstek Gövdesi) içinde yer alır. Verinin formatı uygulamaya göre değişebilir. En yaygın formatlar şunlardır:

### A. URL Encoded (`application/x-www-form-urlencoded`)

Verilerin anahtar-değer (key=value) çiftleri şeklinde yapılandırıldığı bir formattır. Çiftler `&` sembolü ile ayrılır ve özel karakterler **percent-encoding** (yüzde kodlama) ile temsil edilir.

> [!example] Örnek İstek
> 
> HTTP
> 
> ```
> POST /profile HTTP/1.1
> Host: tryhackme.com
> User-Agent: Mozilla/5.0
> Content-Type: application/x-www-form-urlencoded
> Content-Length: 33
> ```

> name=Aleksandra&age=27&country=US

---

### B. Form Data (`multipart/form-data`)

Birden fazla veri bloğunun gönderilmesine olanak tanır. Her blok bir **boundary** (sınır) dizesi ile ayrılır. Bu format, özellikle dosya veya resim yükleme gibi ikili (binary) verilerin gönderilmesi için kullanılır.

> [!example] Örnek İstek
> 
> HTTP
> 
> ```
> POST /upload HTTP/1.1
> Host: tryhackme.com
> Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW
> ```

> ----WebKitFormBoundary7MA4YWxkTrZu0gW
> 
> Content-Disposition: form-data; name="username"

> aleksandra
> 
> ----WebKitFormBoundary7MA4YWxkTrZu0gW
> 
> Content-Disposition: form-data; name="profile_pic"; filename="aleksandra.jpg"
> 
> Content-Type: image/jpeg

> [İmajı temsil eden Binary Veri Burada]
> 
> ----WebKitFormBoundary7MA4YWxkTrZu0gW--

---

### C. JSON (`application/json`)

Veriler **JavaScript Object Notation (JSON)** yapısında gönderilir. Veriler `isim : değer` çiftleri halinde, süslü parantez `{ }` içinde ve virgülle ayrılarak sunulur. Modern API'lerin vazgeçilmezidir.

> [!example] Örnek İstek
> 
> HTTP
> 
> ```
> POST /api/user HTTP/1.1
> Host: tryhackme.com
> Content-Type: application/json
> ```

> {
> 
> "name": "Aleksandra",
> 
> "age": 27,
> 
> "country": "US"
> 
> }

---

### D. XML (`application/xml`)

Veriler, açılış ve kapanış **tag**'leri (etiketleri) içine yerleştirilir. Etiketler iç içe geçebilir.

> [!example] Örnek İstek
> 
> HTTP
> 
> ```
> POST /api/user HTTP/1.1
> Host: tryhackme.com
> Content-Type: application/xml
> ```

---

## 🚩 CTF & Siber Güvenlik İpuçları

### 1. User-Agent ve Referer Sahteciliği

Bazı uygulamalar sadece belirli tarayıcılardan veya belirli bir sayfadan (Referer) gelindiğinde erişime izin verir. CTF'lerde bu başlıkları manuel olarak değiştirerek (Örn: `Referer: admin.tryhackme.com`) yetki atlatma denemeleri yapmalısınız.

### 2. Content-Type Manipülasyonu

Bir sunucu sadece JSON kabul ettiğini söylüyorsa, bazen bu başlığı `application/xml` olarak değiştirip sunucunun **XXE (XML External Entity)** saldırılarına karşı savunmasız olup olmadığını test edebilirsiniz. Sunucu beklemediği bir formatı işlerken hata verebilir ve bilgi sızdırabilir.

### 3. Insecure Deserialization (Güvensiz Serileştirme)

Özellikle JSON ve XML formatındaki gövdelerde, sunucu tarafındaki kod bu verileri objeye dönüştürürken zafiyet barındırabilir. Gövde içindeki veri yapılarını manipüle ederek **Uzaktan Kod Çalıştırma (RCE)** elde edilebilir.

### 4. File Upload (Dosya Yükleme) Bypass

`multipart/form-data` kullanırken `Content-Type: image/jpeg` başlığını manuel olarak ekleyerek, aslında `.php` olan bir dosyayı resimmiş gibi sunucuya yutturmaya çalışabilirsiniz. Sunucu sadece başlığa bakıyorsa zafiyet oluşur.