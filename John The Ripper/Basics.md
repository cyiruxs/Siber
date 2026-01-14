# Hash Nedir? (What are Hashes?)

Bir hash (özet), herhangi bir uzunluktaki bir veri parçasını alıp onu başka bir **sabit uzunluktaki formda temsil etme** yoludur. Bu işlem verinin orijinal değerini maskeler. Hash değeri, orijinal verinin bir hashing algoritmasından geçirilmesiyle elde edilir. MD4, **MD5**, SHA1 ve **NTLM** gibi birçok popüler hashing algoritması mevcuttur. Bunu bir örnekle göstermeyi deneyelim:

Dört karakterli bir dize olan "polo"yu alır ve bir **MD5** hashing algoritmasından geçirirsek, standart 32 karakterli bir MD5 hash'i olan `b53759f3ce692de7aff1b5779d3964da` çıktısını elde ederiz.

Aynı şekilde, 9 karakterli bir dize olan "polomints"i alır ve aynı MD5 hashing algoritmasından geçirirsek, yine başka bir standart 32 karakterli **MD5** hash'i olan `584b6e4f4586e136bc280f27f9c64f3b` çıktısını elde ederiz.

---

### Hash'leri Güvenli Kılan Nedir? (What Makes Hashes Secure?)

Hashing fonksiyonları **tek yönlü fonksiyonlar** (one-way functions) olarak tasarlanmıştır. Diğer bir deyişle, verilen bir girdinin hash değerini hesaplamak kolaydır; ancak, hash değeri verildiğinde orijinal girdiyi bulmak zor bir problemdir. Basit terimlerle, bilgisayar biliminde "zor bir problem", hesaplama açısından hızla imkansız (computationally infeasible) hale gelir. Bu hesaplama problemi, köklerini matematikteki **P vs NP** probleminden alır.

Bilgisayar biliminde P ve NP, algoritmaların verimliliğini anlamamıza yardımcı olan iki problem sınıfıdır:

- **P (Polynomial Time - Polinom Zaman):** Çözümü polinom zamanda bulunabilen problemleri kapsar. Bir listeyi artan düzende sıralamayı düşünün. Liste ne kadar uzunsa sıralamak o kadar uzun sürer; ancak zamandaki artış üstel (exponential) değildir.
    
- **NP (Non-deterministic Polynomial Time - Deterministik Olmayan Polinom Zaman):** NP sınıfındaki problemler, çözümün kendisini bulmak zor olsa bile, verilen bir çözümün hızlıca kontrol edilebildiği problemlerdir. Aslında, çözümü bulmak için en başta hızlı bir algoritma olup olmadığını bile bilmiyoruz.
    

Bu, bilgisayar ve kriptografi için temel teşkil eden büyüleyici bir matematiksel kavram olsa da, tamamen bu odanın kapsamı dışındadır. Ancak soyut olarak, değeri hash'leyen algoritma "P" olacaktır ve bu nedenle makul bir şekilde hesaplanabilir. Bununla birlikte, bir "un-hashing" (hash geri döndürme) algoritması "NP" olacaktır ve çözülmesi imkansız (intractable) olacaktır; yani standart bilgisayarlar kullanılarak makul bir sürede hesaplanamaz.

---

### John Burada Devreye Girer (Where John Comes in)

Algoritma uygulanabilir bir şekilde tersine çevrilebilir olmasa bile, bu hash'leri kırmanın imkansız olduğu anlamına gelmez. Örneğin, bir parolanın hash'lenmiş versiyonuna sahipseniz ve hashing algoritmasını biliyorsanız, bu algoritmayı **sözlük** (dictionary) adı verilen çok sayıda kelimeyi hash'lemek için kullanabilirsiniz. Daha sonra bu hash'leri kırmaya çalıştığınız hash ile karşılaştırarak eşleşip eşleşmediklerini görebilirsiniz. Eğer eşleşirlerse, o hash'e hangi kelimenin karşılık geldiğini bilirsiniz; yani onu kırmış olursunuz!

Bu işleme **sözlük saldırısı** (dictionary attack) denir ve **John the Ripper** (veya yaygın olarak kısaltıldığı adıyla John), çeşitli hash türleri üzerinde hızlı kaba kuvvet (brute force) saldırıları yürütmek için kullanılan bir araçtır.

---

### Daha Fazlasını Öğrenmek (Learning More)

Şifreleme ve deşifreleme hakkında daha derinlemesine materyal için **Cryptography Basics** ve **Public Key Cryptography Basics** odalarını; ayrıca hashing için **Hashing Basics** odasını tavsiye ederiz.

Bu oda, John the Ripper'ın en popüler genişletilmiş versiyonu olan **Jumbo John** üzerine odaklanacaktır.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

**1. John the Ripper (JtR) Neden "Jumbo"?** Standart John'a kıyasla "Jumbo John", topluluk tarafından geliştirilen ve çok daha fazla hash tipini (yüzlerce farklı algoritma) destekleyen versiyondur. CTF'lerde genellikle bu versiyonu kullanırsın.

**2. Kırmadan Önce Format Belirleme:** John genellikle hash tipini otomatik algılar. Ancak bazen manuel belirtmek gerekebilir. Örn: `john --format=raw-md5 hash.txt --wordlist=rockyou.txt`

**3. İşlem Durumunu Takip Etmek:** Kırma işlemi devam ederken terminalde herhangi bir tuşa (boşluk veya enter gibi) basarsan, John sana o anki hızını (CPS - characters per second) ve ne kadarının tamamlandığını gösterir.