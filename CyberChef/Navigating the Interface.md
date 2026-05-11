## CyberChef Arayüzü ve Alanları

CyberChef dört ana alandan oluşur ve her biri farklı bileşenler veya özellikler içerir:

1. **Operations** (İşlemler)
    
2. **Recipe** (Reçete)
    
3. **Input** (Giriş)
    
4. **Output** (Çıkış)
    

### 1. The Operations Area (İşlemler Alanı)

Burası, CyberChef'in gerçekleştirebildiği tüm farklı işlemlerin bulunduğu kapsamlı bir depodur. İşlemler, kullanıcıların yeteneklere kolayca erişebilmesi için titizlikle kategorize edilmiştir. Kullanıcılar, belirli işlemleri hızla bulmak için arama özelliğini kullanabilirler.

Siber güvenlik yolculuğunuz boyunca kullanabileceğiniz bazı işlemler şunlardır:

|İşlem (Operation)|Açıklama|Örnek|
|---|---|---|
|**From Morse Code**|Mors alfabesini (büyük harf) alfanümerik karakterlere çevirir.|`- .... .-. . .- - ...` → `THREATS`|
|**URL Encode**|Sorunlu karakterleri, URI/URL'ler tarafından desteklenen "yüzde kodlama" (**percent-encoding**) formatına dönüştürür.|`[https://tryhackme.com](https://tryhackme.com)` → `https%3A%2F%2Ftryhackme%2Ecom`|
|**To Base64**|Ham verileri bir ASCII **Base64** dizgisine kodlar.|`This is fun!` → `VGhpcyBpcyBmdW4h`|
|**To Hex**|Giriş dizgisini, belirtilen sınırlayıcı ile ayrılmış heksadesimal baytlara dönüştürür.|`Awesome!` → `41 77 65 73 6f 6d 65 21`|
|**To Decimal**|Giriş verilerini bir tamsayı dizisine dönüştürür.|`A` → `65`|
|**ROT13**|Alfabedeki karakterleri belirtilen miktar kadar (varsayılan 13) kaydıran basit bir Sezar ikame şifresidir.|`Forensics` → `Sberafvpf`|

---

### 2. The Recipe Area (Reçete Alanı)

Aracın kalbi olarak kabul edilir. Bu alanda, ihtiyaçlarınıza uygun işlemleri sorunsuz bir şekilde seçebilir, düzenleyebilir ve ince ayar yapabilirsiniz. İşlemlerin argümanlarını ve seçeneklerini hassas bir şekilde tanımladığınız yer burasıdır. Kullanmak istediğiniz işlemleri buraya sürükleyebilir ve davranışlarını özelleştirebilirsiniz.

**Özellikler şunları içerir:**

- **Save recipe:** Seçili işlemleri kaydetmenizi sağlar.
    
- **Load recipe:** Daha önce kaydedilmiş reçeteleri yüklemenizi sağlar.
    
- **Clear Recipe:** Kullanım sırasında seçilen reçeteyi temizlemenizi sağlar.
    
- **BAKE! Butonu:** Verileri verilen reçete ile işler.
    
- **Auto Bake:** Her seferinde manuel olarak **BAKE!** butonuna tıklamadan, seçilen reçeteyi kullanarak otomatik olarak "pişirme" işlemini gerçekleştirir.
    

---

### 3. Input Area (Giriş Alanı)

Giriş alanı; metinleri veya dosyaları yapıştırarak, yazarak veya sürükleyerek işlemler gerçekleştirebileceğiniz kullanıcı dostu bir alandır.

**Ek özellikler:**

- **Add a new input tab:** Farklı değerler kullanmak için ek bir sekme oluşturur.
    
- **Open folder as input:** Tüm bir klasörü giriş değeri olarak yüklemenizi sağlar.
    
- **Open file as input:** Bir dosyayı giriş değeri olarak yüklemenizi sağlar.
    
- **Clear input and output:** Girilen giriş değerlerini ve karşılık gelen çıkış değerlerini temizler.
    
- **Reset pane layout:** Arayüzü varsayılan pencere boyutlarına getirir.
    

---

### 4. Output Area (Çıkış Alanı)

Çıkış alanı, veri işleme sonuçlarını sergileyen görsel bir alandır. Giriş verilerine uyguladığınız manipülasyonların veya dönüşümlerin sonuçlarını net bir şekilde sunar.

**Özellikler şunları içerir:**

- **Save output to file:** Sonucu bir `.dat` dosyası olarak kaydetmenizi sağlar.
    
- **Copy raw output to the clipboard:** Çıkışı doğrudan panoya kopyalamanızı sağlar.
    
- **Replace input with output:** Giriş verilerini, işlemlerden elde edilen sonuçlarla hızlıca değiştirmenizi (üzerine yazmanızı) sağlar.
    
- **Maximise output pane:** Çıkış panelini tam boyuta getirir.