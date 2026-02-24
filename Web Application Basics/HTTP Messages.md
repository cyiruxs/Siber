# HTTP Mesajları (HTTP Messages)

**HTTP mesajları**, bir kullanıcı (**client**) ile web sunucusu (**web server**) arasında teati edilen (değiş Tokuş edilen) veri paketleridir. Bu mesajlar, web uygulamalarının nasıl çalıştığını anlamak için çok önemlidir; çünkü kullanıcıların isteklerinin (**requests**) ve sunucunun yanıtlarının (**responses**) nasıl iletildiğini gösterirler.

Bir **HTTP Request** (İstek) ve **HTTP Response** (Yanıt) örneği hayal edin; burada **method**, **URL**, **headers** ve **status codes** gibi anahtar bölümleri görebilirsiniz. Bunlar, **client-server** etkileşimini mümkün kılan unsurlardır.

İki tür **HTTP** mesajı vardır:

1. **HTTP Requests:** Eylemleri tetiklemek için kullanıcı tarafından web uygulamasına gönderilir.
    
2. **HTTP Responses:** Kullanıcının isteğine karşılık olarak sunucu tarafından gönderilir.
    

Her mesaj, hem kullanıcının hem de sunucunun sorunsuz iletişim kurmasına yardımcı olan belirli bir formatı izler:

### Başlangıç Satırı (Start Line)

Başlangıç satırı, mesajın girişi gibidir. Ne tür bir mesajın gönderildiğini söyler; kullanıcıdan gelen bir istek mi yoksa sunucudan gelen bir yanıt mı olduğunu belirtir. Bu satır ayrıca mesajın nasıl işlenmesi gerektiğine dair önemli ayrıntılar verir.

### Başlıklar (Headers)

**Headers**, **HTTP** mesajı hakkında ekstra bilgi sağlayan anahtar-değer (key-value) çiftlerinden oluşur. İsteği veya yanıtı işleyen **client** ve **server**'a talimatlar verirler. Bu başlıklar güvenlik, içerik türleri (**content types**) ve daha fazlası gibi her türlü konuyu kapsayarak iletişimdeki her şeyin sorunsuz gitmesini sağlar.

### Boş Satır (Empty Line)

Boş satır, **header** ile **body** kısmını birbirinden ayıran küçük bir bölücüdür. Gereklidir çünkü başlıkların nerede bittiğini ve mesajın asıl içeriğinin nerede başladığını gösterir. Bu boş satır olmazsa mesaj karışabilir ve **client** veya **server** bunu yanlış yorumlayarak hatalara neden olabilir.

### Gövde (Body)

**Body**, asıl verinin saklandığı yerdir. Bir istekte (**request**), gövde kullanıcının sunucuya göndermek istediği verileri (form verileri gibi) içerebilir. Bir yanıtta (**response**) ise sunucunun kullanıcının talep ettiği içeriği (bir web sayfası veya **API** verisi gibi) koyduğu yerdir.

---

## Neden HTTP Mesajlarını Anlamak Önemlidir?

Bu mesajlar, web uygulamalarının nasıl iletişim kurduğunun temelidir. Eğer düzgün yapılandırılmışlarsa, her şey sorunsuz çalışır.

Nasıl çalıştıklarını bilmek, web iletişimindeki sorunları teşhis etmenize yardımcı olur; bu da web uygulamanız için daha iyi performans ve güvenilirlik anlamına gelir. Ayrıca güvenlik için de çok önemlidir. **HTTP** mesajlarını anlamak, iletim sırasında verileri korumak için güçlü güvenlik önlemleri uygulamanıza yardımcı olur.

---

## 🛠 Teknik Detay ve Karşılaştırma

### HTTP Mesaj Yapısı Tablosu

|**Bölüm**|**HTTP Request (İstek) Örneği**|**HTTP Response (Yanıt) Örneği**|
|---|---|---|
|**Start Line**|`GET /index.html HTTP/1.1`|`HTTP/1.1 200 OK`|
|**Headers**|`Host: example.com`, `User-Agent: Mozilla...`|`Content-Type: text/html`, `Server: Apache`|
|**Empty Line**|`\r\n` (CRLF)|`\r\n` (CRLF)|
|**Body**|(Genellikle POST isteklerinde veri içerir)|`<html><body>Merhaba Dünya!</body></html>`|

### HTTP Akış Şeması (Mermaid)

Kod snippet'i

```
sequenceDiagram
    participant C as Client (Browser)
    participant S as Web Server
    Note over C: HTTP Request Oluşturulur
    C->>S: GET /login HTTP/1.1 (Headers + Body)
    Note over S: İstek İşlenir
    S->>C: HTTP/1.1 200 OK (Headers + Body)
    Note over C: Sayfa Render Edilir
```

---

## 🚩 CTF & Siber Güvenlik İpuçları

> [!IMPORTANT] **1. Burp Suite: HTTP Manipülasyonunun Şahı**
> 
> Bir siber güvenlik uzmanı için en önemli araç **Burp Suite**'tir. Burp, **client** ile **server** arasındaki bu HTTP mesajlarını yakalamanıza (intercept) ve **Start Line**, **Headers** veya **Body** kısmını sunucuya ulaşmadan önce değiştirmenize olanak tanır.

> [!CAUTION] **2. Güvenlik Başlıkları (Security Headers)**
> 
> `Content-Security-Policy (CSP)`, `X-Frame-Options` ve `Strict-Transport-Security (HSTS)` gibi başlıklar, uygulamanızı XSS ve Clickjacking gibi saldırılardan korumak için kritik mesaj bileşenleridir. Bir CTF'te bu başlıkların eksikliği genellikle bir zafiyetin işaretidir.

> [!TIP] **3. HTTP Verb Tampering (Yöntem Manipülasyonu)**
> 
> Bazen sunucular `GET` isteğini engeller ama `POST` veya `PUT` isteğine izin verir. **Start Line** üzerindeki metodu değiştirerek (örneğin `GET` yerine `DEBUG` veya `TRACE` yazarak) gizli dosyalara erişmeyi deneyebilirsiniz.

> [!NOTE] **4. Bilgi Sızıntısı (Information Leakage)**
> 
> Response mesajındaki `Server` veya `X-Powered-By` başlıkları, sunucunun sürümünü (örneğin `Server: Apache/2.4.41`) ele verebilir. Bu bilgi, saldırganın o sürüme özel bilinen bir **exploit** aramasına neden olur.