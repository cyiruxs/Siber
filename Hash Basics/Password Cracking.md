# Hash Kırma Yöntemleri ve Araçlar

Tuz (salt) kullanmayan hash'leri kırmak için bir yöntem olarak rainbow table'lardan (gökkuşağı tabloları) zaten bahsetmiştik, peki ya işin içine bir tuz (salt) girerse?

Parola hash'lerini "deşifre" edemezsiniz (**decrypt**). Onlar şifrelenmiş değildir. Hash'leri kırmak için birçok farklı girdiyi (birçok olası parolayı kapsadığı için `rockyou.txt` gibi) hash'lemeniz, eğer varsa tuzu eklemeniz ve hedef hash ile karşılaştırmanız gerekir. Eşleşme sağlandığında, parolanın ne olduğunu öğrenmiş olursunuz. **Hashcat** ve **John the Ripper** gibi araçlar yaygın olarak bu amaçlar için kullanılır.

### GPU'lar ile Parola Kırma (Cracking Passwords with GPUs)

Modern GPU'lar (Grafik İşlem Birimleri) binlerce çekirdeğe sahiptir. Dijital görüntü işleme ve bilgisayar grafiklerini hızlandırma konusunda uzmanlaşmışlardır. Bir CPU'nun yapabildiği her işi yapamasalar da, hash fonksiyonlarında yer alan bazı matematiksel hesaplamalarda çok iyidirler. Birçok hash türünü hızlıca kırmak için bir ekran kartı kullanabilirsiniz. **Bcrypt** gibi bazı hashing algoritmaları, GPU üzerinde hashing yapmanın CPU kullanımına göre herhangi bir hız artışı sağlamayacağı şekilde tasarlanmıştır; bu, onların kırılmaya karşı dirençli olmalarına yardımcı olur.

### VM'lerde (Sanal Makineler) Kırma Yapmak?

VM'lerin (Sanal Makineler) normalde ana makinenin (host) grafik kart(lar)ına erişimi olmadığını belirtmekte fayda var. Kullandığınız sanallaştırma yazılımına bağlı olarak bunu ayarlayabilirsiniz, ancak bu zahmetlidir. Ayrıca, sanallaştırılmış bir işletim sisteminden CPU kullandığınızda performans düşüşü meydana gelir ve amacınız bir hash kırmak olduğunda her bir ekstra CPU döngüsüne ihtiyacınız vardır.

Eğer **Hashcat** çalıştırmak istiyorsanız, mevcutsa GPU'nuzdan en iyi şekilde yararlanmak için onu ana makinenizde çalıştırmak en iyisidir. Eğer MS Windows'u tercih ediyorsanız şanslısınız; web sitesinde MS Windows sürümleri mevcuttur ve bunu PowerShell üzerinden çalıştırabilirsiniz. Bir VM içinde OpenCL ile Hashcat çalıştırabilirsiniz ancak hızlar muhtemelen ana makinenizde kırmaktan daha kötü olacaktır.

**John the Ripper** varsayılan olarak CPU kullanır ve bir VM içinde doğrudan çalışır; ancak herhangi bir sanallaştırma yükünden (overhead) kaçınmak ve CPU çekirdekleriniz ile iş parçacıklarınızdan (threads) en iyi şekilde yararlanmak için onu ana işletim sisteminde çalıştırarak daha iyi hızlar elde edebilirsiniz.

---

### Hash Kırma Zamanı (Time to Crack Some Hashes)

Size hash'leri sağlayacağım. Onları kırın. Nasıl yapacağınızı seçebilirsiniz. Çevrimiçi araçları, **Hashcat** veya **John the Ripper** kullanmanız gerekecek. Aşağıdakileri çözmek için çevrimiçi rainbow table'ları kullanabilseniz de, öğrenme deneyiminizi kısıtlayacağı için bunu yapmamanızı şiddetle tavsiye ederiz. İlk üç soru için `rockyou.txt` ile birlikte `hashcat` kullanmak cevapları bulmak için yeterlidir.

**Hashcat temel olarak şu sözdizimini kullanır:** `hashcat -m <hash_type> -a <attack_mode> hashfile wordlist`

- **`-m <hash_type>`**: Hash türünü sayısal formatta belirtir. Örneğin, `-m 1000` NTLM içindir. Kullanılacak hash türü kodunu bulmak için resmi dokümantasyonu (`man hashcat`) ve [örnek sayfasını](https://hashcat.net/wiki/doku.php?id=example_hashes) kontrol edin.
    
- **`-a <attack_mode>`**: Saldırı modunu belirtir. Örneğin, `-a 0` "straight" (doğrudan) saldırı içindir, yani kelime listesindeki parolaları birbiri ardına denemek.
    
- **`hashfile`**: Kırmak istediğiniz hash'i içeren dosyadır.
    
- **`wordlist`**: Saldırınızda kullanmak istediğiniz güvenlik kelime listesidir.
    

**Örnek:** `hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt` Bu komut, hash'i **Bcrypt** olarak kabul edecek ve `rockyou.txt` dosyasındaki parolaları deneyecektir.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

**1. John the Ripper (JtR) Kullanımı:** Eğer hash tipini tam olarak bilmiyorsan, John genellikle bunu otomatik tanır. Basit bir kullanım örneği: `john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt` Eğer hash'i daha önce kırdıysan sonucu görmek için: `john --show hash.txt`

**2. Hashcat'te Cihaz Seçimi:** Eğer bilgisayarında hem işlemci hem ekran kartı varsa, hangisini kullanacağını `-D` parametresiyle seçebilirsin.

- `-D 1` -> CPU
    
- `-D 2` -> GPU
    

**3. Kurallar (Rules) Kullanımı:** Bazen parola listede olduğu gibi değil, sonunda bir sayı veya büyük harf ile bulunabilir. Hashcat'in `-r` (rules) özelliği, listedeki her kelimeye otomatik varyasyonlar ekleyerek şansını artırır: `hashcat -m 0 hash.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule`