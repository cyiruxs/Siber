
## Gobuster: dir Modu

Gobuster, kullanıcıların web sitesi dizinlerini ve dosyalarını enumerate etmesine olanak tanıyan bir **dir** moduna sahiptir. Bu mod, bir penetrasyon testi gerçekleştirirken web sitesinin dizin yapısını ve hangi dosyaları içerdiğini görmek istediğinizde kullanışlıdır. Web sitelerinin ve web uygulamalarının dizin yapıları genellikle belirli bir konvansiyonu takip eder, bu da onları wordlist'ler kullanarak **Brute Force** işlemlerine karşı duyarlı hale getirir. Örneğin, WordPress barındıran bir web sunucusundaki dizin yapısı şuna benzer:

### AttackBox Terminal

Bash

```
root@tryhackme:~# tree -L 3 -d.
└── html
    └── wordpress
        ├── wp-admin
        ├── wp-content
        └── wp-includes
```

Gobuster güçlüdür çünkü web sitesini taramanıza ve **status codes** (durum kodları) döndürmenize olanak tanır. Bu durum kodları, dışarıdan bir kullanıcı olarak o dizini talep edip edemeyeceğinizi size anında söyler.

### Yardım (Help)

Eğer `gobuster dir` komutunun neler sunabileceğine dair eksiksiz bir genel bakış isterseniz, yardım sayfasına bakabilirsiniz. `dir` komutu için hazırlanan kapsamlı yardım sayfasını görmek biraz korkutucu olabilir. Bu nedenle, bu oda kapsamında en temel bayraklara (flags) odaklanacağız. Yardımı görüntülemek için şu komutu yazın: `gobuster dir --help`.

`gobuster dir` komutuna ince ayar yapmak için birçok bayrak kullanılır. Bunların her birinin üzerinden geçmek kapsam dışıdır, ancak aşağıdaki tabloda çoğu senaryoyu kapsayan bayrakları listeledik:

|Bayrak|Uzun Bayrak|Açıklama|
|---|---|---|
|`-c`|`--cookies`|Her istekle birlikte gönderilecek bir cookie (çerez) yapılandırır (örneğin bir session ID).|
|`-x`|`--extensions`|Taramak istediğiniz dosya uzantılarını belirtir. Örn: `.php`, `.js`|
|`-H`|`--headers`|Her istekle birlikte gönderilecek tam bir header (başlık) yapılandırır.|
|`-k`|`--no-tls-validation`|HTTPS kullanıldığında sertifikayı kontrol eden süreci atlar. CTF etkinliklerinde veya THM'deki test odalarında genellikle "self-signed" (kendinden imzalı) sertifika kullanılır; bu da **TLS** kontrolü sırasında hataya neden olur.|
|`-n`|`--no-status`|Alınan her yanıtın durum kodlarını görmek istemediğinizde bu bayrağı ayarlayabilirsiniz. Bu, ekrandaki çıktının temiz kalmasına yardımcı olur.|
|`-P`|`--password`|Kimlik doğrulamalı (authenticated) istekler yürütmek için `--username` bayrağı ile birlikte kullanılabilir. Bir kullanıcıdan kimlik bilgileri elde ettiğinizde kullanışlıdır.|
|`-s`|`--status-codes`|Alınan yanıtlardan hangi durum kodlarının görüntüleneceğini yapılandırmanıza olanak tanır (örneğin `200` veya `300-400` gibi bir aralık).|
|`-b`|`--status-codes-blacklist`|Görüntülenmesini istemediğiniz durum kodlarını yapılandırmanıza olanak tanır. Bu bayrağı kullanmak `-s` bayrağını geçersiz kılar.|
|`-U`|`--username`|Kimlik doğrulamalı istekler yürütmek için `--password` bayrağı ile birlikte kullanılabilir.|
|`-r`|`--followredirect`|Gönderilen isteğe yanıt olarak alınan yönlendirmeyi (redirect) takip etmesi için Gobuster'ı yapılandırır. Bir HTTP yönlendirme durum kodu (örn. 301 veya 302), istemciyi farklı bir URL'ye yönlendirmek için kullanılır.|

E-Tablolar'a aktar

---

## dir Modu Nasıl Kullanılır?

Gobuster'ı **dir** modunda çalıştırmak için şu komut formatını kullanın: `gobuster dir -u "http://www.example.thm" -w /path/to/wordlist`

Komutun, `dir` anahtar kelimesine ek olarak `-u` ve `-w` bayraklarını da içerdiğine dikkat edin. Gobuster dizin enumeration işleminin çalışması için bu iki bayrak zorunludur. Gobuster **dir** modu ile dizin ve dosyaların nasıl enumerate edileceğine dair pratik bir örneğe bakalım:

`gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r`

Bu komut, `directory-list-2.3-medium.txt` wordlist'ini kullanarak `www.example.thm` adresindeki tüm dizinleri tarar. Komutun her bir parçasına daha yakından bakalım:

- **gobuster dir**: Gobuster'ı dizin ve dosya enumeration modunu kullanacak şekilde yapılandırır.
    
- **-u [http://www.example.thm](https://www.google.com/search?q=http://www.example.thm)**:
    
    - URL, Gobuster'ın aramaya başladığı temel yol (base path) olacaktır. Yukarıdaki URL, kök (root) web dizinini kullanmaktadır. Örneğin, Linux üzerindeki tipik bir Apache kurulumunda bu `/var/www/html` dizinidir. Eğer bir "resources" dizininiz varsa ve o dizini enumerate etmek istiyorsanız, URL'yi `http://www.example.thm/resources` olarak ayarlarsınız. Bunu `http://www.example.thm/yol/klasor` şeklinde de düşünebilirsiniz.
        
    - URL, kullanılan protokolü (bu durumda **HTTP**) içermelidir. Bu önemli ve zorunludur. Yanlış protokol girerseniz tarama başarısız olur.
        
    - URL'nin host kısmına IP veya **HOSTNAME** yazabilirsiniz. Ancak, IP kullanırken amaçlanandan farklı bir web sitesini hedefleyebileceğinizi belirtmek önemlidir. Bir web sunucusu, tek bir IP kullanarak birden fazla web sitesi barındırabilir (bu tekniğe **virtual hosting** denir). Emin olmak için HOSTNAME kullanın.
        
    - Gobuster **recursively** (özyinelemeli) olarak enumerate etmez. Bu nedenle, sonuçlar ilgilendiğiniz bir dizin yolunu gösteriyorsa, o özel dizini ayrıca enumerate etmeniz gerekecektir.
        
- **-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt**: Gobuster'ı enumerate işlemi için bu wordlist'i kullanacak şekilde yapılandırır. Wordlist'teki her bir girdi, yapılandırılan URL'nin sonuna eklenir.
    
- **-r**: Gobuster'ı, gönderilen isteklerden alınan yönlendirme (redirect) yanıtlarını takip edecek şekilde yapılandırır. Eğer bir 301 durum kodu alınırsa, Gobuster yanıtta yer alan yönlendirme URL'sine gidecektir.
    

Dosya türlerini belirtmek için `-x` bayrağını kullandığımız ikinci bir örneğe bakalım:

`gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .php,.js`

Bu komut, `directory-list-2.3-medium.txt` wordlist'ini kullanarak `http://example.thm` adresindeki dizinleri arayacaktır. Dizin listelemeye ek olarak, bu komut `.php` veya `.js` uzantısına sahip tüm dosyaları da listeleyecektir.