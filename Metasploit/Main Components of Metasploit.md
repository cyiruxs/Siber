# Metasploit Framework Modülleri ve Yapısı

Metasploit Framework'ü kullanırken, öncelikle Metasploit konsolu ile etkileşime geçeceksiniz. Bunu AttackBox terminalinden **msfconsole** komutunu kullanarak başlatabilirsiniz. Konsol, Metasploit Framework'ün farklı modülleriyle etkileşim kurmak için ana arayüzünüz olacaktır. Modüller, bir zafiyeti istismar etmek (exploit), bir hedefi taramak veya bir kaba kuvvet (brute-force) saldırısı gerçekleştirmek gibi belirli bir görevi yerine getirmek üzere oluşturulmuş, Metasploit framework içindeki küçük bileşenlerdir.

Modüllere dalmadan önce, tekrar eden birkaç kavramı netleştirmek yararlı olacaktır: **zafiyet (vulnerability)**, **sömürü (exploit)** ve **yük (payload)**.

- **Exploit**: Hedef sistemde bulunan bir zafiyeti kullanan bir kod parçasıdır.
    
- **Vulnerability**: Hedef sistemi etkileyen bir tasarım, kodlama veya mantık hatasıdır. Bir zafiyetin istismar edilmesi, gizli bilgilerin ifşa edilmesiyle sonuçlanabilir veya saldırganın hedef sistemde kod yürütmesine izin verebilir.
    
- **Payload**: Bir exploit bir zafiyetten yararlanacaktır. Ancak, exploit'in istediğimiz sonucu vermesini istiyorsak (hedef sisteme erişim sağlamak, gizli bilgileri okumak vb.), bir payload kullanmamız gerekir. Payload'lar, hedef sistemde çalışacak olan koddur.
    

Modüller ve her birinin altındaki kategoriler aşağıda listelenmiştir. Bunlar referans amacıyla verilmiştir, ancak onlarla Metasploit konsolu (**msfconsole**) aracılığıyla etkileşime gireceksiniz.

### Auxiliary (Yardımcı Modüller)

Tarayıcılar, örümcekler (crawlers) ve fuzzer'lar gibi her türlü destekleyici modül burada bulunabilir.

**Terminal**

Bash

```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 auxiliary/
auxiliary/
├── admin
├── analyze
├── bnat
├── client
├── cloud
├── crawler
├── docx
├── dos
├── example.py
├── example.rb
├── fileformat
├── fuzzers
├── gather
├── parser
├── pdf
├── scanner
├── server
├── sniffer
├── spoof
├── sqli
├── voip
└── vsploit

20 directories, 2 files
```

### Encoders (Kodlayıcılar)

Encoder'lar, imza tabanlı bir antivirüs çözümünün onları kaçırması umuduyla exploit ve payload'u kodlamanıza olanak tanır. İmza tabanlı antivirüs ve güvenlik çözümleri, bilinen tehditlerin bir veritabanına sahiptir. Tehditleri, şüpheli dosyaları bu veritabanıyla karşılaştırarak tespit ederler ve bir eşleşme varsa uyarı verirler. Bu nedenle, antivirüs çözümleri ek kontroller gerçekleştirebildiğinden, encoder'ların başarı oranı sınırlı olabilir.

**Terminal**

Bash

```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 encoders/
encoders/
├── cmd
├── generic
├── mipsbe
├── mipsle
├── php
├── ppc
├── ruby
├── sparc
├── x64
└── x86

10 directories, 0 files
```

### Evasion (Atlatma)5

Encoder'lar payload'u kodlarken, bunlar antivirüs yazılımından kaçmak için doğrudan bir girişim olarak görülmemelidir. Öte yandan, "evasion" modülleri 6bunu az çok başarıyla deneyecektir.

**Terminal**

Bash

```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 2 evasion/
evasion/
└── windows
    ├── applocker_evasion_install_util.rb
    ├── applocker_evasion_msbuild.rb
    ├── applocker_evasion_presentationhost.rb
    ├── applocker_evasion_regasm_regsvcs.rb
    ├── applocker_evasion_workflow_compiler.rb
    ├── process_herpaderping.rb
    ├── syscall_inject.rb
    ├── windows_defender_exe.rb
    └── windows_defender_js_hta.rb

1 directory, 9 files
```

### Exploits (Sömürü Kodları)789

Exploit'ler, hedef sisteme göre düzgün bir şekilde organize edilmiştir.

**Terminal1314**

Bash

```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 exploits/
exploits/
├── aix
├── android
├── apple_ios
├── bsd
├── bsdi
├── dialup
├── example_linux_priv_esc.rb
├── example.py
├── example.rb
├── example_webapp.rb
├── firefox
├── freebsd
├── hpux
├── irix
├── linux
├── mainframe
├── multi
├── netware
├── openbsd
├── osx
├── qnx
├── solaris
├── unix
└── windows

20 directories, 4 files
```

### NOPs (No Operation)

NOP'lar (İşlem Yok) kelimenin tam anlamıyla hiçbir şey yapmazlar. Intel x86 işlemci ailesinde **0x90** ile temsil edilirler ve bunu takiben işlemci bir döngü boyunca hiçbir şey yapmaz. Genellikle tutarlı payload boyutları elde etmek için bir tampon (buffer) olarak kullanılırlar.

**Terminal**

Bash

```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 nops/
nops/
├── aarch64
├── armle
├── cmd
├── mipsbe
├── php
├── ppc
├── sparc
├── tty
├── x64
└── x86

10 directories, 0 files
```

### Payloads (Yükler)

Payload'lar, hedef sistemde çalışacak kodlardır. Exploit'ler hedef sistemdeki bir zafiyetten yararlanacaktır, ancak istenen sonucu elde etmek için bir payload'a ihtiyacımız olacaktır. Örnekler şunlar olabilir; bir shell almak, hedef sisteme bir kötü amaçlı yazılım veya arka kapı (backdoor) yüklemek, bir komut çalıştırmak veya bir sızma testi raporuna eklemek için bir kavram kanıtı (proof of concept) olarak **calc.exe**'yi başlatmak. Hedef sistemde **calc.exe** uygulamasını başlatarak hesap makinesini uzaktan çalıştırmak, hedef sistemde komutlar yürütebileceğimizi göstermenin zararsız bir yoludur.

Hedef sistemde komut çalıştırmak zaten önemli bir adımdır ancak hedef sistemde yürütülecek komutları yazmanıza izin veren etkileşimli bir bağlantıya sahip olmak daha iyidir. Bu tür etkileşimli bir komut satırına "**shell**" denir. Metasploit, hedef sistemde shell açabilen farklı payload'lar gönderme yeteneği sunar.

**Terminal**

Bash

```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 payloads/
payloads/
├── adapters
├── singles
├── stagers
└── stages

4 directories, 0 files
```

Payloads altında dört farklı dizin göreceksiniz: **adapters, singles, stagers** ve **stages**.

- **Adapters**: Bir adapter, single payload'ları farklı formatlara dönüştürmek için sarar. Örneğin, normal bir single payload, payload'u yürütecek tek bir powershell komutu haline getirecek bir Powershell adapter içine sarılabilir.
    
- **Singles**: Çalışmak için ek bir bileşen indirmesine gerek duymayan, kendi kendine yeten payload'lardır (kullanıcı ekle, notepad.exe'yi başlat vb.).
    
- **Stagers**: Metasploit ile hedef sistem arasında bir bağlantı kanalı kurmaktan sorumludur. Staged payload'lar ile çalışırken kullanışlıdır. "Staged payload'lar" önce hedef sisteme bir stager yükleyecek, ardından payload'un geri kalanını (**stage**) indirecektir. Bu, tek seferde gönderilen tam payload'a kıyasla payload'un ilk boyutunun nispeten küçük olması nedeniyle bazı avantajlar sağlar.
    
- **Stages**: Stager tarafından indirilir. Bu, daha büyük boyutlu payload'lar kullanmanıza olanak tanır.
    

Metasploit, single (ayrıca "inline" olarak da adlandırılır) payload'ları ve staged payload'ları tanımlamanıza yardımcı olacak ince bir yola sahiptir.

1. `generic/shell_reverse_tcp`
    
2. `windows/x64/shell/reverse_tcp`
    

Her ikisi de reverse Windows shell'leridir. İlki, "shell" ve "reverse" arasındaki "**_**" işaretiyle belirtildiği gibi bir **inline (veya single)** payload'dur. İkincisi ise "shell" ve "reverse" arasındaki "**/**" işaretiyle belirtildiği gibi bir **staged** payload'dur.

### Post (Sızma Sonrası)

Post modülleri, yukarıda listelenen sızma testi sürecinin son aşaması olan sızma sonrası (**post-exploitation**) aşamasında faydalı olacaktır.

**Terminal**

Bash

```
root@ip-10-10-135-188:/opt/metasploit-framework/embedded/framework/modules# tree -L 1 post/
post/
├── aix
├── android
├── apple_ios
├── bsd
├── firefox
├── hardware
├── linux
├── multi
├── networking
├── osx
├── solaris
└── windows

12 directories, 0 files
```

Bu modüllere daha yakından aşina olmak isterseniz, onları Metasploit kurulumunuzun **modules** klasörü altında bulabilirsiniz. AttackBox için bunlar `/opt/metasploit-framework/embedded/framework/modules` altındadır.

---

### 🛡️ Siber Güvenlik Tablosu: Modül Seçim Rehberi2122

| **Modül Tipi** | **Amaç**              | **Örnek Senaryo**                                                            |
| -------------- | --------------------- | ---------------------------------------------------------------------------- |
| **Exploit**    | Zafiyeti Sömürmek3132 | Bir sunucuda açık olan SMB zafiyetini (EternalBlue) tetiklemek.              |
| **Payload      | Erişim Sağlamak       | Sömürü sonrası karşı makineden kendimize **Meterpreter** bağlantısı almak.   |
| **Auxiliary**  | Bilgi Toplamak        | Hedef ağdaki tüm IP'lerin açık portlarını taramak.                           |
| **Post**       | Hak Yükseltmek        | İçeri sızdıktan sonra sistemdeki parola hash'lerini toplamak (**hashdump**). |
