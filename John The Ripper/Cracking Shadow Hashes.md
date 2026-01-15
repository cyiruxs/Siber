# /etc/shadow Dosyasından Hash Kırma (Cracking Hashes from /etc/shadow)

`/etc/shadow` dosyası, Linux makinelerinde parola hash'lerinin saklandığı dosyadır. Ayrıca son parola değiştirme tarihi ve parola sona erme bilgileri gibi diğer bilgileri de saklar. Sistemdeki her kullanıcı veya kullanıcı hesabı için satır başına bir giriş içerir. Bu dosyaya genellikle yalnızca **root** kullanıcısı erişebilir, bu nedenle hash'lere erişmek için yeterli ayrıcalıklara sahip olmanız gerekir. Ancak, eğer erişiminiz varsa, hash'lerden bazılarını kırma şansınız vardır.

### Unshadowing (Gölgeden Çıkarma)

John the Ripper, verilerle çalışabilmek için verilerin sunulduğu formatlar konusunda çok titiz olabilir; bu nedenle, `/etc/shadow` parolalarını kırmak için John'un kendisine verilen veriyi anlayabilmesi amacıyla bu dosyayı `/etc/passwd` dosyası ile birleştirmeniz gerekir. Bunu yapmak için John araç setine dahil olan **unshadow** adlı bir aracı kullanırız. `unshadow` aracının temel sözdizimi şöyledir:

`unshadow [passwd yolu] [shadow yolu]`

- **unshadow**: Unshadow aracını çağırır.
    
- **[path to passwd]**: Hedef makineden aldığınız `/etc/passwd` dosyasının kopyasını içeren dosyadır.
    
- **[path to shadow]**: Hedef makineden aldığınız `/etc/shadow` dosyasının kopyasını içeren dosyadır.
    

Örnek Kullanım:

unshadow local_passwd local_shadow > unshadowed.txt

#### Dosyalar Hakkında Not (Note on the files)

`unshadow` kullanırken, eğer elinizde mevcutsa `/etc/passwd` ve `/etc/shadow` dosyalarının tamamını kullanabilir veya her birinden ilgili satırı alabilirsiniz:

DOSYA 1 - local_passwd

root kullanıcısı için /etc/passwd satırını içerir:

root:x:0:0::/root:/bin/bash

DOSYA 2 - local_shadow

root kullanıcısı için /etc/shadow satırını içerir:

root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::

---

### Kırma İşlemi (Cracking)

Daha sonra `unshadow` çıktısını (örneğimizde `unshadowed.txt` olarak adlandırdık) doğrudan John'a besleyebiliriz. Girdiyi özel olarak John için hazırladığımızdan burada bir mod belirtmemize gerek kalmamalıdır; ancak bazı durumlarda, daha önce yaptığımız gibi formatı belirtmeniz gerekebilir:

`john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt`

---

### 🛡️ Siber Güvenlik ve CTF İpucu

1. Neden Unshadow Yapıyoruz?

John, hash'i kırarken kullanıcı adı, UID ve ana dizin gibi bilgilere ihtiyaç duyar. /etc/shadow sadece hash'i içerirken, /etc/passwd bu diğer bilgileri içerir. unshadow bunları John'un anlayacağı tek bir satırda birleştirir.

2. SHA-512 ($6$) Tanıma:

Örnekteki $6$ öneki, bunun SHA-512 algoritması ile hash'lendiğini gösterir. Bu algoritma oldukça güçlüdür ve kırması MD5'e göre çok daha uzun sürer.

3. Tek Bir Kullanıcıyı Kırmak:

Büyük bir sistemde yüzlerce kullanıcı olabilir. Hepsini kırmaya çalışmak yerine sadece ilgilendiğin kullanıcının (örn: root) satırlarını alıp unshadow yapman zaman kazandırır.