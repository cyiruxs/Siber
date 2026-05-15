Bu görevde, kuralların tetiklenme nedenlerini ve dahil olan koşulları belirlemeye çalışacağız. Bunu başarmak için `-vv` veya **very verbose** parametresini kullanacağız.

|Seçenek (Option)|Açıklama (Description)|Örnek Sözdizimi (Sample Syntax)|
|---|---|---|
|**-v** veya **--verbose**|Verbose sonuç belgesini etkinleştirir.|`capa.exe -v .\cryptbot.bin`|
|**-vv** veya **--vverbose**|Very verbose sonuç belgesini etkinleştirir.|`capa.exe -vv .\cryptbot.bin`|

Hadi çalıştıralım!

### Terminal



```
PS C:\Users\Administrator\Desktop\capa> capa -vv .\cryptbot.bin
loading : 100%|████████████████████| 485/485 [00:00<00:00, 1108.84     rules/s]/ analyzing program...
```

Bu bize daha ayrıntılı sonuçlar verecektir; ancak bu işlem çok zaman alacaktır. Bunu zaten işledik ve "C:\Users\Administrator\Desktop\capa" içindeki dosyayı `cryptbot_vv.txt` olarak adlandırdık. Unutmayın, aracın çalışmasının bitmesini beklemenize gerek yok; bunu aracın çalışmasını deneyimlemeniz ve parametrelerini test etmeniz için yaptık.

Başka bir PowerShell terminali açın ve `Get-Content cryptbot_vv.txt` komutunu kullanarak dosyanın içine bakın.

### Terminal

Plaintext

```
PS C:\Users\Administrator\Desktop\capa> Get-Content .\cryptbot_vv.txt
```

Dosyayı açtınız mı? Buna benzer üç binden fazla satırınız var mı? Bir terminal veya metin editörü kullanarak bu kadar büyük miktarda bilgiye erişmek zorlayıcı olacaktır.

Bu sonucu kolaylıkla analiz etmek için iki şey yapmamız gerekiyor. İlk olarak, `-j` ve `-vv` parametrelerini kullanacağız ve sonucu bir `.json` dosyasına yönlendireceğiz. Komut şu şekilde olacaktır: `capa.bin -j -vv .\cryptbot.bin > cryptbot_vv.json`.

### Terminal

Plaintext

```
PS C:\Users\Administrator\Desktop\capa> capa.bin -j -vv .\cryptbot.bin > cryptbot_vv.json
loading : 100%|████████████████████| 485/485 [00:00<00:00, 1108.84     rules/s]/ analyzing program...
```

Yine bu, çalıştırdığımız önceki komutlara benzer şekilde çok zaman alacaktır. Bunu işledik ve "C:\Users\Administrator\Desktop\capa" adresinde bulunan `cryptbot_vv.json` adında bir dosya oluşturduk. Ayrıca dosyayı bu göreve ekledik. Unutmayın, aracın çalışmasının bitmesini beklemenize gerek yok; bunu aracın çalışmasını deneyimlemeniz ve parametrelerini test etmeniz için yaptık.

Bir sonraki adımımıza başlayabiliriz.

---

### CAPA Web Explorer

Yapmamız gereken ikinci şey, dosyayı **CAPA Explorer Web**'e yüklemektir. Ya bu bağlantıdaki çevrimiçi sürümü ya da sanal makinede zaten bulunan çevrimdışı sürümü kullanabiliriz. Masaüstünde `capa_web_explorer_offline.html` adında bir Google Chrome tarayıcısı bulunmaktadır. Alternatif olarak, normal bir Chrome tarayıcı yer imini kullanarak buna erişebilirsiniz. Yerel sayfanın hedef makinedeki Chrome'da yüklenmesinin bir dakika kadar sürebileceğini unutmayın.

Artık ana sayfaya erişimimiz olmalı!

Sayfanın sol alt kısmında bulunan **Upload from local** butonunu bulun ve `C:\Users\Administrator\Desktop\capa` içindeki `cryptbot_vv.json` dosyasını seçin. Yüklendikten sonra benzer bir çıktı almalısınız.

Bu iyi ve kullanımı daha kolay görünmüyor mu? Bahse girerim öyledir!

Şimdi, araca yapılan bu mükemmel eklentiyi keşfetme zamanı. Bazı yetenekleri gözden geçireceğiz ve kural içinde tam olarak neyin eşleştiğini kontrol edeceğiz. Bu, kuralın nasıl çalıştığı hakkında bize daha iyi bir fikir verecektir.

Aşağıdaki ilk örneğimizi inceleyelim. Yeteneğin **reference anti-VM strings targeting VMWare** olduğunu ve karşılık gelen kural yapılandırma dosyası veya **yaml** dosyasının `anti-VM-Strings-targeting-VMWare.yml` olduğunu biliyoruz. Görseldeki kutuya dikkat edin.

Ardından, size kuralın içeriğine dair bir genel bakış sunalım. **CAPA**, analiz edilen dosya içinde dizgilerin olup olmadığını kontrol etmek için aşağıdaki dizgileri kullandığından **features** kısmına odaklanın.
### Terminal

YAML

```
rule:
  meta:
    name: reference anti-VM strings targeting VMWare
    namespace: anti-analysis/anti-vm/vm-detection
    authors:
      - michael.hunhoff@mandiant.com
      - "@johnk3r"
    scopes:
      static: file
      dynamic: file
    att&ck:
      - Defense Evasion::Virtualization/Sandbox Evasion::System Checks [T1497.001]
    mbc:
      - Anti-Behavioral Analysis::Virtual Machine Detection [B0009]
    references:
      - https://github.com/LordNoteworthy/al-khaser/blob/master/al-khaser/AntiVM/VMWare.cpp
    examples:
      - al-khaser_x86.exe_
      - b83480162ede09d4aa6d4850f9faa0a4c3834152752fd04cfdb22d647aa1f825:0x17D80
  features:
    - or:
      - string: /VMWare/i
      - string: /VMTools/i
      - string: /SOFTWARE\\VMware, Inc\.\\VMware Tools/i
      - string: /VMWare/i
      - string: /VMTools/i
      - string: /SOFTWARE\\VMware, Inc\.\\VMware Tools/i
      - string: /vmnet\.sys/i
      - string: /vmmouse\.sys/i
      - string: /vmusb\.sys/i
      - string: /vm3dmp\.sys/i
      - string: /vmci\.sys/i
      - string: /vmhgfs\.sys/i
      - string: /vmmemctl\.sys/i
      - string: /vmx86\.sys/i
      - string: /vmrawdsk\.sys/i
      - string: /vmusbmouse\.sys/i
      - string: /vmkdb\.sys/i
      - string: /vmnetuserif\.sys/i
      - string: /vmnetadapter\.sys/i
      - string: /\\\\.\\HGFS/i
      - string: /\\\\.\\vmci/i
      - string: /vmtoolsd\.exe/i
      - string: /vmwaretray\.exe/i
      - string: /vmwareuser\.exe/i
      - string: /VGAuthService\.exe/i
      - string: /vmacthlp\.exe/i
      - string: /vmci/i
        description: VMWare VMCI Bus Driver
      - string: /vmhgfs/i
        description: VMWare Host Guest Control Redirector
      - string: /vmmouse/i
      - string: /vmmemctl/i
        description: VMWare Guest Memory Controller Driver
      - string: /vmusb/i
      - string: /vmusbmouse/i
      - string: /vmx_svga/i
      - string: /vmxnet/i
      - string: /vmx86/i
      - string: /VMwareVMware/i
      - string: /vmGuestLib\.dll/i
      - string: /vmGuestLib\.dll/i
      - string: /Applications\\VMwareHostOpen\.exe/i
      - string: /vm3dgl\.dll/i
      - string: /vmdum\.dll/i
      - string: /vm3dver\.dll/i
      - string: /vmtray\.dll/i
      - string: /VMToolsHook\.dll/i
      - string: /vmmousever\.dll/i
      - string: /VmGuestLibJava\.dll/i
      - string: /vmscsi\.sys/i
```

Gördünüz mü? Doğru! **features** altında, `string: /VMWare/i` ifadesi **CAPA Web Explorer** tarafından referans alınmaktadır. Basitçe **CAPA**, bu ad alanı altında, kural içindeki koşulları ve **regex** kullanarak değeri **VMWare** olan dizgileri tanımlayabildiğimizi söylüyor.

Başka bir örneğe bakalım. Yeteneğin **schedule task via schtasks** olduğunu ve karşılık gelen kuralın `schedule task via schtasks.yml` olduğunu biliyoruz. Görseldeki kutuya dikkat edin.

Aynısı ilk örneğimiz için de geçerli; size kuralın içeriğine genel bir bakış sunacağız. **CAPA**, analiz edilen dosya içinde dizgiler olup olmadığını kontrol etmek için aşağıdaki dizgileri kullandığından **features** kısmına odaklanın.

### Terminal

```
rule:
  meta:
    name: schedule task via schtasks
    namespace: persistence/scheduled-tasks
    authors:
      - 0x534a@mailbox.org
    scopes:
      static: function
      dynamic: thread
    att&ck:
      - Persistence::Scheduled Task/Job::Scheduled Task [T1053.005]
    examples:
      - 79cde1aa711e321b4939805d27e160be:0x401440
  features:
    - and:
      - match: host-interaction/process/create
      - or:
        - and:
          - string: /schtasks/i
          - string: /\/create /i
        - string: /Register-ScheduledTask /i
```

**feature** altında, `string: /schtasks/i` ve `/\/create /i` ifadeleri **CAPA Web Explorer** tarafından referans alınmaktadır. Basitçe **CAPA**, bu ad alanı altında ve kural içindeki koşulları ve **regex** kullanarak değeri **schtasks** ve **create** olan dizgileri tanımlayabildiğimizi söylüyor.

---

### Global Search Box

Bu aracın bir başka harika özelliği de filtre seçenekleri ve oldukça yardımcı olan **Global Search** kutusudur.

Herhangi bir metin editörüyle karşılaştırıldığında **CAPA Web Explorer**'ı kullanarak bu bunaltıcı bilgiyi hızla inceleyebiliriz.