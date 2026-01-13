## OS Detection (İşletim Sistemi Tespiti)

`-O` seçeneğini ekleyerek **OS detection** (işletim sistemi tespiti) özelliğini etkinleştirebilirsiniz. Adından da anlaşılacağı gibi bu seçenek, Nmap'in hedef işletim sistemi hakkında "eğitimli bir tahminde" bulunmak için çeşitli göstergelere dayanmasını sağlar.

Aşağıdaki örnekte Nmap, hedefin Linux 4.x veya 5.x çalıştırdığını tespit ediyor. Hedef makine aslında 5.15 sürümünü kullandığı için, Nmap'in "4.15 ile 5.8 arasında" olduğu beyanı gerçeğe oldukça yakındır. Unutulmamalıdır ki mükemmel doğrulukta bir OS dedektörü yoktur.

**AttackBox Terminal**

Bash

```
root@tryhackme:~# nmap -sS -O 192.168.124.211 Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-13 13:37 EEST
Nmap scan report for ubuntu22lts-vm (192.168.124.211)
Host is up (0.00043s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 52:54:00:54:FA:4E (QEMU virtual NIC)
Device type: general purpose
Running: Linux 4.X|5.X
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:linux:linux_kernel:5
OS details: Linux 4.15 - 5.8
Network Distance: 1 hop
```

---

## Service and Version Detection (Servis ve Versiyon Tespiti)

Birkaç açık port keşfettiniz ve bu portlarda hangi servislerin dinleme yaptığını bilmek istiyorsunuz. `-sV` seçeneği **version detection** özelliğini etkinleştirir. Bu, daha az tuş vuruşuyla hedefiniz hakkında daha fazla bilgi toplamak için oldukça kullanışlıdır. Aşağıdaki çıktı, tespit edilen SSH sunucu sürümünü gösteren "VERSION" adlı ek bir sütun sunar.

**AttackBox Terminal**

Bash

```
root@tryhackme:~# nmap -sS -sV 192.168.124.211Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-13 13:33 EEST
Nmap scan report for ubuntu22lts-vm (192.168.124.211)
Host is up (0.000046s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
```

Eğer `-O`, `-sV` ve daha fazlasını tek bir seçenekte toplamak isterseniz, bu `-A` (Aggressive scan) seçeneğidir. Bu seçenek OS tespiti, versiyon taraması ve traceroute gibi özellikleri tek seferde etkinleştirir.

---

## Forcing the Scan (Taramayı Zorlamak)

`-sS` gibi bir port taraması çalıştırdığımızda, hedef hostun **host discovery** (keşif) aşamasında yanıt vermeme ihtimali vardır (örneğin; bir host ICMP isteklerine yanıt vermiyor olabilir). Bu durumda Nmap, hostu "down" (kapalı) olarak işaretler ve port taraması yapmaz.

Nmap'ten tüm hostları "online" kabul etmesini ve keşif aşamasında yanıt vermeyenler dahil her hostu taramasını isteyebiliriz. Bu işlem `-Pn` seçeneği ile tetiklenir.

---

## Özet

| **Seçenek** | **Açıklama**                                                            |
| ----------- | ----------------------------------------------------------------------- |
| **`-O`**    | **OS detection** (İşletim sistemi tespiti)                              |
| **`-sV`**   | **Service and version detection** (Servis ve versiyon tespiti)          |
| **`-A`**    | **OS detection, version detection** ve diğer ek özellikler              |
| **`-Pn`**   | Çevrimdışı görünen hostları da tara (**host discovery** aşamasını atla) |