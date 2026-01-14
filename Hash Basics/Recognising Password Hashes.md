# Hash Tanıma ve Kırma: Ofansif Bakış Açısı

Siber savunma tarafında parolaların nasıl güvenli saklanacağını inceledik. Şimdi ise madalyonun diğer yüzüne, ofansif güvenliğe bakalım: Elimizde bir hash varsa, bunun türünü nasıl anlarız, nasıl kırarız ve orijinal parolayı nasıl elde ederiz?

**hashID** gibi otomatik hash tanıma araçları mevcuttur ancak birçok format için güvenilmez olabilirler. Öneki (prefix) olan hash'ler için bu araçlar daha tutarlıdır. En iyi yöntem, araçları ve bağlamı (context) birlikte kullanmaktır. Örneğin, bir web uygulaması veritabanında bulduğunuz hash'in **NTLM** (NT LAN Manager) olma ihtimali, **MD5** olma ihtimalinden çok daha düşüktür. Otomatik araçlar bu türleri karıştırabildiği için kendi bilginizi geliştirmeniz kritiktir.

---

### Linux Parolaları

Linux sistemlerde parola hash'leri `/etc/shadow` dosyasında saklanır ve normalde sadece **root** kullanıcısı tarafından okunabilir. Eskiden herkes tarafından okunabilen `/etc/passwd` dosyasında saklanırlardı.

`shadow` dosyasındaki her satır, kolonlarla (:) ayrılmış dokuz alandan oluşur. İlk iki alan kullanıcı adı ve şifrelenmiş paroladır. Diğer alanlar hakkında daha fazla bilgi için sistemde `man 5 shadow` komutunu çalıştırabilirsiniz.

Şifrelenmiş parola alanı dört bileşen içerir: **prefix** (algoritma kimliği), **options** (parametreler), **salt** ve **hash**. Bu veri `$prefix$options$salt$hash` formatında kaydedilir. **Prefix**, kullanılan hashing algoritmasını belirlediği için Unix ve Linux tarzı parolaları tanımayı kolaylaştırır.

Aşağıda, en yaygın Unix tarzı parola öneklerini (azalan güç sırasına göre) bulabilirsiniz:

|**Prefix**|**Algoritma**|**Açıklama**|
|---|---|---|
|**$y$**|**yescrypt**|Ölçeklenebilir bir şema; yeni sistemlerde varsayılan ve önerilen tercihtir.|
|**$gy$**|**gost-yescrypt**|GOST R 34.11-2012 hash fonksiyonu ve yescrypt metodunu kullanır.|
|**$7$**|**scrypt**|Parola tabanlı bir anahtar türetme (KDF) fonksiyonudur.|
|**$2b, 2y, 2a, 2x$**|**bcrypt**|Blowfish blok şifrelemesine dayalıdır; modern birçok Linux ve BSD sürümünde desteklenir.|
|**$6$**|**sha512crypt**|512-bit çıktılı SHA-2 tabanlıdır; eski Linux sistemlerinde yaygındır.|
|**$md5**|**SunMD5**|MD5 tabanlıdır; aslen Solaris için geliştirilmiştir.|
|**$1$**|**md5crypt**|FreeBSD için geliştirilen MD5 tabanlı bir hash yöntemidir.|

#### Modern Linux Örneği

Modern bir Linux sisteminin `shadow` dosyasından alınan şu satırı inceleyelim:

**Terminal**

Bash

```
root@TryHackMe# sudo cat /etc/shadow | grep strategos
strategos:$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4:19965:0:99999:7:::
```

Burada `$` işaretleriyle ayrılmış dört ana parça vardır:

1. **y:** Kullanılan algoritmayı belirtir (**yescrypt**).
    
2. **j9T:** Algoritmaya iletilen bir parametredir.
    
3. **76UzfgEM5PnymhQ7TlJey1:** Kullanılan **salt** değeridir.
    
4. **/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4:** Asıl **hash** değeridir.
    

---

### MS Windows Parolaları

Windows parolaları, MD4'ün bir varyantı olan **NTLM** kullanılarak hash'lenir. Görsel olarak MD4 ve MD5 hash'leri ile tıpatıp aynıdırlar; bu nedenle hash türünü belirlemek için bağlamı (context) kullanmak çok önemlidir.

Windows'ta parola hash'leri **SAM** (Security Accounts Manager) içinde saklanır. Windows normal kullanıcıların bunları dökmesini (dump) engellemeye çalışır, ancak **mimikatz** gibi araçlar bu güvenliği aşmak için mevcuttur. Orada bulunan hash'ler genellikle **NT hashes** ve **LM hashes** olarak ikiye ayrılır.

Farklı hash formatlarını ve öneklerini bulmak için en iyi kaynak **Hashcat Example Hashes** sayfasıdır. Diğer hash türleri için genellikle uzunluk, kodlama veya hash'i üreten uygulama üzerinde araştırma yapmanız gerekir. Araştırmanın gücünü asla küçümsemeyin.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

1. Hashcat Modlarını Belirleme:

CTF'lerde bir hash kıralacağı zaman Hashcat kullanılır. Hashcat her algoritma için bir "mode" numarası ister. Örneğin:

- MD5 için: `-m 0`
    
- SHA256 için: `-m 1400`
    
- NTLM için: `-m 1000`
    
- Linux SHA512 ($6$) için: `-m 1800`
    

2. Hash Uzunluğu Analizi:

Eğer bir prefix yoksa, hash'in uzunluğu size ipucu verir:

- 32 karakter (Hex) -> MD5 (128 bit)
    
- 40 karakter (Hex) -> SHA-1 (160 bit)
    
- 64 karakter (Hex) -> SHA-256 (256 bit)
    

3. Online Hash Cracking:

Hash'i kırmak için kendi kaynaklarını harcamadan önce her zaman CrackStation veya Hashes.com gibi veritabanlarını kontrol et abi. Eğer bilinen bir parola ise saniyeler içinde cevabı alırsın.