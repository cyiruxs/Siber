

# Port Tarama (Port Scanning)

Metasploit, hedef sistem ve ağ üzerindeki açık portları taramak için bir dizi modüle sahiptir. Kullanılabilir potansiyel port tarama modüllerini `search portscan` komutunu kullanarak listeleyebilirsiniz.

### Port Tarama Araması

Bash

```
msf6 > search portscan

Matching Modules
================

   #  Name                                              Disclosure Date  Rank    Check  Description
   -  ----                                              ---------------  ----    -----  -----------
   0  auxiliary/scanner/http/wordpress_pingback_access                   normal  No     Wordpress Pingback Locator
   1  auxiliary/scanner/natpmp/natpmp_portscan                           normal  No     NAT-PMP External Port Scanner
   2  auxiliary/scanner/portscan/ack                                     normal  No     TCP ACK Firewall Scanner
   3  auxiliary/scanner/portscan/ftpbounce                               normal  No     FTP Bounce Port Scanner
   4  auxiliary/scanner/portscan/syn                                     normal  No     TCP SYN Port Scanner
   5  auxiliary/scanner/portscan/tcp                                     normal  No     TCP Port Scanner
   6  auxiliary/scanner/portscan/xmas                                    normal  No     TCP "XMas" Port Scanner
   7  auxiliary/scanner/sap/sap_router_portscanner                       normal  No     SAPRouter Port Scanner
```

Bir modül ile ismiyle veya indeksiyle etkileşime geçebilirsiniz; örneğin `use 7` veya `use auxiliary/scanner/sap/sap_router_portscanner` kullanabilirsiniz.

Bash

```
msf6 >
```

Port tarama modülleri, birkaç seçeneği (options) ayarlamanızı gerektirecektir:

### Portscan Seçenekleri

Bash

```
msf6 auxiliary(scanner/portscan/tcp) > show options

Module options (auxiliary/scanner/portscan/tcp):

   Name         Current Setting  Required  Description
   ----         ---------------  --------  -----------
   CONCURRENCY  10               yes       The number of concurrent ports to check per host
   DELAY        0                yes       The delay between connections, per thread, in milliseconds
   JITTER       0                yes       The delay jitter factor (maximum value by which to +/- DELAY) in milliseconds.
   PORTS        1-10000          yes       Ports to scan (e.g. 22-25,80,110-900)
   RHOSTS                        yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'
   THREADS      1                yes       The number of concurrent threads (max one per host)
   TIMEOUT      1000             yes       The socket connect timeout in milliseconds

msf6 auxiliary(scanner/portscan/tcp) >
```

- **CONCURRENCY:** Aynı anda taranacak hedef sayısı.
    
- **PORTS:** Taranacak port aralığı. Lütfen burada `1-1000` kullanmanın varsayılan konfigürasyondaki Nmap ile aynı olmadığını unutmayın. Nmap en çok kullanılan 1000 portu tararken, Metasploit 1'den 10000'e kadar olan port numaralarını tarayacaktır.
    
- **RHOSTS:** Taranacak hedef veya hedef ağ.
    
- **THREADS:** Aynı anda kullanılacak thread (iş parçacığı) sayısı. Daha fazla thread, daha hızlı tarama sağlar.
    

Aşağıda gösterildiği gibi, msfconsole isteminden doğrudan Nmap taramalarını daha hızlı gerçekleştirebilirsiniz:

### Msfconsole İsteminden Nmap Kullanımı

Bash

```
msf6 > nmap -sS 10.10.12.229
[*] exec: nmap -sS 10.10.12.229

Starting Nmap 7.60 ( https://nmap.org ) at 2021-08-20 03:54 BST
Nmap scan report for ip-10-10-12-229.eu-west-1.compute.internal (10.10.12.229)
Host is up (0.0011s latency).
Not shown: 992 closed ports
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49158/tcp open  unknown
MAC Address: 02:CE:59:27:C8:E3 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 64.19 seconds
msf6 >
```

Bilgi toplama aşamasında, eğer çalışmanız port tarama konusunda daha hızlı bir yaklaşım gerektiriyorsa, Metasploit ilk tercihiniz olmayabilir. Ancak, bir dizi modül Metasploit'i tarama aşaması için kullanışlı bir araç haline getirir.

### UDP Servis Tanımlama (UDP Service Identification)

`scanner/discovery/udp_sweep` modülü, UDP (User Datagram Protocol) üzerinden çalışan servisleri hızlıca tanımlamanıza olanak tanır. Aşağıda görebileceğiniz gibi, bu modül tüm olası UDP servislerinin kapsamlı bir taramasını yapmaz, ancak DNS veya NetBIOS gibi servisleri tanımlamak için hızlı bir yol sunar.

### UDP Taraması

Bash

```
msf6 auxiliary(scanner/discovery/udp_sweep) > run

[*] Sending 13 probes to 10.10.12.229->10.10.12.229 (1 hosts)
[*] Discovered NetBIOS on 10.10.12.229:137 (JON-PC::U :WORKGROUP::G :JON-PC::U :WORKGROUP::G :WORKGROUP::U :__MSBROWSE__::G :02:ce:59:27:c8:e3)
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/discovery/udp_sweep) >
```

### SMB Taramaları

Metasploit, belirli servisleri taramamıza izin veren birkaç kullanışlı yardımcı (auxiliary) modül sunar. Aşağıda SMB için bir örnek verilmiştir. Özellikle bir kurumsal ağda `smb_enumshares` ve `smb_version` oldukça kullanışlı olacaktır; ancak lütfen sisteminizde yüklü olan Metasploit sürümünün sunduğu tarayıcıları tanımlamak için zaman ayırın.

### SMB Taraması

Bash

```
msf6 auxiliary(scanner/smb/smb_version) > run

[+] 10.10.12.229:445      - Host is running Windows 7 Professional SP1 (build:7601) (name:JON-PC) (workgroup:WORKGROUP ) (signatures:optional)
[*] 10.10.12.229:445      - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf6 auxiliary(scanner/smb/smb_version) >
```

Servis taramaları yaparken, **NetBIOS** gibi daha "egzotik" servisleri atlamamak önemlidir. NetBIOS (Network Basic Input Output System), SMB'ye benzer şekilde, bilgisayarların dosya paylaşmak veya yazıcılara dosya göndermek için ağ üzerinden iletişim kurmasına olanak tanır. Hedef sistemin NetBIOS adı, rolü ve hatta önemi hakkında size bir fikir verebilir (örneğin: CORP-DC, DEVOPS, SALES vb.). Ayrıca, parolasız veya basit bir parola ile (örneğin: admin, administrator, root, toor vb.) erişilebilen bazı paylaşılan dosya ve klasörlere de rastlayabilirsiniz.

Unutmayın, Metasploit hedef sistemi daha iyi anlamanıza ve muhtemelen zafiyetler bulmanıza yardımcı olabilecek birçok modüle sahiptir. Hedef sisteminize bağlı olarak yardımcı olabilecek herhangi bir modül olup olmadığını görmek için hızlı bir arama yapmaya her zaman değer.

---

## 💡 Ek Bilgiler ve Siber Güvenlik İpuçları

### Port Tarama Teknikleri Karşılaştırması

Aşağıdaki tablo, Metasploit içinde sıkça kullanılan tarama türlerinin farklarını özetler:

|**Tarama Türü**|**Metasploit Modülü**|**Açıklama**|
|---|---|---|
|**TCP Connect**|`portscan/tcp`|Tam bir 3'lü el sıkışma (3-way handshake) gerçekleştirir. Loglarda görünür.|
|**SYN Scan**|`portscan/syn`|Bağlantıyı tamamlamaz (yarım açık). Daha gizlidir ve "stealth" olarak bilinir.|
|**ACK Scan**|`portscan/ack`|Portun açık olup olmadığını değil, güvenlik duvarı (firewall) kurallarını tespit etmek için kullanılır.|
|**XMas Scan**|`portscan/xmas`|PSH, URG ve FIN bayraklarını set eder. Bazı IDS sistemlerini atlatabilir.|

### 🚩 CTF ve Sızma Testi İpuçları

1. **Hız vs. Gizlilik:** CTF'lerde hız (`THREADS` artırmak) önemliyken, gerçek sızma testlerinde yüksek thread sayısı IPS/IDS cihazları tarafından engellenmenize neden olabilir. `DELAY` ve `JITTER` parametrelerini kullanarak trafiği zamana yayın.
    
2. **db_nmap Kullanımı:** Metasploit içinde `nmap` yerine `db_nmap` kullanırsanız, tarama sonuçları otomatik olarak Metasploit veritabanına kaydedilir. Daha sonra `hosts` ve `services` komutlarıyla bu verileri listeleyebilirsiniz.
    
3. **NetBIOS ve Bilgi İfşası:** `udp_sweep` veya `nbname` modülleri ile elde edilen makine isimleri (PC-MUHASEBE gibi) size ağdaki kritik makineleri (Domain Controller gibi) hedefleme şansı verir.
    
4. **SMB Versiyonu Kritikliği:** `smb_version` modülü ile Windows sürümünü netleştirmek, **EternalBlue (MS17-010)** gibi kritik exploitlerin çalışıp çalışmayacağını anlamanın en hızlı yoludur.
    

### Faydalı Metasploit Komutları

- `services -p 445`: Veritabanında sadece 445. portu açık olan makineleri listeler.
    
- `hosts -c address,os_name`: Keşfedilen makinelerin sadece IP ve İşletim Sistemi bilgilerini gösterir.
    
   