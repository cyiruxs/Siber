# Veri Bütünlüğü ve HMAC (Data Integrity and HMACs)

Görev 3'te, hashing'in iki kullanım alanına odaklanacağımızı belirtmiştik: parola saklama ve veri bütünlüğü. Hashing'in kimlik doğrulama sistemlerinde parolaları nasıl güvence altına aldığını kapsamlı bir şekilde tartıştık. Bu görevde, dosyaların bütünlüğünü kontrol etmek için hash fonksiyonlarını nasıl kullanabileceğimizi tartışacağız.

### Bütünlük Kontrolü (Integrity Checking)

Hashing, dosyaların değiştirilmediğini kontrol etmek için kullanılabilir. Aynı veriyi girdi olarak verirseniz, her zaman aynı çıktıyı alırsınız. Görev 2'de gösterildiği gibi, tek bir bit bile değişse hash değeri önemli ölçüde değişecektir. Bu, bir dosyanın modifiye edilip edilmediğini kontrol etmek veya indirdiğiniz dosyanın web sunucusundaki dosya ile tamamen aynı olduğundan emin olmak için hashing'i kullanabileceğiniz anlamına gelir.

Aşağıdaki metin dosyası, iki Fedora Workstation ISO dosyasının SHA256 hash değerini göstermektedir. İndirdiğiniz dosya üzerinde `sha256sum` komutunu çalıştırdığınızda, bu imzalı dosyada listelenen hash değeri ile aynı sonucu alıyorsanız, dosyanızın orijinal dosya ile birebir aynı olduğundan emin olabilirsiniz.

**AttackBox Terminal**

Bash

```
root@AttackBox# head Fedora-Workstation-40-1.14-x86_64-CHECKSUM
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

# Fedora-Workstation-Live-osb-40-1.14.x86_64.iso: 2623733760 bytes
SHA256 (Fedora-Workstation-Live-osb-40-1.14.x86_64.iso) = 8d3cb4d99f27eb932064915bc9ad34a7529d5d073a390896152a8a899518573f

# Fedora-Workstation-Live-x86_64-40-1.14.iso: 2295853056 bytes
SHA256 (Fedora-Workstation-Live-x86_64-40-1.14.iso) = dd1faca950d1a8c3d169adf2df4c3644ebb62f8aac04c401f2393e521395d613
[...]
```

Ayrıca hashing'i kopya dosyaları bulmak için de kullanabilirsiniz; eğer iki belgenin hash değerleri aynıysa, bunlar aynı belgedir. Bu, kopya dosyaları bulup silmek için oldukça kullanışlıdır.

---

### HMAC'ler (Keyed-Hash Message Authentication Code)

**HMAC**, verilerin hem orijinalliğini hem de bütünlüğünü doğrulamak için bir kriptografik hash fonksiyonunu gizli bir anahtar (secret key) ile birleştiren bir mesaj doğrulama kodu (MAC) türüdür.

Bir HMAC, mesajı oluşturan kişinin söylediği kişi olduğundan emin olmak (yani **kimlik doğrulaması / authenticity**) için kullanılabilir; ayrıca mesajın değiştirilmediğini veya bozulmadığını (yani **bütünlük / integrity**) kanıtlar. Bu, kimliği kanıtlamak için gizli bir anahtar ve bütünlüğü kanıtlamak için bir hashing algoritması kullanılarak elde edilir.

HMAC'in nasıl çalıştığına dair genel adımlar şunlardır:

1. Gizli anahtar (secret key), hash fonksiyonunun blok boyutuna kadar doldurulur (padded).
    
2. Doldurulan anahtar, bir sabit ile (genellikle sıfırlar veya birlerden oluşan bir blok) **XOR** işlemine tabi tutulur.
    
3. Mesaj, XOR'lanmış anahtar kullanılarak hash fonksiyonu ile hash'lenir.
    
4. Adım 3'teki sonuç, aynı hash fonksiyonu ile tekrar hash'lenir ancak bu sefer doldurulmuş anahtarın başka bir sabit ile XOR'lanmış hali kullanılır.
    
5. Nihai çıktı, genellikle sabit boyutlu bir dize olan HMAC değeridir.
    

Teknik olarak konuşmak gerekirse, HMAC fonksiyonu şu ifade kullanılarak hesaplanır:

$$HMAC(K,M) = H((K \oplus opad) || H((K \oplus ipad) || M))$$

_Not: $M$ mesajı, $K$ ise anahtarı temsil eder._

---

### 🛡️ Siber Güvenlik ve CTF İpucu

1. Dosya Doğrulama:

Bir CTF sırasında şüpheli bir binary (dosya) indirdiğinde, dosyanın gerçekten orijinal olup olmadığını anlamak için hash değerini alıp "VirusTotal" gibi platformlarda aratabilirsin. Eğer hash biliniyorsa, dosyanın türü ve içeriği hakkında hızlı bilgi alırsın.

2. HMAC ve Web Güvenliği (JWT):

HMAC'ler modern web uygulamalarında, özellikle JSON Web Tokens (JWT) içinde sıkça kullanılır. JWT'nin son kısmı bir HMAC imzasıdır. Eğer sunucu tarafındaki gizli anahtarı ele geçirirsen (veya anahtar çok zayıfsa ve brute force ile kırılırsa), kendi sahte token'larını oluşturabilir ve sistemde admin yetkisi kazanabilirsin.

3. Hashing ile Hızlı Karşılaştırma:

Büyük veritabanlarında veya dosya sistemlerinde iki dosyanın aynı olup olmadığını bayt bayt kontrol etmek yerine hash'lerini karşılaştırmak çok daha performanslıdır.