Web uygulamalarıyla etkileşime girdiğinizde, sunucu isteğinizin başarılı olup olmadığını veya bir sorun oluşup oluşmadığını bildirmek için bir **HTTP yanıtı (Response)** gönderir. Bu yanıtlar, bir **durum kodu (Status Code)** ve sunucunun isteğinizi nasıl işlediğine dair kısa bir açıklama olan **gerekçe ifadesi (Reason Phrase)** içerir.
	
---

## 1. Durum Satırı (Status Line)

Her HTTP yanıtının ilk satırına **Durum Satırı** denir. Bu satır size üç temel bilgi verir:

- **HTTP Versiyonu:** Kullanılan HTTP protokol sürümünü (örn. HTTP/1.1) belirtir.
    
- **Durum Kodu (Status Code):** İsteğinizin sonucunu gösteren üç haneli bir sayıdır.
    
- **Gerekçe İfadesi (Reason Phrase):** Durum kodunu insanların anlayabileceği terimlerle açıklayan kısa bir mesajdır.
    

---

## 2. Durum Kodları ve Gerekçe İfadeleri

**Durum kodu**, isteğin başarılı olup olmadığını veya neden başarısız olduğunu belirten sayısal bir koddur. **Gerekçe ifadesi** ise bu kodu açıklar. Bu kodlar beş ana kategoriye ayrılır:

### Durum Kodu Kategorileri

|**Kategori**|**Tür**|**Açıklama**|
|---|---|---|
|**100-199**|**Informational** (Bilgisel)|Sunucu isteğin bir kısmını almış ve geri kalanını bekliyor. "Devam et" sinyalidir.|
|**200-299**|**Successful** (Başarılı)|Her şey beklendiği gibi çalıştı. Sunucu isteği işledi ve veriyi gönderdi.|
|**300-399**|**Redirection** (Yönlendirme)|İstenen kaynak başka bir yere taşındı. Genellikle yeni bir URL sağlanır.|
|**400-499**|**Client Error** (İstemci Hatası)|İstekte bir sorun var (yanlış URL, eksik kimlik doğrulaması vb.).|
|**500-599**|**Server Error** (Sunucu Hatası)|Sunucu isteği yerine getirirken bir hata ile karşılaştı. Sorun sunucu taraflıdır.|

---

### Sık Karşılaşılan Durum Kodları

- **100 (Continue):** Sunucu isteğin ilk kısmını aldı ve geri kalanı için hazır.
    
- **200 (OK):** İstek başarılı oldu ve sunucu istenen kaynağı gönderiyor.
    
- **301 (Moved Permanently):** Kaynak kalıcı olarak yeni bir URL'ye taşındı. Bundan sonra yeni URL kullanılmalıdır.
    
- **404 (Not Found):** Sunucu belirtilen URL'de kaynağı bulamadı. Adresi tekrar kontrol edin.
    
- **500 (Internal Server Error):** Sunucu tarafında bir şeyler ters gitti ve istek işlenemedi.
    

---

## 🚩 CTF & Siber Güvenlik İpuçları

HTTP yanıtlarını analiz etmek, bir web uygulamasının mimarisini ve zayıf noktalarını anlamak için hayati önem taşır.

> [!tip] Bilgi İfşası (Information Disclosure)
> 
> Bir **500 Internal Server Error** yanıtı aldığınızda, dönen gövdeyi (body) dikkatlice inceleyin. Bazen sunucular, saldırganın sistem hakkında (dosya yolları, veritabanı versiyonları vb.) bilgi edinmesine yol açan **stack trace** (hata yığın izi) verilerini sızdırabilir.

> [!info] 403 Forbidden vs 404 Not Found
> 
> Güvenlik odaklı yapılandırılmış sistemlerde, bir dosyanın varlığını gizlemek için (directory bruteforcing'i engellemek amacıyla) aslında var olan ancak yetkiniz olmayan bir dosya için `403` yerine `404` döndürülebilir. Buna "security through obscurity" (belirsizlik yoluyla güvenlik) denir.

> [!bug] Redirection Exploits (Open Redirect)
> 
> **301** veya **302** yönlendirmeleri sırasında sunucu `Location` başlığı kullanır. Eğer uygulama, yönlendirilecek adresi kullanıcıdan aldığı bir parametre ile (örn: `?next=google.com`) belirliyorsa ve bunu doğrulamıyorsa, kullanıcıları zararlı sitelere yönlendiren **Open Redirect** zafiyeti oluşabilir.

> [!abstract] CTF İpucu: Durum Kodlarını İzleme
> 
> `gobuster` veya `ffuf` gibi araçlarla dizin taraması yaparken, sadece `200` koduna odaklanmayın. `301`, `302` ve hatta `403` yanıtları, ilginç dizinlerin veya admin panellerinin habercisi olabilir.