>**Gobuster**, Golang diliyle yazılmış, açık kaynaklı bir ofansif güvenlik aracıdır. Belirli wordlist'ler (kelime listeleri) kullanarak ve gelen yanıtları işleyerek; web dizinlerini, **DNS** alt alan adlarını (subdomains), vhost'ları, Amazon **S3** bucket'larını ve Google Cloud Storage alanlarını **brute force** (kaba kuvvet) yöntemiyle enumerate eder. Birçok güvenlik profesyoneli bu aracı penetrasyon testleri, bug bounty avcılığı ve siber güvenlik değerlendirmeleri için kullanır. Etik hackleme aşamalarına baktığımızda, Gobuster'ı **reconnaissance** (keşif) ve **scanning** (tarama) aşamaları arasında konumlandırabiliriz.

Gobuster'ı keşfetmeden önce, **enumeration** ve **Brute Force** kavramlarını kısaca ele alalım.

### Enumeration (Numaralandırma/Listeleme)

Enumeration, erişilebilir olsun ya da olmasın, mevcut tüm kaynakları listeleme eylemidir. Örneğin, Gobuster web dizinlerini enumerate eder.

### Brute Force (Kaba Kuvvet)

Brute force, bir eşleşme bulunana kadar her ihtimali deneme eylemidir. Bu, elinizde on tane anahtar olması ve uygun olanı bulana kadar her birini kilit üzerinde denemenize benzer. Gobuster bu amaçla **wordlist**'leri kullanır.

---

## Gobuster: Genel Bakış

Gobuster; Kali Linux gibi dağıtımlarda varsayılan olarak yüklü gelir. Gobuster'ın yardım sayfasına bakarak işlevlerine ve seçeneklerine genel bir göz atalım.

Aşağıdaki komutu girin: `gobuster --help`. Aşağıda gösterildiği gibi Gobuster aracının yardım sayfasını almalısınız:

### AttackBox Terminal

Yardım sayfası birden fazla bölüm içerir:

- **Usage (Kullanım):** Komutun nasıl kullanılacağına dair sözdizimini (syntax) gösterir.
    
- **Available Commands (Mevcut Komutlar):** Dizinleri, dosyaları, **DNS** alt alan adlarını, Google Cloud Storage bucket'larını ve Amazon **AWS S3** bucket'larını enumerate etmemize yardımcı olacak birden fazla komut mevcuttur. Bu doküman boyunca `dir`, `dns` ve `vhost` komutlarına odaklanacağız.
    
- **Flags (Bayraklar/Parametreler):** Bunlar, komutlarımızı özelleştirmek için yapılandırabileceğimiz belirli seçeneklerdir. Sıkça kullanacağımız bayraklara göz atalım:
    

---

### Örnek Kullanım

Bir web dizinini enumerate etmek için bu komutları ve bayrakları bir arada nasıl kullanacağımıza dair bir örneğe bakalım:

`gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64`

- `gobuster dir`: Dizin ve dosya enumeration modunu kullanacağımızı belirtir.
    
- `-u "http://www.example.thm/"`: Gobuster'a hedef URL'nin `http://example.thm/` olduğunu söyler.
    
- `-w /usr/share/wordlists/dirb/small.txt`: Gobuster'ı, web dizinlerini brute force etmek için `small.txt` wordlist'ini kullanmaya yönlendirir. Gobuster, wordlist'teki her bir girdiyi kullanarak yeni bir URL oluşturacak ve bu URL'ye bir GET isteği gönderecektir. Eğer wordlist'in ilk girdisi `images` olsaydı, Gobuster `http://example.thm/images/` adresine bir GET isteği gönderecekti.
    
- `-t 64`: Gobuster'ın kullanacağı thread sayısını 64'e ayarlar. Bu, performansı ciddi şekilde artırır.