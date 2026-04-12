
# Metasploit Payload Türleri ve Meterpreter Versiyonları

Metasploit payload'ları başlangıçta iki kategoriye ayrılabilir; inline (single/tekil olarak da adlandırılır) ve staged (aşamalı).

Hatırlayacağınız üzere, staged (aşamalı) payload'lar hedefe iki adımda gönderilir. İlk kısım yüklenir (stager) ve payload'un geri kalanını talep eder. Bu, başlangıçtaki payload boyutunun daha küçük olmasını sağlar. Inline (tekil) payload'lar ise tek bir adımda gönderilir. Meterpreter payload'ları da aşamalı ve inline versiyonlara ayrılmıştır. Ancak Meterpreter, hedef sisteminize göre seçebileceğiniz çok geniş bir versiyon yelpazesine sahiptir.

Mevcut Meterpreter versiyonları hakkında fikir edinmenin en kolay yolu, aşağıda görüldüğü gibi msfvenom kullanarak bunları listelemektir.

`msfvenom --list payloads` komutunu kullandık ve "meterpreter" payload'larını (komut satırına `| grep meterpreter` ekleyerek) ayıkladık, böylece çıktı sadece bunları göstermektedir. Bu komutu AttackBox üzerinde deneyebilirsiniz.

**Meterpreter Payload'larını Listeleme**

Bash

```
root@ip-10-10-186-44:~# msfvenom --list payloads | grep meterpreter
    android/meterpreter/reverse_http                    Android'de bir meterpreter sunucusu çalıştırır. İletişimi HTTP üzerinden tüneller
    android/meterpreter/reverse_https                   Android'de bir meterpreter sunucusu çalıştırır. İletişimi HTTPS üzerinden tüneller
    android/meterpreter/reverse_tcp                     Android'de bir meterpreter sunucusu çalıştırır. Geri bağlantı aşamalandırıcısı
    android/meterpreter_reverse_http                    Saldırgana geri bağlanır ve bir Meterpreter shell açar
    android/meterpreter_reverse_https                   Saldırgana geri bağlanır ve bir Meterpreter shell açar
    android/meterpreter_reverse_tcp                     Saldırgana geri bağlanır ve bir Meterpreter shell açar
    apple_ios/aarch64/meterpreter_reverse_http          Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    apple_ios/aarch64/meterpreter_reverse_https         Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    apple_ios/aarch64/meterpreter_reverse_tcp           Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    apple_ios/armle/meterpreter_reverse_http            Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    apple_ios/armle/meterpreter_reverse_https           Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    apple_ios/armle/meterpreter_reverse_tcp             Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    java/meterpreter/bind_tcp                           Java'da bir meterpreter sunucusu çalıştırır. Bir bağlantı için dinler
    java/meterpreter/reverse_http                       Java'da bir meterpreter sunucusu çalıştırır. İletişimi HTTP üzerinden tüneller
    java/meterpreter/reverse_https                      Java'da bir meterpreter sunucusu çalıştırır. İletişimi HTTPS üzerinden tüneller
    java/meterpreter/reverse_tcp                        Java'da bir meterpreter sunucusu çalıştırır. Geri bağlantı aşamalandırıcısı
    linux/aarch64/meterpreter/reverse_tcp               Mettle sunucu payload'unu enjekte eder (staged). Saldırgana geri bağlanır
    linux/aarch64/meterpreter_reverse_http              Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    linux/aarch64/meterpreter_reverse_https             Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    linux/aarch64/meterpreter_reverse_tcp               Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    linux/armbe/meterpreter_reverse_http                Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    linux/armbe/meterpreter_reverse_https               Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    linux/armbe/meterpreter_reverse_tcp                 Meterpreter / Mettle sunucu payload'unu çalıştırır (stageless)
    linux/armle/meterpreter/bind_tcp                    Mettle sunucu payload'unu enjekte eder (staged). Bir bağlantı için dinler
    linux/armle/meterpreter/reverse_tcp                 Mettle sunucu payload'unu enjekte eder (staged). Saldırgana geri bağlanır [...]
```

Bu liste, aşağıdaki platformlar için mevcut olan Meterpreter versiyonlarını gösterecektir:

- Android
    
- Apple iOS
    
- Java
    
- Linux
    
- OSX
    
- PHP
    
- Python
    
- Windows
    

Hangi Meterpreter versiyonunu kullanacağınıza dair kararınız çoğunlukla üç faktöre dayanacaktır:

1. **Hedef işletim sistemi** (Hedef işletim sistemi Linux mu yoksa Windows mu? Bir Mac cihazı mı? Bir Android telefon mu? vb.)
    
2. **Hedef sistemde mevcut olan bileşenler** (Python yüklü mü? Bu bir PHP web sitesi mi? vb.)
    
3. **Hedef sistemle kurabileceğiniz ağ bağlantısı türleri** (Ham TCP bağlantılarına izin veriyorlar mı? Yalnızca bir HTTPS ters bağlantınız mı olabilir? IPv6 adresleri IPv4 adresleri kadar yakından izlenmiyor mu? vb.)
    

Eğer Meterpreter'ı Msfvenom tarafından oluşturulan bağımsız bir payload olarak kullanmıyorsanız, seçiminiz exploit tarafından da kısıtlanabilir. Bazı exploit'lerin, aşağıda `ms17_010_eternalblue` exploit'i örneğinde görebileceğiniz gibi varsayılan bir Meterpreter payload'una sahip olacağını fark edeceksiniz.

**MS17-010 İçin Varsayılan Payload**

Bash

```
msf6 > use exploit/windows/smb/ms17_010_eternalblue 
[*] Using configured payload windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Ayrıca herhangi bir modül ile `show payloads` komutunu kullanarak mevcut diğer payload'ları listeleyebilirsiniz.

**Mevcut Payload'lar**

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
   8   windows/x64/meterpreter/bind_named_pipe                      manual  No     Windows Meterpreter (Reflective Injection x64), Windows x64 Bind Named Pipe Stager [...]
```

---

### 🛡️ Siber Güvenlik ve CTF İpucu

Payload listesinde isimlere dikkat et abi; eğer isimde `/` varsa (örneğin `meterpreter/reverse_tcp`), bu genellikle **staged** (aşamalı) bir payload'dur ve hedefe iki parça halinde gider. Eğer isimde `_` varsa (örneğin `meterpreter_reverse_tcp`), bu **stageless/inline** (tekil) bir payload'dur ve her şey tek seferde gönderilir. Sıkı güvenlik duvarı olan ağlarda bazen tekil payload'lar daha iyi sonuç verebilir.