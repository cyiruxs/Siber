Odaklanacağımız son mod **vhost** modudur. Bu mod, Gobuster'ın sanal host'ları (**virtual hosts**) brute force yöntemiyle bulmasına olanak tanır. Sanal host'lar, aynı makine üzerindeki farklı web siteleridir. Bazen alt alan adlarına (subdomains) benzerler, ancak aldanmayın! Sanal host'lar IP tabanlıdır ve aynı sunucu üzerinde çalışırlar; alt alan adları ise DNS üzerinde yapılandırılır. **vhost** ve **dns** modu arasındaki fark, Gobuster'ın tarama yapma şeklindedir:

- **vhost modu:** Yapılandırılan HOSTNAME (`-u` bayrağı) ile bir wordlist girdisini birleştirerek oluşturulan URL'ye gider.
    
- **dns modu:** Yapılandırılan alan adı (`-d` bayrağı) ile bir wordlist girdisini birleştirerek oluşturulan FQDN (Tam Nitelenmiş Alan Adı) için bir **DNS lookup** (sorgusu) yapar.
    

### Yardım (Help)

Eğer `gobuster vhost` komutunun neler sunabileceğine dair eksiksiz bir genel bakış isterseniz, yardım sayfasına bakabilirsiniz. `vhost` komutu için hazırlanan kapsamlı yardım sayfasını görmek biraz korkutucu olabilir. Bu nedenle, bu oda kapsamında en önemli bayraklara (flags) odaklanacağız. Yardımı görüntülemek için şu komutu yazın: `gobuster vhost --help`

**vhost** modu, **dir** moduna benzer bayraklar sunar. Yaygın olarak kullanılan bazı bayraklara göz atalım:

| Kısa Bayrak | Uzun Bayrak         | Açıklama                                                                                                                         |
| ----------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `-u`        | `--url`             | Virtual hostname'leri brute force etmek için temel URL'yi (hedef domain) belirtir.                                               |
|             | `--append-domain`   | Wordlist'teki her kelimenin sonuna temel alan adını ekler (örn. `word.example.com`).                                             |
| `-m`        | `--method`          | İstekler için kullanılacak HTTP metodunu belirtir (örn. GET, POST).                                                              |
|             | `--domain`          | Geçerli bir hostname oluşturmak için her wordlist girdisine bir alan adı ekler (açıkça belirtilmediği durumlarda kullanışlıdır). |
|             | `--exclude-length`  | Yanıt gövdesinin (body) uzunluğuna göre sonuçları hariç tutar (istenmeyen yanıtları filtrelemek için kullanışlıdır).             |
| `-r`        | `--follow-redirect` | HTTP yönlendirmelerini (redirect) takip eder (alt alan adlarının yönlendirme yaptığı durumlar için kullanışlıdır).               |
|             |                     |                                                                                                                                  |


---

## vhost Modu Nasıl Kullanılır?

Gobuster'ı **vhost** modunda çalıştırmak için şu komutu yazın: `gobuster vhost -u "http://example.thm" -w /path/to/wordlist`

Komutun, `vhost` anahtar kelimesine ek olarak `-u` ve `-w` bayraklarını da içerdiğine dikkat edin. Gobuster vhost enumeration işleminin çalışması için bu iki bayrak zorunludur. Gobuster **vhost** modu ile sanal host'ların nasıl enumerate edileceğine dair pratik bir örneğe bakalım:

### AttackBox Terminal

Bash

```
root@tryhackme:~# gobuster vhost -u "http://10.112.164.24" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:              http://10.10.94.214
[+] Method:           GET
[+] Threads:          10
[+] Wordlist:         /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
[+] User Agent:       gobuster/3.6
[+] Timeout:          10s
[+] Append Domain:    true
[+] Exclude Length:   250,254,263,274,283,293,294,299,253,261,269,277,285,290,300,257,258,270,278,282,291,252,260,264,268,271,279,280,289,251,256,262,265,272,297,287,292,295,255,266,276,284,286,296,267,273,275,281,288,259,298
===============================================================
Starting gobuster in VHOST enumeration mode
===============================================================
Found: blog.example.thm Status: 200 [Size: 1493]
Found: shop.example.thm Status: 200 [Size: 2983]
Found: www.example.thm Status: 200 [Size: 84352]
Found: chelyabinsk-rnoc-rr02.backbone.example.thm Status: 404 [Size: 304]
Found: academy.example.thm Status: 200 [Size: 434]
Progress: 4989 / 4990 (99.98%)
===============================================================
Finished
===============================================================
```

Bu komutun temel komut sözdiziminden çok daha karmaşık olduğunu fark edeceksiniz. Çok daha fazla yapılandırılmış bayrak içerir. Gerçekçi testlerde, test edilecek alan adının altyapısının nasıl kurulduğuna bağlı olarak durum genellikle böyledir. Bizim durumumuzda, tam olarak kurulmuş bir **DNS** altyapımız yok. Bu da `--domain` ve `--append-domain` gibi ekstra bayraklar vermemizi gerektiriyor. Bu bayrakların nasıl çalıştığını daha iyi anlamak için Gobuster'ın gönderdiği web isteklerine bakmamız gerekir. Aşağıda, `www.example.thm` adresine gönderilen temel bir GET isteği görebilirsiniz:

HTTP

```
GET / HTTP/1.1
Host: www.example.thm
User-Agent: gobuster/3.6
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

Gobuster, her seferinde isteğin `Host:` kısmını değiştirerek birden fazla istek gönderecektir. Bu örnekteki `Host:` değeri `www.example.thm`'dir. Bunu üç parçaya ayırabiliriz:

1. **www:** Bu alt alan adıdır. Gobuster'ın yapılandırılan wordlist'teki her bir girdiyle dolduracağı kısımdır.
    
2. **.example:** Bu ikinci düzey alan adıdır (second-level domain). Bunu `--domain` bayrağı ile yapılandırabilirsiniz (üst düzey alan adı ile birlikte yapılandırılması gerekir).
    
3. **.thm:** Bu üst düzey alan adıdır (top-level domain). Bunu `--domain` bayrağı ile yapılandırabilirsiniz.
    

---

### Komutun Detaylı İncelemesi

Gobuster'ın isteği nasıl gönderdiğini öğrendiğimize göre, komutu parçalarına ayıralım ve her bayrağı daha yakından inceleyelim:

- **gobuster vhost:** Gobuster'a sanal host'ları enumerate etmesi talimatını verir.
    
- **-u "[http://10.112.164.24](http://10.112.164.24)"**: Gidilecek URL'yi 10.112.164.24 olarak ayarlar.
    
- **-w /usr/share/wordlists/...**: Gobuster'ı belirtilen wordlist'i kullanacak şekilde yapılandırır. Gobuster, wordlist'teki her bir girdiyi yapılandırılan alan adının başına ekler. Eğer `--domain` bayrağı ile açıkça bir alan adı yapılandırılmamışsa, Gobuster bunu URL'den çıkaracaktır (Eğ. `test.example.thm`, `help.example.thm` vb.). Herhangi bir sanal host bulunursa, Gobuster bunları terminalde raporlayacaktır.
    
- **--domain example.thm**: İsteğin `Hostname:` kısmındaki üst ve ikinci düzey alan adlarını `example.thm` olarak ayarlar.
    
- **--append-domain**: Yapılandırılan alan adını wordlist'teki her girdinin sonuna ekler. Bu bayrak yapılandırılmazsa, ayarlanan hostname sadece `www`, `blog` vb. şeklinde kalır. Bu durum komutun yanlış çalışmasına ve hatalı pozitif (**false positives**) sonuçlar görüntülenmesine neden olur.
    
- **--exclude-length**: Gönderilen web isteklerinden aldığımız yanıtları filtreler. Bu bayrakla hatalı pozitifleri (false positives) temizleyebiliriz. Komutu bu bayrak olmadan çalıştırırsanız, "Found: Orion.example.thm Status: 404 [Size: 279]" gibi birçok hatalı sonuç aldığınızı fark edeceksiniz. Bu hatalı pozitifler tipik olarak benzer bir yanıt boyutuna sahiptir, bu nedenle bunu çoğu hatalı sonucu filtrelemek için kullanabiliriz. Gerçek bir pozitif sonuç (true positive) elde etmek için `200 OK` yanıtı almayı bekleriz (ancak istisnalar mevcuttur, bu odanın kapsamı dışındadır).