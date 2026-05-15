### Capability ve Namespace Bloğu


```
┌──────────────────────────────────────────────────────┬──────────────────────────────────────────────────────┐
│ Capability                                           │ Namespace                                            │
├──────────────────────────────────────────────────────┼──────────────────────────────────────────────────────┤
│ reference anti-VM strings                            │ anti-analysis/anti-vm/vm-detection                   │
│ reference anti-VM strings targeting VMWare           │ anti-analysis/anti-vm/vm-detection                   │
│ reference anti-VM strings targeting VirtualBox       │ anti-analysis/anti-vm/vm-detection                   │
│ contain obfuscated stackstrings (2 matches)          │ anti-analysis/obfuscation/string/stackstring         │
│ reference HTTP User-Agent string                     │ communication/http                                   │
│ check HTTP status code                               │ communication/http/client                            │
│ reference Base64 string                              │ data-manipulation/encoding/base64                    │
│ encode data using XOR                                │ data-manipulation/encoding/xor                       │
│ contain a thread local storage (.tls) section        │ executable/pe/section/tls                            │
│ get common file path                                 │ host-interaction/file-system                         │
│ create directory                                     │ host-interaction/file-system/create                  │
│ delete file                                          │ host-interaction/file-system/delete                  │
│ read file on Windows (4 matches)                     │ host-interaction/file-system/read                    │
│ write file on Windows (5 matches)                    │ host-interaction/file-system/write                   │
│ get thread local storage value                       │ host-interaction/process                             │
│ create process on Windows                            │ host-interaction/process/create                      │
│ allocate or change RWX memory                        │ host-interaction/process/inject                      │
│ reference cryptocurrency strings                     │ impact/cryptocurrency                                │
│ link function at runtime on Windows (5 matches)      │ linking/runtime-linking                              │
│ parse PE header (4 matches)                          │ load-code/pe                                         │
│ resolve function by parsing PE exports (186 matches) │ load-code/pe                                         │
│ run PowerShell expression                            │ load-code/powershell/                                │
│ schedule task via at                                 │ persistence/scheduled-tasks                          │
│ schedule task via schtasks                           │ persistence/scheduled-tasks                          │
└──────────────────────────────────────────────────────┴──────────────────────────────────────────────────────┘
```

Bu bloğun içeriği aşağıdaki formatta temsil edilir:

|Format|Örnek (Sample)|Açıklama (Explanation)|
|---|---|---|
|**Capability (Rule Name)::TLN (Top-Level Namespace)/Namespace**|reference anti-VM strings::Anti-Analysis/anti-vm/vm-detection|**Reference anti-VM strings** = Capability (Rule Name)<br><br>  <br><br>**Anti-Analysis** = TLN veya Top-Level Namespace<br><br>  <br><br>**anti-vm/vm-detection** = Namespace|


---

### Namespaces (Ad Alanları)

**CAPA**, aynı amaca sahip öğeleri gruplandırmak için **namespaces** kullanır.

|Top-Level Namespace (TLN)|Açıklama (Explanation)|
|---|---|
|**anti-analysis**|Kötü amaçlı yazılımlar tarafından analizden kaçınmak için sergilenen davranışları tespit etmek üzere özel olarak tasarlanmış bir dizi kural içerir. Bu davranışlar arasında **obfuscation**, **packing** ve **anti-debugging** teknikleri yer alır.|
|**collection**|Kötü amaçlı yazılımların sızdırma veya diğer amaçlar için listeleyebileceği ve toplayabileceği veriyle ilgili bir dizi kural içerir. Bunu kötü amaçlı yazılım davranışının "veri toplama" (**data-gathering**) yönü olarak düşünün.|
|**communication**|Kötü amaçlı yazılımlar tarafından sergilenen farklı iletişim davranışlarıyla ilgili bir dizi kural içerir. Bu, veri iletimi ve alımı, **command and control** iletişimleri ve diğer ağla ilgili davranışlar dahil olmak üzere yazılımın ağlarla nasıl etkileşime girdiğini kapsar.|
|**compiler**|Yürütülebilir dosyaların oluşturulmasında kullanılan belirli derleme ortamlarını veya derleyicileri tanımak için bir dizi kural ve yapılandırma içerir. Bu ad alanları temel olarak bir programın derleme sürecini tanımlayan benzersiz "imza" (**signature**) görevi görür.|
|**data-manipulation**|Yürütülebilir dosyalar içindeki verilerin değiştirilmesini içeren davranışları düzenleyen bir dizi kural içerir. Bu yön, **String Encryption** ve **Data Encoding** gibi eylemleri kapsayan kötü amaçlı yazılım davranışının "veri dönüştürme" (**data transformation**) bileşeni olarak kabul edilebilir.|
|**executable**|Yürütülebilir dosyalardaki özniteliklerle ilgili bir dizi kural içerir. Bu öznitelikler, yürütülebilir dosya ile ilişkili **PE sections** veya **debug info** bilgilerini içerir.|
|**host-interaction**|Ana sistemle etkileşim içeren davranışlarla ilgili bir dizi kural içerir. Bu, kötü amaçlı yazılımın çevresiyle nasıl etkileşime girdiğini kapsar. Özellikle bu ad alanındaki kurallar; dosya ve dizin oluşturma, silme veya değiştirme dahil olmak üzere diskteki dosyaları okuma, yazma veya değiştirme ile ilgili davranışları yakalayabilir.|
|**impact**|Bir programın davranışının potansiyel sonuçları veya etkileriyle ilgili bir dizi kural içerir. Bunu, bu kötü amaçlı yazılımın neden olabileceği olası zarara odaklanan yön olarak düşünün. Uzaktan erişim kurma, veri sızdırma, imha veya değiştirme ile ilgili davranışları içerebilir.|
|**internal**|Sistem içinde yer alan kurallar analistler tarafından doğrudan kullanım veya raporlama için tasarlanmamıştır. Bunun yerine bu kurallar, **CAPA** aracı içindeki dahili amaçlara yöneliktir ve kural geliştirme ve yürütmenin sahne arkası yönü olarak hizmet eder.|
|**lib**|Diğer kuralları oluşturmak için kullanılan yapı taşlarıdır (**building blocks**).|
|**linking**|Program yürütme sırasında harici kod veya kütüphanelerin bağlanması veya dinamik olarak yüklenmesi ile ilgili davranışları tanımlayan kurallar içerir. Bu, programın güvenliği için çok önemlidir. **Linking** davranışını anlamak, kötü amaçlı yazılımların belirli görevleri yerine getirmek için genellikle harici kütüphanelere (**OpenSSL**, **Zlib** vb.) bağımlı olması nedeniyle yeteneklerini anlamaya yardımcı olur.|
|**load-code**|Program yürütme sırasında kodun dinamik olarak yüklenmesi veya yürütülmesi ile ilgili davranışlarla ilgili bir dizi kural ve düzenleme içerir. Bu kavram, programın yürütülmesi sırasında yetkisiz kod girişini içeren kötü amaçlı yazılım davranışının "çalışma zamanı kod enjeksiyonu" (**runtime code injection**) yönüyle eşdeğer görülebilir.|
|**malware-family**|Belirli kötü amaçlı yazılım aileleri veya gruplarıyla bağlantılı davranışlarla ilgili bir dizi kural içerir. Bilinen ailelerle ilişkili belirgin özellikleri veya "imzaları" tanımlamanın bir yolu olarak hizmet eder.|
|**nursery**|Henüz tam olarak cilalanmamış (olgunlaşmamış) kuralları içeren bir hazırlık alanıdır (**staging ground**).|
|**persistence**|Ele geçirilmiş bir sistem içinde erişimi sürdürme veya kalıcılık sağlama ile ilgili davranışlarla ilgili kurallar içerir. Bu ad alanı, kötü amaçlı yazılımın ele geçirilmiş bir ortamda nasıl varlık kurup sürdürebileceğini anlamaya odaklanır.|
|**runtime**|Programın üzerinde çalıştığı dili veya platformu tanımlamaya çalışan bir dizi kural içerir.|
|**targeting**|ATM'lerle etkileşime giren programlar tarafından sergilenen davranışlarla ilgili bir dizi kural içerir.|

Bunun nasıl çalıştığını aşağıdaki tabloyu inceleyerek görelim:

|Top-Level Namespace (TLN)|Namespaces|Rule YAML File|Açıklama (Explanation)|
|---|---|---|---|
|**Anti-Analysis**|**anti-vm/vm-detection**|reference-anti-vm-strings-targeting-virtualbox.yml<br><br>  <br><br>reference-anti-vm-strings-targeting-virtualpc.yml|"**anti-vm/vm-detection**" ad alanı, sanal makine (**VM**) ortamlarını tespit etmeye yönelik kurallar içerir. Bu kurallar, yazılımın çalışırken **VM**'leri tespit etmek için yaygın olarak kullandığı belirli dizgileri veya desenleri tanımlamaya odaklanır. **CAPA**, bu kuralları kullanarak yazılımın **VMware**'e özgü kayıt defteri anahtarlarını, **VMware** araçlarının varlığını veya diğer **VM** ile ilgili öğeleri arayıp aramadığını belirleyebilir.|
|**Anti-Analysis**|**obfuscation**|obfuscated-with-dotfuscator.yml<br><br>  <br><br>obfuscated-with-smartassembly.yml|Kötü amaçlı yazılımlar analizi zorlaştırmak için sıklıkla **obfuscation** teknikleri kullanır. Bunlar arasında **String Encryption**, **Code Obfuscation**, **Packing** ve **Anti-Debugging Tricks** bulunur. **obfuscation** ad alanı, kodun gerçek amacını gizleyen veya belirsizleştiren bu teknikleri ele alır.|

Bu örnek için, **TLN** veya **Top-Level Namespace** olarak yalnızca **Anti-Analysis** kullandık. Bu **TLN** altında, **anti-vm/vm-detection** ve **obfuscation** gibi gruplandırılmış ad alanlarına (**namespaces**) sahibiz. Her ad alanının içinde yine birlikte gruplandırılmış bir kural koleksiyonu vardır. **anti-vm/vm-detection** için kurallarımız ve bunların yapılandırma dosyaları mevcuttur:

- `reference-anti-vm-strings-targeting-virtualbox.yml`
    
- `reference-anti-vm-strings-targeting-virtualpc.yml`
    

Aynısı **obfuscation** ad alanı için de geçerlidir. Gruplandırılmış kurallarımız vardır:

- `obfuscated-with-dotfuscator.yml`
    
- `obfuscated-with-smartassembly.yml`
    

Tekrar belirtmek gerekirse, bunların hepsi hala **TLN Anti-Analysis** altındadır!

Lütfen aşağıdaki illüstrasyona da başvurun.

---

Yukarıdaki tabloda belirtilenlere ek olarak, **Anti-Analysis** altında ilgili kurallara sahip birkaç ad alanı daha bulunmaktadır. Daha derinlemesine incelemek isterseniz lütfen ilgili bağlantıyı kontrol edin. **collection**, **compiler**, **persistence**, **linking** ve **impact** gibi diğer **TLN** veya **Top-Level Namespaces** ile ilgileniyorsanız diğer bağlantıları kullanın.