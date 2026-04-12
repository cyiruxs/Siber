 # JavaScript'in HTML ile Entegrasyonu

Bu bölüm, temel HTML yapısı hakkında bilgi sahibi olduğunuzu varsayar. JS genellikle içerik oluşturmak için değil; HTML ve CSS ile birlikte çalışarak **dinamik** ve **etkileşimli** web sayfaları üretmek için kullanılır. JS'yi HTML'e entegre etmenin iki ana yolu vardır: **Internal** (Dahili) ve **External** (Har ici).

---

## 1. Internal JavaScript (Dahili JavaScript)

Internal JS, kodun doğrudan bir HTML belgesi içine gömülmesidir. Bu yöntem, script'in HTML ile nasıl etkileşime girdiğini doğrudan görmenizi sağladığı için başlangıç aşamasında tercih edilir. Kodlar `<script>` etiketleri arasına yazılır.

- **`<head>` bölümünde:** Sayfa içeriği yüklenmeden önce çalışması gereken scriptler için kullanılır.
    
- **`<body>` bölümünde:** Sayfa öğeleri yüklenirken onlarla etkileşime giren scriptler için kullanılır.
    

### Örnek Uygulama

Masaüstünde `internal.html` adında bir dosya oluşturun ve şu kodu içine yapıştırın:

HTML

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Internal JS</title>
</head>
<body>
    <h1>İki Sayının Toplamı</h1>
    <p id="result"></p>

    <script>
        let x = 5;
        let y = 10;
        let result = x + y;
        // HTML öğesini seçme ve içeriğini değiştirme
        document.getElementById("result").innerHTML = "Sonuç: " + result;
    </script>
</body>
</html>
```

Bu belgede JS, `id="result"` olan `<p>` etiketini seçer ve `innerHTML` özelliğini kullanarak içeriğini günceller.

---

## 2. External JavaScript (Harici JavaScript)

External JS, kodun `.js` uzantılı ayrı bir dosyada saklanmasıdır. Bu yöntem, kodun daha düzenli ve bakımı kolay (maintainable) olmasını sağlar.

### Örnek Uygulama

1. **`script.js`** adında bir dosya oluşturun:
    
    JavaScript
    
    ```
    let x = 5;
    let y = 10;
    let result = x + y;
    document.getElementById("result").innerHTML = "Sonuç: " + result;
    ```
    
2. **`external.html`** adında bir dosya oluşturup JS dosyasını çağırın:
    
    HTML
    
    ```
    <!DOCTYPE html>
    <html lang="en">
    <body>
        <h1>İki Sayının Toplamı</h1>
        <p id="result"></p>
        <script src="script.js"></script>
    </body>
    </html>
    ```
    

**Avantajı:** JS kodunu HTML'den ayırarak karmaşıklığı azaltır ve aynı script'in birden fazla sayfada kullanılmasına (reusability) olanak tanır.

---

## 🔍 Internal ve External JS Tespiti (Pen-Testing)

Bir web uygulamasına sızma testi (**pen-testing**) yaparken, JS'nin nasıl yüklendiğini kontrol etmek kritiktir. Sayfaya sağ tıklayıp **"Sayfa Kaynağını Görüntüle" (View Page Source)** diyerek bunu doğrulayabilirsiniz.

|**Script Türü**|**Kaynak Koddaki Görünümü**|
|---|---|
|**Internal**|`<script>` etiketleri arasında doğrudan kod görünür.|
|**External**|`<script src="dosya.js">` şeklinde bir yol (path) görünür.|

---

## 🛡️ Siber Güvenlik ve CTF İpuçları

> [!IMPORTANT]
> 
> **Saldırı Yüzeyi Analizi:** Bir siber güvenlik uzmanı olarak, harici JS dosyaları her zaman ilginizi çekmelidir.

### 1. Hardcoded Credentials (Gömülü Bilgiler)

Geliştiriciler bazen harici `.js` dosyalarının içine test amaçlı kullanıcı adları, API anahtarları veya gizli URL'ler bırakabilirler.

- **CTF İpucu:** Sayfa kaynağındaki tüm `.js` linklerine tıklayın ve içlerinde `admin`, `password`, `key` veya `token` gibi kelimeleri aratın.
    

### 2. Third-Party Risks (Üçüncü Taraf Riskleri)

Eğer bir web sitesi JS dosyasını başka bir sunucudan (örneğin bir CDN'den) çekiyorsa ve o sunucu ele geçirilirse, tüm site ziyaretçilerine zararlı kod (Malware/Keylogger) bulaştırılabilir.

### 3. XSS ve Script Injection

Eğer bir uygulama, kullanıcıdan aldığı veriyi doğrudan bir `<script>` bloğu içine (Internal JS) yerleştiriyorsa, bu durum **Reflected XSS** zafiyetine yol açar.

---

### Karşılaştırma Tablosu

| **Özellik**          | **Internal JS**                    | **External JS**                                                      |
| -------------------- | ---------------------------------- | -------------------------------------------------------------------- |
| **Hız**              | Küçük scriptler için hızlıdır.     | Tarayıcı önbelleği (cache) sayesinde büyük projelerde daha hızlıdır. |
| **Bakım**            | Zor (Kod HTML içinde dağılmıştır). | Kolay (Modüler yapı).                                                |
| **Güvenlik Analizi** | Kaynak kodda hemen görülür.        | Analiz için dosyanın ayrıca indirilmesi gerekir.                     |
