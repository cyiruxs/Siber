# Metasploit Veritabanı ve Proje Yönetimi

TryHackMe üzerindeki tek bir hedefle etkileşime girerken gerekli olmasa da, gerçek bir sızma testi çalışması muhtemelen birkaç hedefe sahip olacaktır. Metasploit, proje yönetimini basitleştirmek ve parametre değerlerini ayarlarken olası karışıklıkları önlemek için bir veritabanı işlevine sahiptir.

Öncelikle Metasploit'in kullanacağı PostgreSQL veritabanını şu komutla başlatmanız gerekecektir: `systemctl start postgresql`. Ardından `msfdb init` komutunu kullanarak Metasploit Veritabanını başlatmanız (initialize) gerekecektir. Ancak, `msfdb init` komutunu root olarak çalıştırmayı denemek "Lütfen msfdb'yi root olmayan bir kullanıcı olarak çalıştırın" (Please run msfdb as a non-root user) hata mesajını verecektir. Bu durum, `sudo -u postgres msfdb init` komutu kullanılarak **postgres** hesabı olarak çalıştırılarak çözülebilir.

Aşağıdaki terminal örnek çıktıyı göstermektedir. Belirtildiği gibi, aşağıdaki adımlar AttackBox üzerinde zaten gerçekleştirilmiştir; ancak bunları tekrarlamakla ilgileniyorsanız, önce `sudo -u postgres msfdb delete` komutunu kullanarak mevcut veritabanını silmeniz gerekecektir.

**Postgresql'i Başlatma**

Bash

```
root@attackbox:~# systemctl start postgresql
root@attackbox:~# sudo -u postgres msfdb init 
Running the 'init' command for the database:
Creating database at /var/lib/postgresql/.msf4/db
Creating db socket file at /tmp
Starting database at /var/lib/postgresql/.msf4/db...waiting for server to start.... done
server started
success
Creating database users
Writing client authentication configuration file /var/lib/postgresql/.msf4/db/pg_hba.conf
Stopping database at /var/lib/postgresql/.msf4/db
Starting database at /var/lib/postgresql/.msf4/db...waiting for server to start.... done
server started
success
Creating initial database schema
Database initialization successful
root@attackbox:~#
```

Artık `msfconsole`'u başlatabilir ve **`db_status`** komutunu kullanarak veritabanı durumunu kontrol edebilirsiniz.

**Veritabanı durumunu kontrol etme**

Bash

```
msf6 > db_status
[*] Connected to msf. Connection type: postgresql.
msf6 >
```

Veritabanı özelliği, farklı projeleri izole etmek için çalışma alanları (workspaces) oluşturmanıza olanak tanır. İlk başlatıldığında, varsayılan (default) çalışma alanında olmalısınız. Mevcut çalışma alanlarını **`workspace`** komutunu kullanarak listeleyebilirsiniz.

**Çalışma alanlarını listeleme**

Bash

```
msf6 > workspace
* default
msf6 >
```

Sırasıyla, `-a` parametresini kullanarak bir çalışma alanı ekleyebilir veya `-d` parametresini kullanarak bir çalışma alanını silebilirsiniz. Aşağıdaki ekran görüntüsü "tryhackme" adında yeni bir çalışma alanının oluşturulduğunu göstermektedir.

**Bir çalışma alanı ekleme**

Bash

```
msf6 > workspace -a tryhackme
[*] Added workspace: tryhackme
[*] Workspace: tryhackme
msf5 > workspace
default
* tryhackme
msf6 >
```

Yeni veritabanı adının kırmızıyla yazıldığını ve başında bir `*` sembolü olduğunu da fark edeceksiniz. Çalışma alanları arasında gezinmek için sadece `workspace` komutunun ardından istediğiniz çalışma alanı adını yazarak kullanabilirsiniz.

**Çalışma alanlarını değiştirme**

Bash

```
msf6 > workspace
default
* tryhackme
msf5 > workspace default
[*] Workspace: default
msf5 > workspace 
tryhackme
* default
msf6 >
```

`workspace` komutu için mevcut seçenekleri listelemek için **`workspace -h`** komutunu kullanabilirsiniz.

**Workspace yardım menüsü**

Bash

```
msf6 > workspace -h
Usage:
workspace                  List workspaces
workspace -v               List workspaces verbosely
workspace [name]           Switch workspace
workspace -a [name] ...    Add workspace(s)
workspace -d [name] ...    Delete workspace(s)
workspace -D               Delete all workspaces
workspace -r     Rename workspace
workspace -h               Show this help information
```

Normal Metasploit kullanımından farklı olarak, Metasploit bir veritabanı ile başlatıldığında, `help` komutu size "Database Backends Commands" (Veritabanı Arka Plan Komutları) menüsünü gösterecektir.

**Veritabanı arka plan komutları**

Plaintext

```
Database Backend Commands
=========================

Command           Description
-------           -----------
analyze           Belirli bir adres veya adres aralığı hakkındaki veritabanı bilgilerini analiz eder
db_connect        Mevcut bir veri servisine bağlanır
db_disconnect     Mevcut veri servisinden bağlantıyı keser
db_export         Veritabanının içeriğini içeren bir dosya dışa aktarır
db_import         Bir tarama sonuç dosyasını içe aktarır (dosya türü otomatik olarak algılanır)
db_nmap           Nmap'i yürütür ve çıktıyı otomatik olarak kaydeder
db_rebuild_cache  Veritabanında saklanan modül önbelleğini yeniden oluşturur (kullanımdan kaldırıldı)
db_remove         Kaydedilen veri servisi girişini kaldırır
db_save           Mevcut veri servisi bağlantısını başlangıçta yeniden bağlanmak için varsayılan olarak kaydeder
db_status         Mevcut veri servisi durumunu gösterir
hosts             Veritabanındaki tüm ana makineleri listeler
loot              Veritabanındaki tüm ganimetleri (loot) listeler
notes             Veritabanındaki tüm notları listeler
services          Veritabanındaki tüm servisleri listeler
vulns             Veritabanındaki tüm zafiyetleri listeler
workspace         Veritabanı çalışma alanları arasında geçiş yapar
```

Aşağıda gösterilen **`db_nmap`** kullanarak bir Nmap taraması çalıştırırsanız, tüm sonuçlar veritabanına kaydedilecektir.

**db_nmap komutu**

Bash

```
msf6 > db_nmap -sV -p- 10.10.12.229
[*] Nmap: Starting Nmap 7.80 ( https://nmap.org ) at 2021-08-20 03:15 UTC
[*] Nmap: Nmap scan report for ip-10-10-12-229.eu-west-1.compute.internal (10.10.12.229)
[*] Nmap: Host is up (0.00090s latency).
[*] Nmap: Not shown: 65526 closed ports
[*] Nmap: PORT      STATE SERVICE            VERSION
[*] Nmap: 135/tcp   open  msrpc              Microsoft Windows RPC
[*] Nmap: 139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn
[*] Nmap: 445/tcp   open  microsoft-ds       Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
[*] Nmap: 3389/tcp  open  ssl/ms-wbt-server?
[*] Nmap: 49152/tcp open  msrpc              Microsoft Windows RPC
[*] Nmap: 49153/tcp open  msrpc              Microsoft Windows RPC
[*] Nmap: 49154/tcp open  msrpc              Microsoft Windows RPC
[*] Nmap: 49158/tcp open  msrpc              Microsoft Windows RPC
[*] Nmap: 49162/tcp open  msrpc              Microsoft Windows RPC
[*] Nmap: MAC Address: 02:CE:59:27:C8:E3 (Unknown)
[*] Nmap: Service Info: Host: JON-PC; OS: Windows; CPE: cpe:/o:microsoft:windows
[*] Nmap: Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
[*] Nmap: Nmap done: 1 IP address (1 host up) scanned in 94.91 seconds
msf6 >
```

Artık hedef sistemlerde çalışan ana makinelere (hosts) ve servislere (services) ilişkin bilgilere sırasıyla **`hosts`** ve **`services`** komutlarıyla ulaşabilirsiniz.

**Hosts ve servisler**

Bash

```
msf6 > hosts

Hosts
=====

address       mac                name                                        os_name  os_flavor  os_sp  purpose  info  comments
-------       ---                ----                                        -------  ---------  -----  -------  ----  --------
10.10.12.229  02:ce:59:27:c8:e3  ip-10-10-12-229.eu-west-1.compute.internal  Unknown                    device         

msf6 > services
Services
========

host          port   proto  name               state  info
----          ----   -----  ----               -----  ----
10.10.12.229  135    tcp    msrpc              open   Microsoft Windows RPC
10.10.12.229  139    tcp    netbios-ssn        open   Microsoft Windows netbios-ssn
10.10.12.229  445    tcp    microsoft-ds       open   Microsoft Windows 7 - 10 microsoft-ds workgroup: WORKGROUP
10.10.12.229  3389   tcp    ssl/ms-wbt-server  open   
10.10.12.229  49152  tcp    msrpc              open   Microsoft Windows RPC
10.10.12.229  49153  tcp    msrpc              open   Microsoft Windows RPC
10.10.12.229  49154  tcp    msrpc              open   Microsoft Windows RPC
10.10.12.229  49158  tcp    msrpc              open   Microsoft Windows RPC
10.10.12.229  49162  tcp    msrpc              open   Microsoft Windows RPC

msf6 >
```

`hosts -h` ve `services -h` komutları mevcut seçeneklere daha aşina olmanıza yardımcı olabilir. Ana makine bilgileri veritabanında saklandıktan sonra, bu değeri RHOSTS parametresine eklemek için **`hosts -R`** komutunu kullanabilirsiniz.

### Örnek İş Akışı

1. `use auxiliary/scanner/smb/smb_ms17_010` komutuyla potansiyel MS17-010 zafiyetlerini bulan zafiyet tarama modülünü kullanacağız.
    
2. `hosts -R` kullanarak RHOSTS değerini ayarlıyoruz.
    
3. Tüm değerlerin doğru atanıp atanmadığını kontrol etmek için `show options` yazdık. (Bu örnekte, 10.10.12.229, daha önce `db_nmap` komutunu kullanarak taradığımız IP adresidir).
    
4. Tüm parametreler ayarlandıktan sonra, `run` veya `exploit` komutunu kullanarak sömürüyü (exploit) başlatıyoruz.
    

**Kaydedilen ana makineleri kullanma**

Bash

```
msf6 > use auxiliary/scanner/smb/smb_ms17_010 
msf5 auxiliary(scanner/smb/smb_ms17_010) > hosts -R 

Hosts
=====

address       mac                name                                        os_name  os_flavor  os_sp  purpose  info  comments
-------       ---                ----                                        -------  ---------  -----  -------  ----  --------
10.10.12.229  02:ce:59:27:c8:e3  ip-10-10-12-229.eu-west-1.compute.internal  Unknown                    device         

RHOSTS => 10.10.12.229

msf6 auxiliary(scanner/smb/smb_ms17_010) > show options 

Module options (auxiliary/scanner/smb/smb_ms17_010):

Name         Current Setting                                                 Required  Description
----         ---------------                                                 --------  -----------
CHECK_ARCH   true                                                            no        Check for architecture on vulnerable hosts
CHECK_DOPU   true                                                            no        Check for DOUBLEPULSAR on vulnerable hosts
CHECK_PIPE   false                                                           no        Check for named pipe on vulnerable hosts
NAMED_PIPES  /usr/share/metasploit-framework/data/wordlists/named_pipes.txt  yes       List of named pipes to check
RHOSTS       10.10.12.229                                                    yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'
RPORT        445                                                             yes       The SMB service port (TCP)
SMBDomain    .                                                               no        The Windows domain to use for authentication
SMBPass                                                                      no        The password for the specified username
SMBUser                                                                      no        The username to authenticate as
THREADS      1                                                               yes       The number of concurrent threads (max one per host)

msf6 auxiliary(scanner/smb/smb_ms17_010) > run
```

Veritabanına kaydedilmiş birden fazla ana makine varsa, `hosts -R` komutu kullanıldığında tüm IP adresleri kullanılacaktır.

Tipik bir sızma testi çalışmasında aşağıdaki senaryoya sahip olabiliriz:

- `db_nmap` komutunu kullanarak mevcut ana makineleri bulma.
    
- Bunları daha fazla zafiyet veya açık portlar için tarama (bir port tarama modülü kullanarak).
    
- `-S` parametresiyle kullanılan `services` komutu, ortamdaki belirli servisleri aramanıza olanak tanır.
    

**Servisler için veritabanını sorgulama**

Bash

```
msf6 > services -S netbios                                                                                       
Services                                                                                                             
========                                                                                                             
                                                                                                                
host          port  proto  name         state  info                                                                              
----          ----  -----  ----         -----  ----                                                                              
10.10.12.229  139   tcp    netbios-ssn  open   Microsoft Windows netbios-ssn

msf6 >
```

Aşağıdaki gibi kolay lokmaları (low-hanging fruits) aramak isteyebilirsiniz:

- **HTTP**: SQL enjeksiyonu veya Uzaktan Kod Yürütme (RCE) gibi zafiyetler bulabileceğiniz bir web uygulamasına potansiyel olarak ev sahipliği yapabilir.
    
- **FTP**: Anonim girişe izin verebilir ve ilginç dosyalara erişim sağlayabilir.
    
- **SMB**: MS17-010 gibi SMB sömürülerine karşı savunmasız olabilir.
    
- **SSH**: Varsayılan veya tahmin edilmesi kolay kimlik bilgilerine sahip olabilir.
    
- **RDP**: Bluekeep'e karşı savunmasız olabilir veya zayıf kimlik bilgileri kullanılmışsa masaüstü erişimine izin verebilir.
    

Gördüğünüz gibi, Metasploit, çalışmalarınızı çalışma alanlarına ayırma, sonuçlarınızı üst düzeyde analiz etme ve verileri hızlı bir şekilde içe aktarıp keşfetme yeteneği gibi çalışmalara yardımcı olacak birçok özelliğe sahiptir.