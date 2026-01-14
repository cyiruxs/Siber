# John the Ripper: Temel Hash Kırma (Basic Hashing)

Basit hash'leri kırmak için John the Ripper'ı kullanmanın birden fazla yolu vardır. Kendimiz kırma işlemine geçmeden önce birkaç yöntemi inceleyeceğiz.

### John Temel Sözdizimi (Basic Syntax)

John the Ripper komutlarının temel sözdizimi aşağıdaki gibidir:

`john [seçenekler] [dosya yolu]`

- **`john`**: John the Ripper programını çağırır.
    
- **`[options]`**: Kullanmak istediğiniz seçenekleri belirtir.
    
- **`[file path]`**: Kırmaya çalıştığınız hash'i içeren dosyadır; eğer dosya aynı dizindeyse tam yolu belirtmenize gerek yoktur, sadece dosya adını yazmanız yeterlidir.
    

### Otomatik Kırma (Automatic Cracking)

John, kendisine verilen hash türünü algılamak ve onu kırmak için uygun kuralları ve formatları seçmek üzere yerleşik özelliklere sahiptir. Bu her zaman en iyi fikir değildir çünkü güvenilmez olabilir; ancak hangi hash türüyle çalıştığınızı tanımlayamıyorsanız ve kırmayı denemek istiyorsanız iyi bir seçenek olabilir. Bunu yapmak için aşağıdaki sözdizimini kullanırız:

`john --wordlist=[wordlist yolu] [dosya yolu]`

- **`--wordlist=`**: Belirttiğiniz yoldaki dosyadan okuma yaparak wordlist (kelime listesi) modunu kullanacağınızı belirtir.
    
- **`[path to wordlist]`**: Önceki görevde açıklandığı gibi, kullandığınız wordlist'in yoludur.
    

**Örnek Kullanım:** `john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

---

### Hash'leri Tanımlama (Identifying Hashes)

Bazen John hash'leri otomatik olarak tanıma ve yükleme konusunda pek iyi çalışmaz. Bu durumda, hash'i tanımlamak için diğer araçları kullanabilir ve ardından John'u belirli bir formata ayarlayabiliriz. Bunu yapmak için çevrimiçi hash tanımlama siteleri veya **hash-identifier** gibi araçlar kullanılabilir. `hash-identifier`, kullanımı süper kolay olan bir Python aracıdır; girdiğiniz hash'in hangi türlerde olabileceğini söyler ve ilk seçenek başarısız olursa size daha fazla seçenek sunar.

`hash-identifier` aracını kullanmak için `wget` veya `curl` ile GitLab sayfasından `hash-id.py` dosyasını indirebilir, ardından `python3 hash-id.py` ile çalıştırıp tanımlamak istediğiniz hash'i girebilirsiniz.

**Terminal Uygulaması:**

Bash

```
user@TryHackMe$ wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py
user@TryHackMe$ python3 hash-id.py
...
HASH: 2e728dd31fb5949bc39cac5a9f066498

Olası Hash Türleri:
[+] MD5
[+] Domain Cached Credentials - MD4(MD4(($pass)).(strtolower($username)))
```

---

### Formata Özgü Kırma (Format-Specific Cracking)

Elinizdeki hash'in türünü tanımladıktan sonra, John'a bu formatı kullanarak kırma işlemi yapmasını şu sözdizimiyle söyleyebilirsiniz:

`john --format=[format] --wordlist=[path to wordlist] [path to file]`

- **`--format=`**: John'a belirli bir formatta hash verdiğinizi ve kırma işlemi için bu formatı kullanmasını söyleyen bayraktır (flag).
    
- **`[format]`**: Hash'in içinde bulunduğu format.
    

**Örnek Kullanım:** `john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`

> [!IMPORTANT] **Formatlar Hakkında Not:** John'a format belirtirken, yukarıdaki örnekteki gibi standart bir hash türüyle (örneğin **md5**) uğraşıyorsanız, John'a sadece standart bir hash ile uğraştığınızı anlatmak için başına **`raw-`** ön ekini eklemeniz gerekebilir; ancak bu her zaman geçerli değildir. Ön ek eklemeniz gerekip gerekmediğini kontrol etmek için `john --list=formats` ile tüm formatları listeleyebilir veya `john --list=formats | grep -iF "md5"` gibi bir komutla arama yapabilirsiniz.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

**1. John'un Belleği (Pot):** John, kırdığı hash'leri `.john/john.pot` (veya `/root/.john/john.pot`) adlı bir dosyaya kaydeder. Eğer aynı hash'i tekrar kırmaya çalışırsan John "No password hashes left to crack" der. Daha önce kırdığın şifreyi görmek için: `john --show [dosya_adi]` komutunu kullanmalısın.

**2. Hangi Wordlist?** Genellikle `rockyou.txt` yeterlidir ancak bazı özel CTF'lerde web sitesinden toplanan kelimelerle oluşturulan bir wordlist gerekebilir. Bu durumda `cewl` aracını kullanarak hedefe özel wordlist oluşturup John'a verebilirsin.

**3. Format Karmaşası:** `hash-identifier` MD5 diyorsa ve John `raw-md5` ile kırmıyorsa, bu bir Windows hash'i (NTLM) olabilir. Bu durumda `--format=nt` denemek hayat kurtarır.

---

### Pratik (Practical)

Artık temel hash'leri kırmak için gereken sözdizimini, niteleyicileri ve yöntemleri biliyorsunuz; kendiniz deneyin! Dosyalar, ekli sanal makinedeki `~/John-the-Ripper-The-Basics/Task04/` dizininde bulunmaktadır.