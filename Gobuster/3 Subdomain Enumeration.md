Odaklanacağımız bir sonraki mod **dns** modudur. Bu mod, Gobuster'ın alt alan adlarını (**subdomains**) brute force yöntemiyle bulmasına olanak tanır. Bir penetrasyon testi sırasında, hedefinizin ana alan adına (top domain) bağlı alt alan adlarını kontrol etmek esastır. Bir açığın ana alan adında yamalanmış (patched) olması, alt alan adında da yamalandığı anlamına gelmez. Bu alt alan adlarından birinde bir güvenlik açığını sömürme (exploit) fırsatı mevcut olabilir. Örneğin, TryHackMe hem `tryhackme.thm` hem de `mobile.tryhackme.thm` adreslerine sahipse, `mobile.tryhackme.thm` üzerinde `tryhackme.thm`’de bulunmayan bir zafiyet olabilir. İşte bu yüzden alt alan adlarını da aramak oldukça önemlidir!

### Yardım (Help)

Eğer `gobuster dns` komutunun neler sunabileceğine dair eksiksiz bir genel bakış isterseniz, yardım sayfasına bakabilirsiniz. `dns` komutu için hazırlanan kapsamlı yardım sayfasını görmek biraz korkutucu olabilir. Bu nedenle, bu oda kapsamında en önemli bayraklara (flags) odaklanacağız. Yardımı görüntülemek için şu komutu yazın: `gobuster dns --help`

**dns** modu, **dir** moduna göre daha az bayrak sunar. Ancak bunlar, çoğu DNS subdomain enumeration senaryosunu kapsamak için fazlasıyla yeterlidir. Yaygın olarak kullanılan bazı bayraklara göz atalım:

|**Bayrak**|**Uzun Bayrak**|**Açıklama**|
|---|---|---|
|`-c`|`--show-cname`|CNAME Kayıtlarını gösterir (`-i` bayrağı ile birlikte kullanılamaz).|
|`-i`|`--show-ips`|Bu bayrağın eklenmesi, alan adının ve alt alan adlarının çözümlendiği (resolve) IP adreslerini gösterir.|
|`-r`|`--resolver`|Çözümleme işlemi için kullanılacak özel bir DNS sunucusu yapılandırır.|
|`-d`|`--domain`|Enumerate etmek istediğiniz alan adını (domain) yapılandırır.|

---

## dns Modu Nasıl Kullanılır?

Gobuster'ı dns modunda çalıştırmak için şu komut sözdizimini (syntax) kullanın:

`gobuster dns -d example.thm -w /path/to/wordlist`

Komutun, `dns` anahtar kelimesine ek olarak `-d` ve `-w` bayraklarını da içerdiğine dikkat edin. Gobuster alt alan adı enumeration işleminin çalışması için bu iki bayrak zorunludur. Gobuster **dns** modu ile alt alan adlarının nasıl enumerate edileceğine dair bir örneğe bakalım:

`gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`

- **gobuster dns**: Yapılandırılan alan adı üzerindeki alt alan adlarını (subdomains) enumerate eder.
    
- **-d example.thm**: Hedefi `example.thm` alan adı olarak belirler.
    
- **-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt**: Wordlist'i `subdomains-top1million-5000.txt` olarak ayarlar. Gobuster bu listedeki her bir girdiyi kullanarak yeni bir **DNS** sorgusu oluşturur. Eğer listenin ilk girdisi 'all' ise, sorgu `all.example.thm` şeklinde olacaktır.
    

Komutu kendiniz girdiğinizde aşağıdaki gibi bir çıktı almalısınız:

### AttackBox Terminal

Bash

```
root@tryhackme:~# gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Domain:     example.thm
[+] Threads:    10
[+] Timeout:    1s
[+] Wordlist:   /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
===============================================================
Starting gobuster in DNS enumeration mode
===============================================================
Found: www.example.thm
                                                                                                                                                            
Found: shop.example.thm
                                                                                                                                                            
Found: academy.example.thm
                                                                                                                                                            
Found: primary.example.thm
                                                                                                                                                            
Progress: 4989 / 4990 (99.98%)
===============================================================
Finished
===============================================================
```