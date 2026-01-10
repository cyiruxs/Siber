
## Who is online? (Kimler çevrimiçi?)

Bu görev, canlı hostları keşfetmek için **Nmap**'in nasıl kullanılacağını bulmayı amaçlamaktadır. **Nmap**, canlı hostları keşfetmek için çeşitli gelişmiş yöntemler kullanır.

Başlamadan önce, **Nmap**'in hedeflerini belirtmek için birden fazla yol kullandığını belirtmeliyiz:

- **`-` kullanarak IP aralığı:** 192.168.0.1'den 192.168.0.10'a kadar olan tüm IP adreslerini taramak istiyorsanız, `192.168.0.1-10` yazabilirsiniz.
    
- **`/` kullanarak IP alt ağı (subnet):** Eğer bir subnet taramak istiyorsanız, bunu `192.168.0.1/24` olarak ifade edebilirsiniz; bu, `192.168.0.0-255` aralığına eşdeğerdir.
    
- **Hostname:** Hedefinizi hostname (ana bilgisayar adı) ile de belirtebilirsiniz, örneğin: `example.thm`.
    

Diyelim ki bir ağdaki çevrimiçi hostları keşfetmek istiyorsunuz. **Nmap**, `-sn` seçeneğini, yani **ping scan** özelliğini sunar. Ancak bunun `ping` gibi sınırlı olmasını beklemeyin. Şimdi bunu iş başında görelim.

Başlamadan önce şunu not etmeliyiz: Bu oda boyunca `nmap` komutunu ya **root** olarak çalıştırıyoruz ya da `sudo` kullanıyoruz; çünkü hesap ayrıcalıklarımızla Nmap’in yeteneklerini kısıtlamak istemiyoruz. Nmap'i yerel (non-root) bir kullanıcı olarak çalıştırmak bizi **ICMP echo** ve **TCP connect scan** gibi temel tarama türleriyle sınırlandıracaktır; buna bu odanın sonunda tekrar değineceğiz.

### Scanning a “Local” Network (Yerel Bir Ağı Taramak)

Bu bağlamda, "yerel" terimini Ethernet veya WiFi gibi doğrudan bağlı olduğumuz ağı ifade etmek için kullanıyoruz. İlk gösterimde, bağlı olduğumuz WiFi ağını tarayacağız. IP adresimiz `192.168.66.89` ve `192.168.66.0/24` ağını tarıyoruz. `nmap -sn 192.168.66.0/24` komutu ve çıktısı aşağıdaki terminalde gösterilmiştir.

**AttackBox Terminal**

Bash

```
root@tryhackme:~# nmap -sn 192.168.66.0/24
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-07 13:49 EEST
Nmap scan report for XiaoQiang (192.168.66.1)
Host is up (0.0069s latency).
MAC Address: 44:DF:65:D8:FE:6C (Unknown)
Nmap scan report for S190023240007 (192.168.66.88)
Host is up (0.090s latency).
MAC Address: 7C:DF:A1:D3:8C:5C (Espressif)
Nmap scan report for wlan0 (192.168.66.97)
Host is up (0.20s latency).
MAC Address: 10:D5:61:E2:18:E6 (Tuya Smart)
Nmap scan report for 192.168.66.179
Host is up (0.10s latency).
MAC Address: E4:AA:EC:8F:88:C9 (Tianjin Hualai Technology)
[...]
Nmap done: 256 IP addresses (7 hosts up) scanned in 2.64 seconds
```

Doğrudan bağlı bir ağı taradığımız için (Ethernet veya WiFi üzerinden), cihazların **MAC addresses** (MAC adreslerini) görebiliriz. Sonuç olarak, ağ kartı satıcılarını (vendors) öğrenebiliriz; bu, hedef cihazın türünü tahmin etmemize yardımcı olabilecek faydalı bir bilgidir.

Doğrudan bağlı bir ağ taranırken, **Nmap** işe **ARP requests** göndererek başlar. Bir cihaz **ARP request**'e yanıt verdiğinde, **Nmap** onu "**Host is up**" olarak etiketler.

### Scanning a “Remote” Network (Uzak Bir Ağı Taramak)

"Uzak" bir ağ durumunu düşünün. Bu bağlamda "uzak", sistemimiz ile bu ağ arasında en az bir yönlendiricinin (**router**) bulunduğu anlamına gelir. Sonuç olarak, hedef sistemlere giden tüm trafiğimiz bir veya daha fazla router üzerinden geçmelidir. Yerel bir ağı taramanın aksine, hedefe bir **ARP request** gönderemeyiz.

Sistemimiz `192.168.66.89` IP adresine sahip ve `192.168.66.0/24` ağına ait. Aşağıdaki terminalde, yerel sistemimiz ile hedef hostlar arasında iki veya daha fazla router (hop) bulunan `192.168.11.0/24` hedef ağını tarıyoruz.

**AttackBox Terminal**

Bash

```
root@tryhackme:~# nmap -sn 192.168.11.0/24
Starting Nmap 7.92 ( https://nmap.org ) at 2024-08-07 14:05 EEST
Nmap scan report for 192.168.11.1
Host is up (0.018s latency).
Nmap scan report for 192.168.11.151
Host is up (0.0013s latency).
Nmap scan report for 192.168.11.152
Host is up (0.13s latency).
Nmap scan report for 192.168.11.154
Host is up (0.22s latency).
Nmap scan report for 192.168.11.155
Host is up (2.3s latency).
Nmap done: 256 IP addresses (5 hosts up) scanned in 10.67 seconds
```

**Nmap** çıktısı beş hostun ayakta olduğunu gösteriyor. Peki Nmap bunu nasıl keşfetti? Daha fazlasını öğrenmek için **Nmap** tarafından oluşturulan örnek trafiğe bakalım. Trafikte iki hosttan gelen yanıtları görebiliriz:

- `192.168.11.1` canlıdır ve **ICMP echo (ping)** isteğine yanıt vermiştir.
    
- `192.168.11.2` kapalı görünmektedir. Nmap iki **ICMP echo (ping)** isteği, iki **ICMP timestamp** isteği, port 443'e **SYN** bayrağı set edilmiş iki **TCP** paketi ve port 80'e **ACK** bayrağı set edilmiş iki **TCP** paketi göndermiştir. Hedef hiçbirine yanıt vermemiştir. `192.168.11.151` router'ından birkaç **ICMP destination unreachable** paketi gözlemliyoruz.
    

Şunu belirtmekte fayda var: Nmap'in canlı hostları nasıl keşfedeceği üzerinde, verilen portlar üzerinden **TCP SYN**, **TCP ACK** ve **UDP** keşfi için `-PS[portlist]`, `-PA[portlist]`, `-PU[portlist]` gibi seçeneklerle daha fazla kontrole sahip olabiliriz. Ancak bu, bu odanın kapsamı dışındadır.

Son bir nokta olarak, Nmap `-sL` seçeneği ile bir **list scan** sunar. Bu tarama, hedefleri gerçekten taramadan sadece listeler. Örneğin, `nmap -sL 192.168.0.1/24` komutu, taranacak olan 256 hedefi listeleyecektir. Bu seçenek, gerçek taramayı çalıştırmadan önce hedefleri onaylamaya yardımcı olur.

Daha önce belirttiğimiz gibi, `-sn` seçeneği, üzerinde çalışan servisleri keşfetmeye çalışmadan canlı hostları bulmayı amaçlar. Bu tarama, çok fazla gürültü (noise) çıkarmadan bir ağdaki cihazları keşfetmek istiyorsanız yararlı olabilir. Ancak bu, bize hangi servislerin çalıştığını söylemez. Canlı hostlarda çalışan ağ servisleri hakkında daha fazla bilgi edinmek istiyorsak, bir sonraki görevde inceleyeceğimiz daha "gürültülü" bir tarama türüne ihtiyacımız var.