# Zip Dosyalarını Kırma (Cracking Zip Files)

Evet! Doğru okudunuz. John'u, parola korumalı Zip dosyalarındaki parolayı kırmak için de kullanabiliriz. Yine, Zip dosyasını John'un anlayabileceği bir formata dönüştürmek için John araç setinin (suite) ayrı bir parçasını kullanacağız; ancak tüm amaç ve niyetler için halihazırda aşina olduğunuz sözdizimini (syntax) kullanmaya devam edeceğiz.

### Zip2John

Daha önce kullandığımız `unshadow` aracına benzer şekilde, Zip dosyasını John'un anlayabileceği ve umarız kırabileceği bir hash formatına dönüştürmek için **`zip2john`** aracını kullanacağız. Temel kullanımı şöyledir:

`zip2john [seçenekler] [zip dosyası] > [çıktı dosyası]`

- **`[options]`**: `zip2john` aracına belirli sağlama toplamı (checksum) seçeneklerini iletmenize olanak tanır; buna genellikle ihtiyaç duyulmamalıdır.
    
- **`[zip file]`**: Hash değerini almak istediğiniz Zip dosyasının yoludur.
    
- **`>`**: Bu işaret, bu komutun çıktısını başka bir dosyaya yönlendirir.
    
- **`[output file]`**: Çıktıyı saklayacak olan dosyadır.
    

Örnek Kullanım:

zip2john zipfile.zip > zip_hash.txt

---

### Kırma İşlemi (Cracking)

Daha sonra, örneğimizde `zip_hash.txt` olarak adlandırdığımız `zip2john` çıktısını alabiliriz. Tıpkı `unshadow` aracında yaptığımız gibi, bu dosyayı doğrudan John'a besleyebiliriz çünkü girdiyi özel olarak onun için hazırladık.

Terminal Komutu:

john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt

---

### 🛡️ Siber Güvenlik ve CTF İpucu

1. Sadece Zip Değil:

John araç seti içinde sadece zip2john yok abi. CTF'lerde karşına çıkabilecek diğer arşiv türleri için de kardeş araçlar var:

- `rar2john` (RAR dosyaları için)
    
- `7z2john` (7-Zip dosyaları için)
    
- `ssh2john` (Şifreli SSH anahtarları için)
    

2. Hash Dosyasını Temizlemek:

zip2john bazen çıktının başına dosya yolunu veya gereksiz metinleri ekleyebilir. Eğer John "No password hashes loaded" hatası verirse, oluşturduğun .txt dosyasını nano ile açıp sadece zipfile.zip:$pkzip$2$1$2$... ile başlayan hash kısmının kaldığından emin olmalısın.

3. Brute-Force Hızı:

Zip dosyalarını kırmak, sistem hash'lerini kırmaktan (özellikle Bcrypt veya SHA-512) çok daha hızlıdır. Bu yüzden devasa wordlist'ler ve ağır "mangling" kuralları kullanmak burada daha verimlidir.

| **Araç**     | **Hedef Dosya** | **John Formatı** |
| ------------ | --------------- | ---------------- |
| **zip2john** | .zip            | PKZIP / ZIP      |
| **rar2john** | .rar            | RAR / RAR5       |
| **7z2john**  | .7z             | 7z               |