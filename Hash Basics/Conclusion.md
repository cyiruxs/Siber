# Hashing, Encoding ve Encryption Arasındaki Farklar

Bu oda, hash fonksiyonlarını ve kullanım alanlarını çeşitli açılardan ele aldı. Devam etmeden önce **hashing**, **encoding** (kodlama) ve **encryption** (şifreleme) arasındaki farkları net bir şekilde ayırt etmeliyiz.

### Hashing (Özetleme)

Daha önce de belirtildiği gibi hashing, girdi verisini alan ve **digest** (özet) olarak da adlandırılan sabit boyutlu bir karakter dizisi (hash değeri) üreten bir işlemdir. Bu hash değeri veriyi benzersiz bir şekilde temsil eder ve verideki en küçük değişiklik bile hash değerinin değişmesine neden olur. Hashing, şifreleme veya kodlama ile karıştırılmamalıdır; hashing **tek yönlüdür** ve orijinal veriyi elde etmek için işlemi geri döndüremezsiniz.

### Encoding (Kodlama)

**Encoding**, veriyi belirli bir sistemle uyumlu hale getirmek için bir formdan diğerine dönüştürür. ASCII, UTF-8, UTF-16, UTF-32, ISO-8859-1 ve Windows-1252, İngiliz dili için geçerli kodlama yöntemleridir. UTF-8, UTF-16 ve UTF-32'nin Unicode kodlamaları olduğunu ve Arapça, Japonca gibi diğer dillerdeki karakterleri de temsil edebildiğini unutmayın.

Veri gönderirken veya kaydederken yaygın olarak kullanılan bir başka kodlama türü ise belirli bir dile özgü değildir. Örnekler arasında **Base32** ve **Base64** kodlaması yer alır. Kodlama ve kod çözme (decoding) için `base64` kullanımına dair aşağıdaki örneği inceleyin:

**Terminal**

Bash

```
strategos@g5000 ~> echo "TryHackMe" | base64
VHJ5SGFja01lCg==
strategos@g5000 ~> echo "VHJ5SGFja01lCg==" | base64 -d
TryHackMe
```

Encoding, mesajın gizliliğini (**confidentiality**) korumadığı için şifreleme ile karıştırılmamalıdır. Encoding **tersine çevrilebilir** bir işlemdir; doğru araçlara sahip olan herkes verinin kodlamasını değiştirebilir.

### Encryption (Şifreleme)

Sadece önceki odalarda işlediğimiz **encryption**, kriptografik bir algoritma (cipher) ve bir anahtar (key) kullanarak veri gizliliğini korur. Şifreleme, algoritmayı bildiğimiz ve anahtara erişebildiğimiz sürece tersine çevrilebilir bir işlemdir.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

**1. "Bunu Nasıl Ayırt Ederim?" Tablosu:**

|**Özellik**|**Hashing**|**Encoding**|**Encryption**|
|---|---|---|---|
|**Amacı**|Veri bütünlüğü & Kimlik doğrulama|Veri uyumluluğu & İletim|Gizlilik & Güvenlik|
|**Geri Döndürülebilir mi?**|Hayır (Tek Yönlü)|Evet (Algoritma bellidir)|Evet (Anahtar gereklidir)|
|**Anahtar Kullanır mı?**|Hayır (HMAC hariç)|Hayır|Evet|
|**Çıktı Boyutu**|Sabit|Değişken|Değişken|

2. CTF'lerde Base64 Tanıma:

Eğer bir metnin sonunda = veya == işaretleri görüyorsan, bu %99 ihtimalle bir Base64 kodlamasıdır. Base64 bir şifreleme değildir! Sadece base64 -d komutuyla içeriğini okuyabilirsin.

3. Karmaşık Senaryolar:

Gerçek dünyada bu üçü birlikte kullanılır. Örneğin, bir web sitesine bağlanırken:

1. Parolanız **Hash**'lenerek saklanır (Güvenlik).
    
2. Verileriniz **Encrypt** edilerek gönderilir (Gizlilik - HTTPS).
    
3. Veriler iletilirken **Encode** edilir (Uyumluluk - Base64/UTF-8).