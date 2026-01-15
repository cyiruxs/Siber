# John the Ripper: Single Crack Modu

Şimdiye kadar, basit ve pek de basit olmayan hash'leri kırmak için John'un kelime listesi (wordlist) modunu kullandık. Ancak John'un **Single Crack** modu adında başka bir modu daha vardır. Bu modda John, kullanıcı adındaki harfleri ve sayıları sezgisel (heuristically) olarak hafifçe değiştirerek olası parolaları bulmak için yalnızca kullanıcı adında sağlanan bilgileri kullanır.

### Kelime Evirme (Word Mangling)

Single Crack modunu ve "word mangling" işlemini açıklamanın en iyi yolu bir örnek üzerinden gitmektir: "Markus" kullanıcı adını ele alalım. Bazı olası parolalar şunlar olabilir:

- Markus1, Markus2, Markus3 (vb.)
    
- MArkus, MARkus, MARKus (vb.)
    
- Markus!, Markus$, Markus* (vb.)
    

Bu tekniğe **word mangling** denir. John, kendisine beslenen bilgilere dayanarak kendi sözlüğünü oluşturur ve kırmaya çalıştığınız hedefle ilgili faktörlere dayalı bir kelime listesi üretmek için başlangıç kelimesini nasıl değiştirebileceğini tanımlayan "mangling kuralları" (mangling rules) setini kullanır. Bu mod, kullanıcı adı veya giriş yapılan servis hakkındaki bilgilere dayanan zayıf parolaları istismar eder.

---

### GECOS Alanı

John'un word mangling uygulaması, UNIX ve Linux gibi UNIX benzeri işletim sistemlerindeki **GECOS** alanı ile uyumluluk özelliğine de sahiptir. GECOS, "General Electric Comprehensive Operating System" anlamına gelir. Önceki görevde `/etc/shadow` ve `/etc/passwd` girişlerine bakmıştık. Yakından bakarsanız, alanların iki nokta üst üste `:` ile ayrıldığını fark edeceksiniz. Kullanıcı hesabı kaydındaki beşinci alan GECOS alanıdır. Bu alan; kullanıcının tam adı, ofis numarası ve telefon numarası gibi genel bilgileri saklar. John, Single Crack modu ile `/etc/shadow` hash'lerini kırarken, oluşturduğu kelime listesine eklemek için tam ad ve ev dizini adı gibi bu kayıtlarda saklanan bilgileri alabilir.

---

### Single Crack Modunu Kullanma

Single Crack modunu kullanmak için şimdiye kadar kullandığımıza benzer bir sözdizimi kullanırız; örneğin, "Mike" adlı kullanıcının parolasını single mod kullanarak kırmak isteseydik şunu kullanırdık:

`john --single --format=[format] [dosya yolu]`

- **`--single`**: John'a "single" hash kırma modunu kullanmak istediğinizi bildirir.
    
- **`--format=[format]`**: Her zaman olduğu gibi, doğru formatı tanımlamak hayati önem taşır.
    

**Örnek Kullanım:** `john --single --format=raw-sha256 hashes.txt`

> [!IMPORTANT] **Dosya Formatları Hakkında Not:** Single Crack modunda hash kırıyorsanız, John'un hangi veriden kelime listesi oluşturacağını anlaması için ona beslediğiniz dosya formatını değiştirmeniz gerekir. Bunu, hash'in başına ait olduğu kullanıcı adını ekleyerek yaparsınız. Yukarıdaki örneğe göre `hashes.txt` dosyasını şu hale getiririz:
> 
> **Eski hali:** `1efee03cdcb96d90ad48ccc7b8666033` **Yeni hali:** `mike:1efee03cdcb96d90ad48ccc7b8666033`

---

### 🛡️ Siber Güvenlik ve CTF İpucu

**1. Neden Single Crack?** Birçok kullanıcı, parolasını belirlerken kullanıcı adını, adını-soyadını veya çalıştığı departmanı temel alır (Örn: `Ahmet123`). Single Crack modu, devasa wordlist'leri taramak yerine bu psikolojik hatayı hedef aldığı için çok daha hızlı sonuç verebilir.

**2. Veri Hazırlama:** Eğer elinde sadece bir hash varsa ve kullanıcı adının "Joker" olduğunu biliyorsan, John'un çalışması için dosyayı mutlaka `Joker:HASH_DEĞERİ` şeklinde düzenlemelisin. Aksi takdirde John, kime göre "mangling" yapacağını bilemez.

**3. Karma Kurallar:** Eğer Single Crack modu başarısız olursa, John'un yapılandırma dosyasındaki (`john.conf`) mangling kurallarını değiştirerek daha agresif denemeler yapmasını sağlayabilirsin.