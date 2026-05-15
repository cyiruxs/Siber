## Extractors (Ayıklayıcılar)

Aşağıdaki tabloda belirtilen spesifik işlemler **Extractors** kategorisi altında yer almaktadır.

|**İşlem (Operation)**|**Açıklama**|
|---|---|
|**Extract IP addresses**|Tüm IPv4 ve IPv6 adreslerini ayıklar.|
|**Extract URLs**|Girdiden **Uniform Resource Locators** (URL'leri) ayıklar. Protokol (HTTP, FTP vb.) gereklidir, aksi takdirde çok fazla **false positive** (hatalı tespit) oluşacaktır.|
|**Extract email addresses**|Girdideki tüm e-posta adreslerini ayıklar.|

- **Extract IP addresses:** Herhangi bir girdiden geçerli tüm IPv4/6 adreslerini ayıklayacaktır. Ağ temellerini hızlıca hatırlamak için mevcut "Networking Concepts" odamızı kontrol etmenizi öneririz.
    
- **Extract email addresses:** `herhangi_bir_sey@domain[.]com` formatındaki tüm dizgileri ve karakterleri ayıklar. Örnek alan adları arasında `hotmail.com`, `google.com`, `tryhackme.com` ve `yahoo.com` bulunur.
    
- **Extract URLs:** Yaygın olarak URL olarak bilinen **Uniform Resource Locator**'ları ayıklar. URL, internet üzerindeki kaynaklara erişmek için kullanılan adrestir. URL'ler ve web uygulamaları hakkında daha derinlemesine bilgi edinmek isterseniz "Web Applications Basics" odasını kontrol edebilirsiniz.
    

---

## Date and Time (Tarih ve Saat)

Aşağıdaki tabloda yer alan spesifik işlemler **Date / Time** kategorisi altında yer almaktadır.

|**İşlem (Operation)**|**Açıklama**|
|---|---|
|**From UNIX Timestamp**|Bir **UNIX timestamp** değerini bir tarih-saat (**datetime**) dizgisine dönüştürür.|
|**To UNIX Timestamp**|UTC formatındaki bir tarih-saat dizgisini analiz eder ve karşılık gelen **UNIX timestamp** değerini döndürür.|

**UNIX timestamp**, 1 Ocak 1970 UTC'den (**UNIX epoch**) bu yana geçen saniye sayısını temsil eden 32 bitlik bir değerdir. "Fri Sep 6 20:30:22 +04 2024" tarihini bir **UNIX Timestamp**'e dönüştürmek için **To UNIX Timestamp** işlemini kullanın; sonuç `1725654622` olacaktır. Eğer bunu tekrar daha okunabilir bir formata dönüştürmek isterseniz **From UNIX Timestamp** işlemini kullanabilirsiniz.

---

## Data Format (Veri Formatı)

Aşağıdaki tabloda yer alan spesifik işlemler **Data format** kategorisi altında yer almaktadır.

|**İşlem (Operation)**|**Açıklama**|**Örnekler**|
|---|---|---|
|**From Base64**|Bu işlem, veriyi bir ASCII **Base64** dizgisinden ham (**raw**) formatına geri döndürür (decode eder).|`V2VsY29tZSB0byB0cnloYWNrbWUh` -> `Welcome to tryhackme!`|
|**URL Decode**|**URI/URL** yüzde kodlamalı (**percent-encoded**) karakterleri ham değerlerine geri dönüştürür.|`https%3A%2F%2Fgchq%2Egithub%2Eio%2FCyberChef%2F` -> `[https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/)`|
|**From Base85**|Rastgele bayt verilerini kodlamak için kullanılan bir notasyondur. Genellikle **Base64**'ten daha verimlidir. Bu işlem, (seçeceğiniz bir alfabe ve hazır ayarlar dahil) bir ASCII dizgisinden veriyi çözer.|`BOu!rD]j7BEbo7` -> `hello world`|
|**From Base58**|Rastgele bayt verilerini kodlamak için kullanılan bir notasyondur. İnsan okunabilirliğini artırmak için kolayca yanlış okunan karakterleri (yani l, I, 0 ve O) çıkararak **Base64**'ten ayrılır.|`AXLU7qR` -> `Thm58`|
|**To Base62**|İnsanların rahatça kullanabileceği ve bilgisayarlar tarafından işlenebilen kısıtlı bir sembol seti kullanarak veriyi kodlar. Yüksek taban sayısı, ondalık veya heksadesimal sisteme göre daha kısa dizgiler üretilmesini sağlar.|`Thm62` -> `6NiRkOY`|

**Base(64, 85, 58, 62)** gibi işlemler **base encodings** (taban kodlamaları) olarak bilinir. **Base encoding**, ikili verileri (0 ve 1 dizilerini) alır ve belirli bir **ASCII** (**American Standard Code for Information Interchange**) karakter seti kullanarak metin tabanlı bir temsile dönüştürür.

### Manuel Base64 Dönüşümü: "THM" Örneği

Örneğimiz "THM" harflerini kodlamak olacaktır. Burada referans olarak kullanabileceğimiz kısa bir **ASCII Tablosu** bulunmaktadır. (Tam tabloya dış bağlantılardan ulaşabilirsiniz).

|**Ondalık (Dec)**|**İkili (Binary)**|**Sembol**|**Ondalık (Dec)**|**İkili (Binary)**|**Sembol**|
|---|---|---|---|---|---|
|65|01000001|**A**|78|01001110|**N**|
|66|01000010|**B**|79|01001111|**O**|
|67|01000011|**C**|80|01010000|**P**|
|68|01000100|**D**|81|01010001|**Q**|
|69|01000101|**E**|82|01010010|**R**|
|70|01000110|**F**|83|01010011|**S**|
|71|01000111|**G**|84|01010100|**T**|
|72|01001000|**H**|85|01010101|**U**|
|73|01001001|**I**|86|01010110|**V**|
|74|01001010|**J**|87|01010111|**W**|
|75|01001011|**K**|88|01011000|**X**|
|76|01001100|**L**|89|01011001|**Y**|
|77|01001101|**M**|90|01011010|**Z**|

**Adım 1: İkili Sisteme Dönüştürme ve Birleştirme (Manuel)**

Tablomuza göre; **T = 01010100**, **H = 01001000**, **M = 01001101**. Ardından bu ikilileri birleştirin ve toplamda 24 karakter olduklarından emin olun: `010101000100100001001101`

**Adım 2: Bölme ve Ondalık Sisteme Dönüştürme (Manuel)**

`010101000100100001001101` dizisini 6'şar karakterlik parçalara ayırın. Elinizde şu dört grup olmalı: `010101` | `000100` | `100001` | `001101`. Bunlar 6 bitlik karakterlerdir; şu an bu gruplardan dört adet olmalı. Şimdi her bir grubu ondalık (**Decimal**) sisteme çevirelim!

|**İkili (Binary)**|**Ondalık (Base10)**|
|---|---|
|`010101`|**21**|
|`000100`|**4**|
|`100001`|**33**|
|`001101`|**13**|

**Adım 3: Base64 İndeksine Dönüştürme (Manuel)**

Önceki adımdan elde ettiğimiz numaralar olan **21, 4, 33 ve 13** için aşağıdaki tabloyu kullanarak eşdeğer karakterleri arayalım. Bu tablo bir **Base64 Index Table**'dır.

|**İndeks**|**Karakter**|**İndeks**|**Karakter**|**İndeks**|**Karakter**|
|---|---|---|---|---|---|
|0|A|26|a|52|0|
|4|**E**|30|e|56|4|
|13|**N**|39|n|65|+|
|21|**V**|47|v|73|/|
|33|**h**|59|7|||

_(Not: Tablo örnektir, 21=V, 4=E, 33=h, 13=N değerlerini doğrular)._

Karakterleri birleştirdiğinizde "THM" ifadesinin **Base64** formatındaki karşılığını elde edersiniz. Cevap **VEhN** olacaktır.

Vay be! Bu harika değil mi? Bir grup karakteri manuel olarak **Base64**'e dönüştürdünüz.

Şimdi **URL Decode** işlemini ele alalım. Bu işlem, yüzde kodlamalı (**percent-encoded**) karakterleri tekrar ham değerlerine dönüştürerek çalışır. HTML5'teki varsayılan karakter seti **UTF-8**'dir. Bir URL'de tipik olarak görebileceğimiz karakterler için aşağıdaki tabloya göz atın:

|**Karakterler**|**UTF-8 Karşılığı**|
|---|---|
|`:`|`%3A`|
|`/`|`%2F`|
|`.`|`%2E`|
|`=`|`%3D`|
|`#`|`%23`|