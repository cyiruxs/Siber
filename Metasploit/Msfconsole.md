<<<<<<< HEAD
# Metasploit Konsolu (msfconsole)

Daha önce belirtildiği gibi, konsol Metasploit Framework ile ana etkileşim arayüzünüz olacaktır. Bunu AttackBox terminalinizde veya Metasploit Framework'ün kurulu olduğu herhangi bir sistemde **`msfconsole`** komutunu kullanarak başlatabilirsiniz.

**msfconsole**

Bash

```
root@ip-10-10-220-191:~# msfconsole                                                   
=======
- [ ] # Metasploit Konsolu (msfconsole)

Daha önce belirtildiği gibi, konsol Metasploit Framework ile ana etkileşim arayüzünüz olacaktır. Bunu AttackBox terminalinizde veya Metasploit Framework'ün kurulu olduğu herhangi bir sistemde **`msfconsole`** komutunu kullanarak başlatabilirsiniz.
   
>>>>>>> origin/main

                 _---------.
             .' #######   ;."
  .---,.    ;@             @@`;   .---,..
." @@@@@'.,'@@            @@@@@',.'@@@@ ".
'-.@@@@@@@@@@@@@          @@@@@@@@@@@@@ @;
   `.@@@@@@@@@@@@        @@@@@@@@@@@@@@ .'
     "--'.@@@  -.@        @ ,'-   .'--"
          ".@' ; @       @ `.  ;'
            |@@@@ @@@     @    .
             ' @@@ @@   @@    ,
              `.@@@@    @@   .
                ',@@     @   ;           _____________
                 (   3 C    )     /|___ / Metasploit! \
                 ;@'. __*__,."    \|--- \_____________/
                  '(.,...."/


       =[ metasploit v6.0                         ]
+ -- --=[ 2048 exploits - 1105 auxiliary - 344 post       ]
+ -- --=[ 562 payloads - 45 encoders - 10 nops            ]
+ -- --=[ 7 evasion                                       ]

Metasploit tip: Search can apply complex filters such as search cve:2009 type:exploit, see all the filters with help search

msf6 >
```

Başlatıldıktan sonra, komut satırı isteminin **msf6** (veya kurulu Metasploit sürümüne bağlı olarak msf5) şeklinde değiştiğini göreceksiniz. Metasploit konsolu (msfconsole), aşağıda görebileceğiniz gibi tıpkı normal bir komut satırı kabuğu (shell) gibi kullanılabilir. İlk komut olan **`ls`**, Metasploit'in `msfconsole` komutu kullanılarak başlatıldığı klasörün içeriğini listeler.

Bunu, Google'ın DNS IP adresine (8.8.8.8) gönderilen bir **`ping`** takip eder. Linux olan AttackBox üzerinden çalıştığımız için, yalnızca tek bir ping gönderilmesi adına **`-c 1`** seçeneğini eklemek zorunda kaldık. Aksi takdirde, ping işlemi **CTRL+C** kullanılarak durdurulana kadar devam ederdi.

**Metasploit İçinde Linux Komutları**

Bash

```
msf6 > ls
[*] exec: ls

burpsuite_community_linux_v2021_8_1.sh	Instructions  Scripts
Desktop					Pictures      thinclient_drives
Downloads				Postman       Tools
msf6 > ping -c 1 8.8.8.8
[*] exec: ping -c 1 8.8.8.8

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=109 time=1.33 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 1.335/1.335/1.335/0.000 ms
msf6 >
```

Aşağıda görüldüğü gibi, terminal ekranını temizlemek için **`clear`** dahil çoğu Linux komutunu destekleyecektir ancak normal bir komut satırının bazı özelliklerini kullanmanıza izin vermeyecektir (örneğin çıktı yönlendirmeyi desteklemez).

**Başarısız Çıktı Yönlendirme**

Bash

```
msf6 > help > help.txt
[-] No such command
msf6 >
```

Konuyla ilgili olarak, **`help`** komutu tek başına veya belirli bir komut için kullanılabilir. Aşağıda, yakında ele alacağımız **`set`** komutu için yardım menüsü yer almaktadır.

**Yardım Özelliği**

Bash

```
msf6 > help set
Usage: set [option] [value]

Set the given option to value.  If value is omitted, print the current value.
If both are omitted, print options that are currently set.

If run from a module context, this will set the value in the module's
datastore.  Use -g to operate on the global datastore.

If setting a PAYLOAD, this command can take an index from `show payloads'.

msf6 >
```

Daha önce yazdığınız komutları görmek için **`history`** komutunu kullanabilirsiniz.

**History Komutu**

Bash

```
msf6 > history
1  use exploit/multi/http/nostromo_code_exec
2  set lhost 10.10.16.17
3  set rport 80
4  options
5  set rhosts 10.10.29.187
6  run
7  exit
8  exit -y
9  version
10  use exploit/multi/script/web_delivery
```

<<<<<<< HEAD
msfconsole'un önemli bir özelliği **sekme tamamlama (tab completion)** desteğidir. Bu, daha sonra Metasploit komutlarını kullanırken veya modüllerle uğraşırken işinize yarayacaktır. Örneğin, **`he`** yazmaya başlar ve tab tuşuna basarsanız, bunun otomatik olarak **`help`** şeklinde tamamlandığını görürsünüz.
=======
msfconsole'un önemli bir özelliği **sekme tamamlama (tab completion)** desteğidir. Bu, daha sonra Metasploit komutlarını kullanırken veya modüllerle uğraarken işinize yarayacaktır. Örneğin, **`he`** yazmaya başlar ve tab tuşuna basarsanız, bunun otomatik olarak **`help`** şeklinde tamamlandığını görürsünüz.
>>>>>>> origin/main

Msfconsole bağlam (context) ile yönetilir; bu, global bir değişken olarak ayarlanmadığı sürece, kullanmaya karar verdiğiniz modülü değiştirirseniz tüm parametre ayarlarının kaybolacağı anlamına gelir. Aşağıdaki örnekte, **ms17_010_eternalblue** exploit'ini kullandık ve **RHOSTS** gibi parametreleri ayarladık. Başka bir modüle (örneğin bir port tarayıcıya) geçecek olursak, yaptığımız tüm değişiklikler `ms17_010_eternalblue` exploit bağlamında kaldığından RHOSTS değerini tekrar ayarlamamız gerekecektir.

Bu özelliği daha iyi anlamak için aşağıdaki örneğe bakalım. İllüstrasyon amaçlı MS17-010 “Eternalblue” exploit'ini kullanacağız.

**`use exploit/windows/smb/ms17_010_eternalblue`** komutunu yazdığınızda, komut satırı isteminin `msf6`dan `msf6 exploit(windows/smb/ms17_010_eternalblue)` şeklinde değiştiğini göreceksiniz. "EternalBlue", çok sayıda Windows sistemindeki SMBv1 sunucusunu etkileyen bir zafiyet için ABD Ulusal Güvenlik Ajansı (N.S.A.) tarafından geliştirildiği iddia edilen bir exploit'tir. **SMB** (Server Message Block), Windows ağlarında dosya paylaşımı ve hatta yazıcılara dosya göndermek için yaygın olarak kullanılır. EternalBlue, Nisan 2017'de siber suç grubu "Shadow Brokers" tarafından sızdırılmıştır. Mayıs 2017'de bu zafiyet, WannaCry fidye yazılımı saldırısında dünya çapında istismar edilmiştir.

**Bir Exploit Kullanma**

Bash

```
msf6 > use exploit/windows/smb/ms17_010_eternalblue 
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Kullanılacak modül, **`use`** komutunun ardından arama sonucu satırının başındaki numara ile de seçilebilir. İstem değişmiş olsa da, daha önce bahsedilen komutları hala çalıştırabildiğimizi fark edeceksiniz. Bu, bir işletim sistemi komut satırında tipik olarak beklediğiniz gibi bir klasöre "girmediğimiz" anlamına gelir.

**Bir Bağlam İçinde Linux Komutları**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > ls
[*] exec: ls

burpsuite_community_linux_v2021_8_1.sh	Instructions  Scripts
Desktop					Pictures      thinclient_drives
Downloads				Postman       Tools
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

İstem bize artık içinde çalışacağımız bir bağlamın ayarlandığını söyler. Bunu **`show options`** komutunu yazarak görebilirsiniz.

**Seçenekleri Göster (Show options)**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'
   RPORT          445              yes       The target port (TCP)
   SMBDomain      .                no        (Optional) The Windows domain to use for authentication
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target.


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     10.10.220.191    yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows 7 and Server 2008 R2 (x64) All Service Packs


msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

<<<<<<< HEAD
Bu, daha önce seçtiğimiz exploit ile ilgili seçenekleri yazdıracaktır. `show options` komutu, kullanıldığı bağlama bağlı olarak farklı çıktılara sahip olacaktır. Yukarıdaki örnek, bu exploit'in RHOSTS ve RPORT gibi değişkenleri ayarlamamızı gerektireceğini göstermektedir. Öte yandan, bir sızma sonrası (post-exploitation) modülü sadece bir **SESSION ID** ayarlamamıza ihtiyaç duyabilir. Bir oturum (session), sızma sonrası modülünün kullanacağı hedef sisteme olan mevcut bir bağlantıdır.
=======
Bu, daha önce seçtiğimiz exploit ile ilgili seçenekleri yazdıracaktır. `show options` komutu, kullanıldığı bağlama bağlı olarak farklı çıktılara sahip olacaktır. Yukarıdaki örnek, bu exploit'in RHOSTS ve RPORT gibi değişkenleri ayarlamamızı gerektireceğini göstermektedir. Öte yandan, bir sızma sonrası (post-exploitation) modülü sadece bir **SESSION ID** ayarlamamıza ihtiyaç duyabilir (aşağıdaki ekran görüntüsüne bakın). Bir oturum (session), sızma sonrası modülünün kullanacağı hedef sisteme olan mevcut bir bağlantıdır.
>>>>>>> origin/main

**Bir Sızma Sonrası Modülü İçin Seçenekler**

Bash

```
msf6 post(windows/gather/enum_domain_users) > show options

Module options (post/windows/gather/enum_domain_users):

   Name     Current Setting  Required  Description
   ----     -----------  --------  -----------
   HOST                      no        Target a specific host
   SESSION                   yes       The session to run this module on.
   USER                      no        Target User for NetSessionEnum

msf6 post(windows/gather/enum_domain_users) >
```

**`show`** komutu herhangi bir bağlamda kullanılabilir ve mevcut modülleri listelemek için ardından bir modül tipi (auxiliary, payload, exploit vb.) getirilebilir. Aşağıdaki örnek, ms17-010 Eternalblue exploit'i ile kullanılabilecek payload'ları listeler.

**Show Payloads Komutu**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > show payloads

Compatible Payloads
===================

   #   Name                                        Disclosure Date  Rank    Check  Description
   -   ----                                        ---------------  ----    -----  -----------
   0   generic/custom                                               manual  No     Custom Payload
   1   generic/shell_bind_tcp                                       manual  No     Generic Command Shell, Bind TCP Inline
   2   generic/shell_reverse_tcp                                    manual  No     Generic Command Shell, Reverse TCP Inline
   3   windows/x64/exec                                             manual  No     Windows x64 Execute Command
   4   windows/x64/loadlibrary                                      manual  No     Windows x64 LoadLibrary Path
   5   windows/x64/messagebox                                       manual  No     Windows MessageBox x64
   6   windows/x64/meterpreter/bind_ipv6_tcp                        manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 IPv6 Bind TCP Stager
   7   windows/x64/meterpreter/bind_ipv6_tcp_uuid                   manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 IPv6 Bind TCP Stager with UUID Support 
```

`show` komutu `msfconsole` isteminden kullanılırsa tüm modülleri listeleyecektir. Şimdiye kadar gördüğümüz **`use`** ve **`show options`** komutları Metasploit'teki tüm modüller için özdeştir.

**`back`** komutunu kullanarak bağlamdan ayrılabilirsiniz.

**Back Komutu**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > back
msf6 > 
```

Herhangi bir modül hakkında daha fazla bilgi, bağlamı içindeyken **`info`** komutu yazılarak elde edilebilir.

**Info Komutu**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > info

       Name: MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
     Module: exploit/windows/smb/ms17_010_eternalblue
   Platform: Windows
       Arch: 
 Privileged: Yes
    License: Metasploit Framework License (BSD)
       Rank: Average
  Disclosed: 2017-03-14

... (Açıklama ve Referanslar kısmı devam eder)
```

Alternatif olarak, `msfconsole` isteminden modülün yolunu takip eden `info` komutunu kullanabilirsiniz (örneğin `info exploit/windows/smb/ms17_010_eternalblue`). Info bir yardım menüsü değildir; modül hakkında yazarı, ilgili kaynaklar vb. gibi ayrıntılı bilgileri görüntüler.

### Arama (Search)

msfconsole'daki en kullanışlı komutlardan biri **`search`** komutudur. Bu komut, verilen arama parametresiyle ilgili modüller için Metasploit Framework veritabanını tarayacaktır. CVE numaralarını, exploit adlarını (eternalblue, heartbleed vb.) veya hedef sistemi kullanarak aramalar yapabilirsiniz.

**Arama Komutu**

Bash

```
msf6 > search ms17-010

Matching Modules
================

   #  Name                                      Disclosure Date  Rank     Check  Description
   -  ----                                      ---------------  ----     -----  -----------
   0  auxiliary/admin/smb/ms17_010_command      2017-03-14       normal   No     MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Command Execution
   1  auxiliary/scanner/smb/smb_ms17_010                         normal   No     MS17-010 SMB RCE Detection
   2  exploit/windows/smb/ms17_010_eternalblue  2017-03-14       average  Yes    MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
   3  exploit/windows/smb/ms17_010_psexec       2017-03-14       normal   Yes    MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Code Execution
   4  exploit/windows/smb/smb_doublepulsar_rce  2017-04-14       great    Yes    SMB DOUBLEPULSAR Remote Code Execution
```

`search` komutunun çıktısı, döndürülen her modülün genel bir özetini sunar. "Name" sütununun zaten modül adından daha fazla bilgi verdiğini fark edebilirsiniz. Modülün tipini (auxiliary, exploit vb.) ve kategorisini (scanner, admin, windows, Unix vb.) görebilirsiniz. Arama sonucunda döndürülen herhangi bir modülü, sonucun başındaki numara ile birlikte `use` komutunu kullanarak kullanabilirsiniz. (Örneğin `use auxiliary/admin/smb/ms17_010_command` yerine `use 0`)

Döndürülen bir diğer temel bilgi ise "**rank**" (sıralama) sütunundadır. Exploit'ler güvenilirliklerine göre derecelendirilir.

Arama işlevini **type** ve **platform** gibi anahtar kelimeleri kullanarak yönlendirebilirsiniz.

Örneğin, arama sonuçlarımızın yalnızca yardımcı (auxiliary) modülleri içermesini isteseydik, tipi `auxiliary` olarak ayarlayabilirdik. Aşağıdaki ekran görüntüsü `search type:auxiliary telnet` komutunun çıktısını göstermektedir.

**Modül Tipine Göre Arama**

Bash

```
msf6 > search type:auxiliary telnet

Matching Modules
================

   #   Name                                                Disclosure Date  Rank    Check  Description
   -   ----                                                ---------------  ----    -----  -----------
   0   auxiliary/admin/http/dlink_dir_300_600_exec_noauth  2013-02-04       normal  No     D-Link DIR-600 / DIR-300 Unauthenticated Remote Command Execution
... (Liste devam eder)
```

Lütfen exploit'lerin hedef sistemdeki bir zafiyetten yararlandığını ve her zaman beklenmedik davranışlar gösterebileceğini unutmayın. Düşük dereceli bir exploit mükemmel çalışabilir ve mükemmel dereceli bir exploit çalışmayabilir, ya da daha kötüsü hedef sistemi çökertebilir.

---

<<<<<<< HEAD
### 🛡️ Siber Güvenlik ve CTF İpucu
=======
### 🛡️ Siber Güvenlik ve CTF İpuçları
>>>>>>> origin/main

- **RHOSTS Ayarlama:** Bir modül seçtikten sonra hedef IP'yi ayarlamak için `set RHOSTS [Hedef_IP]` komutunu kullan.
    
- **LHOST Ayarlama:** Dinleyici IP'nizi (genellikle kendi VPN IP'niz) ayarlamak için `set LHOST [Senin_IP]` komutunu kullan.
    
<<<<<<< HEAD
- **Arama İpucu:** Spesifik bir platform için arama yaparken `search platform:windows type:exploit` gibi filtreler kullanarak zaman kazanabilirsin.m 
=======
- **Arama İpucu:** Spesifik bir platform için arama yaparken `search platform:windows type:exploit` gibi filtreler kullanarak zaman kazanabilirsin.
>>>>>>> origin/main
