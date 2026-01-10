
Bu görevde, daha önce `-sn` ile bulduğumuz canlı hostlar üzerinde hangi ağ servislerinin çalıştığını keşfetmeyi öğreneceğiz. "Ağ servisi" dediğimizde, bir TCP veya UDP portu üzerinden gelen bağlantıları dinleyen süreçleri kastediyoruz (örneğin; web sunucuları TCP 80/443, DNS sunucuları UDP 53 gibi).

TCP ve UDP protokollerinin her biri tasarım gereği 65.535 porta sahiptir. Hangi portların bir servise bağlı olduğunu nasıl belirleyebileceğimizi aşağıda inceleyelim.

---

### Scanning TCP Ports (TCP Portlarını Taramak)

Bir TCP portunun açık olup olmadığını anlamanın en temel yolu, o porta `telnet` ile bağlanmaya çalışmaktır. Bu, her hedef portla bir **TCP three-way handshake** (üçlü el sıkışma) tamamlamaya çalışmak anlamına gelir. Sadece açık portlar uygun yanıtı verecektir.

#### Connect Scan (`-sT`)

Connect scan, `-sT` seçeneği ile tetiklenir. Her hedef TCP portu ile üçlü el sıkışmayı tamamlamaya çalışır. Eğer port açıksa ve Nmap başarıyla bağlanırsa, Nmap bağlantıyı hemen sonlandırır.

- **Açık Port:** Üçlü el sıkışma tamamlanır, ardından Nmap bir **TCP RST-ACK** paketi ile bağlantıyı koparır.
    
- **Kapalı Port:** Hedef sistem doğrudan bir **TCP RST-ACK** paketi ile yanıt vererek bağlantı isteğini reddeder.
    

#### SYN Scan (Stealth / Gizli Tarama) (`-sS`)

`-sS` bayrağı ile seçilen bu yöntem, üçlü el sıkışmayı tamamlamak yerine sadece ilk adımı gerçekleştirir: Bir **TCP SYN** paketi gönderir.

- **Avantajı:** Bağlantı hiçbir zaman tam olarak kurulmadığı için uygulama günlüklerinde (logs) daha az iz bırakır; bu yüzden "stealth" (gizli) tarama olarak kabul edilir.
    
- **İşleyiş:** Dinleyen bir servis **TCP SYN-ACK** ile yanıt verdiğinde, Nmap el sıkışmayı tamamlamak yerine bir **TCP RST** paketi göndererek süreci yarıda keser. Kapalı portlarda ise süreç connect scan ile aynıdır.
    

---

### Scanning UDP Ports (UDP Portlarını Taramak) (`-sU`)

DNS, DHCP, NTP ve VoIP gibi birçok önemli servis UDP kullanır. UDP bağlantı kurma veya sonlandırma gerektirmez, bu da onu gerçek zamanlı iletişim için uygun kılar.

- Nmap, UDP servislerini taramak için `-sU` seçeneğini sunar.
    
- UDP, TCP'den daha basit olduğu için trafik farklılık gösterir. Nmap kapalı bir UDP portuna paket gönderdiğinde, genellikle hedef sistemden çeşitli **ICMP destination unreachable** (port unreachable) yanıtları gelir.
    

---

### Limiting the Target Ports (Hedef Portları Sınırlama)

Nmap varsayılan olarak en yaygın 1.000 portu tarar. Ancak bu her zaman yeterli veya verimli olmayabilir:

- **`-F` (Fast mode):** Varsayılan 1.000 port yerine en yaygın 100 portu tarar.
    
- **`-p[range]`:** Belirli bir port aralığını taramanıza olanak tanır.
    
    - Örn: `-p10-1024` (10 ile 1024 arası).
        
    - Örn: `-p-25` (1 ile 25 arası).
        
    - Örn: `-p-` (1'den 65535'e kadar **tüm portları** tarar; en kapsamlı seçenek budur).
        

---

### Özet Tablo

|**Seçenek**|**Açıklama**|
|---|---|
|**`-sT`**|**TCP connect scan** – Üçlü el sıkışmayı tamamlar.|
|**`-sS`**|**TCP SYN** – Üçlü el sıkışmanın sadece ilk adımını atar (gizli).|
|**`-sU`**|**UDP scan** – UDP servislerini tarar.|
|**`-F`**|**Fast mode** – En yaygın 100 portu tarar.|
|**`-p[range]`**|Belirli port numaralarını belirtir (`-p-` tüm portları tarar).|
