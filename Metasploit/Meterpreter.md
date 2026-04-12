# Meterpreter

Meterpreter, sızma testi sürecini birçok değerli bileşenle destekleyen bir Metasploit payload'udur. Meterpreter, hedef sistem üzerinde çalışır ve bir komut ve kontrol (C2) mimarisi içerisinde bir ajan (agent) görevi görür. Hedef işletim sistemi ve dosyalarla etkileşime girerken Meterpreter'ın özelleşmiş komutlarını kullanırsınız.

Meterpreter'ın, hedef sisteme bağlı olarak farklı işlevsellikler sunan birçok sürümü mevcuttur.

### Meterpreter Nasıl Çalışır?

- **Bellek Üzerinde Çalışma:** Meterpreter hedef sistem üzerinde çalışır ancak oraya kurulmaz. Bellekte (RAM) çalışır ve kendini hedefteki diske yazmaz.
    
- **Antivirüs Atlatma:** Bu özelliğin amacı, antivirüs taramaları sırasında tespit edilmekten kaçınmaktır. Varsayılan olarak çoğu antivirüs yazılımı, diskteki yeni dosyaları tarar (örneğin internetten bir dosya indirdiğinizde). Meterpreter, hedef sistemde diske yazılması gereken bir dosya (örneğin `meterpreter.exe`) bulundurmamak için RAM üzerinde çalışır. Bu sayede Meterpreter sadece bir süreç (process) olarak görülür ve hedef sistemde bir dosyası bulunmaz.
    
- **Ağ Gizliliği (IPS/IDS):** Meterpreter, Metasploit'in çalıştığı sunucuyla (genellikle saldırgan makineniz) şifreli iletişim kullanarak ağ tabanlı IPS (Saldırı Önleme Sistemi) ve IDS (Saldırı Tespit Sistemi) çözümleri tarafından tespit edilmekten kaçınmayı amaçlar. Eğer hedef organizasyon yerel ağa gelen ve ağdan çıkan şifreli trafiği (örneğin HTTPS) deşifre edip incelemiyorsa, IPS ve IDS çözümleri aktiviteyi tespit edemeyecektir.
    

Meterpreter ana antivirüs yazılımları tarafından tanınıyor olsa da, bu özellikleri belirli bir düzeyde gizlilik sağlar.

### Süreç Analizi ve İzler

Aşağıdaki örnek, MS17-010 zafiyeti kullanılarak istismar edilmiş bir Windows makinesini göstermektedir. Meterpreter'ın **1304** işlem kimliği (PID) ile çalıştığını göreceksiniz; bu numara sizde farklı olacaktır. Meterpreter'ın çalıştığı işlem kimliğini döndüren **`getpid`** komutu kullanılmıştır. İşlem kimliği (veya süreç tanımlayıcı), işletim sistemleri tarafından çalışan süreçleri tanımlamak için kullanılır. Linux veya Windows'ta çalışan tüm süreçlerin benzersiz bir kimlik numarası vardır; bu numara ihtiyaç duyulduğunda süreçle etkileşime girmek (örneğin durdurmak) için kullanılır.

**Getpid**

Bash

```
meterpreter > getpid 
Current pid: 1304
```

Hedef sistemde çalışan süreçleri **`ps`** komutuyla listelersek, PID 1304'ün beklenildiği gibi `Meterpreter.exe` değil, **`spoolsv.exe`** olduğunu görürüz.

**ps Komutu**

Bash

```
meterpreter > ps

Process List
============

 PID   PPID  Name                  Arch  Session  User                          Path
 ---   ----  ----                  ----  -------  ----                          ----
 0     0     [System Process]                                                   
 4     0     System                x64   0                                      
 396   644   LogonUI.exe           x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\LogonUI.exe
 416   4     smss.exe              x64   0        NT AUTHORITY\SYSTEM           \SystemRoot\System32\smss.exe
 428   692   svchost.exe           x64   0        NT AUTHORITY\SYSTEM           
 548   540   csrss.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\csrss.exe
 596   540   wininit.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\wininit.exe
 604   588   csrss.exe             x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\csrss.exe
 644   588   winlogon.exe          x64   1        NT AUTHORITY\SYSTEM           C:\Windows\system32\winlogon.exe
 692   596   services.exe          x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\services.exe
 700   692   sppsvc.exe            x64   0        NT AUTHORITY\NETWORK SERVICE  
 716   596   lsass.exe             x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\lsass.exe
 1276  1304  cmd.exe               x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\cmd.exe
 1304  692   spoolsv.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\System32\spoolsv.exe
 1340  692   svchost.exe           x64   0        NT AUTHORITY\LOCAL SERVICE    
 1388  548   conhost.exe           x64   0        NT AUTHORITY\SYSTEM           C:\Windows\system32\conhost.exe
```

Bir adım daha ileri gidip Meterpreter süreci (bu durumda PID 1304) tarafından kullanılan **DLL**'lere (Dinamik Bağlantı Kitaplıkları) baksak bile, göze çarpan bir şey (örneğin bir `meterpreter.dll`) bulamazdık.

**Meterpreter Süreci**

DOS

```
C:\Windows\system32>tasklist /m /fi "pid eq 1304"
tasklist /m /fi "pid eq 1304"

Image Name                     PID Modules                                     
========================= ======== ============================================
spoolsv.exe                   1304 ntdll.dll, kernel32.dll, KERNELBASE.dll,    
                                   msvcrt.dll, sechost.dll, RPCRT4.dll,        
                                   USER32.dll, GDI32.dll, LPK.dll, USP10.dll,  
                                   POWRPROF.dll, SETUPAPI.dll, CFGMGR32.dll,   
                                   ADVAPI32.dll, OLEAUT32.dll, ole32.dll,      
                                   DEVOBJ.dll, DNSAPI.dll, WS2_32.dll,         
                                   NSI.dll, IMM32.DLL, MSCTF.dll,              
                                   CRYPTBASE.dll, slc.dll, RpcRtRemote.dll,    
                                   secur32.dll, SSPICLI.DLL, credssp.dll,      
                                   IPHLPAPI.DLL, WINNSI.DLL, mswsock.dll,      
                                   wshtcpip.dll, wship6.dll, rasadhlp.dll,     
                                   fwpuclnt.dll, CLBCatQ.DLL, umb.dll,         
                                   ATL.DLL, WINTRUST.dll, CRYPT32.dll,         
                                   MSASN1.dll, localspl.dll, SPOOLSS.DLL,      
                                   srvcli.dll, winspool.drv,                   
                                   PrintIsolationProxy.dll, FXSMON.DLL,        
                                   tcpmon.dll, snmpapi.dll, wsnmp32.dll,       
                                   msxml6.dll, SHLWAPI.dll, usbmon.dll,        
                                   wls0wndh.dll, WSDMon.dll, wsdapi.dll,       
                                   webservices.dll, FirewallAPI.dll,           
                                   VERSION.dll, FunDisc.dll, fdPnp.dll,        
                                   winprint.dll, USERENV.dll, profapi.dll,     
                                   GPAPI.dll, dsrole.dll, win32spl.dll,        
                                   inetpp.dll, DEVRTL.dll, SPINF.dll,          
                                   CRYPTSP.dll, rsaenh.dll, WINSTA.dll,        
                                   cscapi.dll, netutils.dll, WININET.dll,      
                                   urlmon.dll, iertutil.dll, WINHTTP.dll,      
                                   webio.dll, SHELL32.dll, MPR.dll,            
                                   NETAPI32.dll, wkscli.dll, PSAPI.DLL,        
                                   WINMM.dll, dhcpcsvc6.DLL, dhcpcsvc.DLL,     
                                   apphelp.dll, NLAapi.dll, napinsp.dll,       
                                   pnrpnsp.dll, winrnr.dll                     
```

Meterpreter'ı tespit etmek için kullanılabilecek teknikler ve araçlar bu odanın kapsamı dışındadır. Bu bölüm, Meterpreter'ın ne kadar gizli çalıştığını göstermeyi amaçlamıştır; unutmayın, çoğu antivirüs yazılımı yine de onu tespit edecektir.

Ayrıca Meterpreter'ın, saldırganın sistemiyle şifreli (**TLS**) bir iletişim kanalı kuracağını not etmekte fayda vardır.

---

### 🛡️ Siber Güvenlik İpucu: Süreç Taşıma (Process Migration)

Abi, yukarıdaki `ps` çıktısında gördüğün gibi Meterpreter bazen kendini `spoolsv.exe` (yazdırma servisi) gibi masum bir servisin içine saklar. Ancak eğer kurban makineyi yeniden başlatırsa veya o servis kapanırsa bağlantın kopar.

**İpucu:** Bağlantıyı aldıktan sonra daha kalıcı bir sürece geçmek için `migrate` komutunu kullanabilirsin. Örneğin `explorer.exe` (masaüstü arayüzü) genellikle en güvenli limandır. `meterpreter > migrate [Explorer_PID]`