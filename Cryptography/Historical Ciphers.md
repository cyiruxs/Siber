Kriptografinin tarihi M.Ö. 1900'lerde Antik Mısır'a kadar uzanır. Ancak tarihteki en basit ve en bilinen şifreleme yöntemlerinden biri, M.Ö. 1. yüzyılda kullanılan **Caesar Cipher** (Sezar Şifrelemesi) yöntemidir.

---

### Caesar Cipher (Sezar Şifrelemesi) Mantığı

Bu yöntemin temel fikri oldukça basittir: Mesajdaki her harfi, alfabede belirli bir sayı kadar kaydırarak şifrelemek.

**Örnek Senaryo:**

- **Plaintext (Düz Metin):** `TRYHACKME`
    
- **Key (Anahtar):** 3 (Harfleri sağa doğru 3 birim kaydırdığımızı varsayalım.)
    
- **Cipher (Algoritma):** Caesar Cipher
    

Bu durumda:

- `T` harfi `W` olur.
    
- `R` harfi `U` olur.
    
- `Y` harfi `B` olur (Alfabenin sonuna gelindiğinde başa dönülür).
    

Sonuç olarak elde edilen **Ciphertext (Şifreli Metin):** `WUBKDFNPH`

**Deşifreleme İşlemi:** Şifreyi çözmek için aynı anahtarı kullanırız ancak kaydırma yönünü tersine çeviririz. Şifrelerken sağa 3 birim kaydırdıysak, çözerken sola 3 birim kaydırarak orijinal `TRYHACKME` metnine ulaşırız.

---

### Caesar Cipher Neden Güvensizdir?

Günümüz standartlarına göre Sezar Şifrelemesi son derece güvensiz kabul edilir. Bunun temel sebebi, anahtar uzayının çok küçük olmasıdır. İngiliz alfabesi 26 harften oluşur ve bir harfi 26 kez kaydırmak onu yine kendisine döndürür. Bu da denenebilecek sadece **25 geçerli anahtar** olduğu anlamına gelir.

Bir saldırgan, şifreleme yönteminin Sezar Şifrelemesi olduğunu biliyorsa, tüm olasılıkları tek tek deneyerek (**Brute Force**) mesajı saniyeler içinde çözebilir.

---

### Diğer Önemli Tarihsel Şifreler

Tarih boyunca ve popüler kültürde sıkça karşınıza çıkabilecek diğer bazı önemli şifreleme yöntemleri şunlardır:

- **Vigenère Şifresi (16. Yüzyıl):** Sezar şifresinin daha gelişmiş bir versiyonudur ve farklı harfler için farklı kaydırma miktarları (bir anahtar kelime aracılığıyla) kullanır.
    
- **Enigma Makinesi (2. Dünya Savaşı):** Alman ordusu tarafından kullanılan, karmaşık rotor mekanizmalarına sahip elektromekanik bir cihazdır.
    
- **One-Time Pad (Soğuk Savaş):** Eğer anahtar tamamen rastgele ise, mesaj kadar uzunsa ve asla tekrar kullanılmıyorsa, matematiksel olarak kırılamaz olduğu kanıtlanmış tek yöntemdir.