# JavaScript Temelleri ve Web Mekanizması

## Değişkenler (Variables)

Değişkenler, veri değerlerini saklamanıza olanak tanıyan kapsayıcılardır. Diğer dillerde olduğu gibi, JS'deki değişkenler de veriyi depolamak için kullanılan kutulara benzer. Bir kovaya bir şey koyduğunuzda, daha sonra kolayca referans verebilmek için onu etiketlemeniz gerekir. Benzer şekilde, JS'de her değişkenin bir ismi vardır; bir değişkene belirli bir değer atadığımızda, ona daha sonra erişmek için bir isim veririz.

JS'de değişken tanımlamanın üç yolu vardır: `var`, `let` ve `const`.

- **var:** Fonksiyon kapsamlıdır (function-scoped).
    
- **let** ve **const:** Blok kapsamlıdır (block-scoped). Bu, belirli kod blokları içinde değişken görünürlüğü üzerinde daha iyi kontrol sağlar.
    

> [!TIP]
> 
> **Siber Güvenlik İpucu: Variable Hoisting ve Scope**
> 
> `var` kullanımı, değişkenin tanımlanmadan önce kullanılabilmesine (hoisting) neden olabilir. Güvenli kod geliştirme (Secure Coding) pratikleri açısından, kapsam dışı veri sızıntılarını önlemek için modern projelerde her zaman `let` ve `const` tercih edilmelidir.

---

## Veri Tipleri (Data Types)

JS'de veri tipleri, bir değişkenin tutabileceği değerin türünü tanımlar. Örnekler:

- **string** (metin)
    
- **number** (sayı)
    
- **boolean** (true/false)
    
- **null**
    
- **undefined**
    
- **object** (array/dizi veya nesneler gibi daha karmaşık veriler için)
    

|**Veri Tipi**|**Açıklama**|**Örnek**|
|---|---|---|
|String|Karakter dizileri|`"admin"`|
|Number|Tam ve ondalıklı sayılar|`404`|
|Boolean|Mantıksal değerler|`true`|
|Object|Anahtar-değer çiftleri|`{id: 1, role: "user"}`|

---

## Fonksiyonlar (Functions)

Bir fonksiyon, belirli bir görevi yerine getirmek üzere tasarlanmış bir kod bloğunu temsil eder. Benzer bir görevi yapması gereken kodları bir fonksiyon içinde gruplandırırsınız. Örneğin, öğrencilerin sonuçlarını web sayfasında yazdıran bir uygulama geliştiriyorsunuz. En ideal durum, kullanıcının sıra numarasını (roll number) argüman olarak alan bir `PrintResult(rollNum)` fonksiyonu oluşturmaktır.

JavaScript

```
<script>
    function PrintResult(rollNum) {
        alert("Roll numarası " + rollNum + " olan kullanıcı sınavı geçti");
        // sonucu görüntülemek için diğer mantıksal işlemler
    }

    // sıra numaraları dizisini hazırla (veri)
    const rollNumbers = [101, 102, 103];

    // Not: Sadece 3 numaramız var, bu yüzden i = 2'den sonra rollNumbers[i] 'undefined' olur

    for (let i = 0; i < 100; i++) {
        PrintResult(rollNumbers[i]);
    }
</script>
```

Tüm öğrenciler için aynı kodu tekrar tekrar yazmak yerine, sonucu yazdırmak için basit bir fonksiyon kullanırız.

---

## Döngüler (Loops)

Döngüler, bir koşul **true** (doğru) olduğu sürece bir kod bloğunu birden çok kez çalıştırmanıza olanak tanır. JS'deki yaygın döngüler `for`, `while` ve `do...while`'dır. Bunlar, bir öğe listesini taramak gibi tekrarlayan görevler için kullanılır.

![for loop flow chart, yapay zekayla üretilmiş](https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcQt_UNk84Ja6TI7j1AzBUOl9QdxCp7hvWHTs_DFMMxBhjjqz_aLXnElccyfXoam5XDEt7ST6PpHdHe0mXVyFwBIFLsZZuKAJfg6XUyegO7EdZqzmbM)



> [!CAUTION]
> 
> **CTF / Siber Güvenlik Notu: Sonsuz Döngü ve DoS**
> 
> Döngü koşullarının yanlış yapılandırılması (örneğin bitiş koşulunun asla sağlanmaması), tarayıcının kilitlenmesine veya sunucu kaynaklarının tükenmesine neden olabilir. Bu durum basit bir **Client-side DoS** (Hizmet Dışı Bırakma) zafiyetine yol açabilir.

---

## İstek-Yanıt Döngüsü (Request-Response Cycle)

Web geliştirmede istek-yanıt döngüsü, bir kullanıcının tarayıcısının (istemci/client) bir web sunucusuna istek göndermesi ve sunucunun istenen bilgilerle yanıt vermesidir. Bu yanıt bir web sayfası, veri veya diğer kaynaklar olabilir.

### Güvenlik Perspektifi: İstek ve Yanıtlar

|**Bileşen**|**Güvenlik Kontrolü**|
|---|---|
|**Request (İstek)**|Girdi doğrulama (Input Validation) yapılmalıdır.|
|**Response (Yanıt)**|Hassas veri sızıntısı (Sensitive Data Exposure) kontrol edilmelidir.|
|**Headers (Başlıklar)**|`Content-Security-Policy` (CSP) gibi güvenlik başlıkları eklenmelidir.|

---

### 🚩 Siber Güvenlik / CTF İpucu: Insecure Direct Object Reference (IDOR)

Yukarıdaki kod örneğinde kullanılan `rollNum` gibi ardışık ve tahmin edilebilir sayılar, siber güvenlikte büyük bir risk oluşturabilir. Eğer bir saldırgan `PrintResult(101)` fonksiyonunu gördükten sonra manuel olarak `PrintResult(105)` parametresini denerse ve yetkisi olmadığı halde başka birinin sonucunu görebilirse, buna **IDOR (Güvensiz Doğrudan Nesne Referansı)** denir.

**Çözüm:** Kullanıcı verilerine erişirken sadece ID'ye güvenmeyin; her zaman oturum (session) kontrolü yapın!