### Capability (Yetenek)

Aşağıda **Capability** ve onunla ilgili **TLN**, **namespace** ve **yaml** dosyasıyla ilişkili kuralları içeren bir tablo bulunmaktadır. Lütfen dikkatlice inceleyin.

|Capability|Top-Level Namespace (TLN)|Namespaces|Rule YAML file|Notes|
|---|---|---|---|---|
|**reference anti-VM strings**|**Anti-Analysis**|**anti-vm/vm-detection**|`reference-anti-vm-strings.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**reference anti-VM strings targeting VMWare**|**Anti-Analysis**|**anti-vm/vm-detection**|`reference-anti-vm-strings-targeting-vmware.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**reference anti-VM strings targeting VirtualBox**|**Anti-Analysis**|**anti-vm/vm-detection**|`reference-anti-vm-strings-targeting-virtualbox.yml`|**TLN (Top-Level Namespace)**'i kontrol edebilirsiniz.|
|**reference HTTP User-Agent string**|**Communication**|**http/client**|`reference-http-user-agent-string.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**check HTTP status code**|**Communication**|**http**|`check-http-status-code.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**reference Base64 string**|**Data Manipulation**|**encoding/base64**|`reference-base64-string.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**encode data using XOR**|**Data Manipulation**|**encoding/XOR**|`encode-data-using-xor.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**contain a thread local storage (.tls) section**|**Executable**|**pe/section/tls**|`contain-a-thread-local-storage-tls-section.yml`|Daha fazla kural için **TLN**'i kontrol edebilirsiniz.|
|**get common file path**|**Host-Interaction**|**file-system**|`get-common-file-path.yml`|Daha fazla kural için **TLN**'i kontrol edebilirsiniz.|
|**create directory**|**Host-Interaction**|**file-system/create**|`create-directory.yml`|Daha fazla kural için **TLN**'i kontrol edebilirsiniz.|
|**delete file**|**Host-Interaction**|**file-system/delete**|`delete-file.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**read file on Windows**|**Host-Interaction**|**file-system/read**|`read-file-on-windows.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**write file on Windows**|**Host-Interaction**|**file-system/write**|`write-file-on-windows.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**get thread local storage value**|**Host-Interaction**|**process**|`get-thread-local-storage-value.yml`|Bu kural, cilalanmamış kurallar için bir hazırlık alanı olan **TLN Nursery** altında bulunur.|
|**allocate or change RWX memory**|**Host-Interaction**|**process/inject**|`allocate-or-change-rwx-memory.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**create process on Windows**|**Host-Interaction**|**process create**|`create-process-on-windows.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**reference cryptocurrency strings**|**Impact**|**impact/cryptocurrency**|`reference-cryptocurrency-strings.yml`|Bu kural, cilalanmamış kurallar için bir hazırlık alanı olan **TLN Nursery** altında bulunur.|
|**link function at runtime on Windows**|**Linking**|**runtime-linking**|`link-function-at-runtime-on-windows.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**parse PE header**|**load-code**|**load-code/pe**|`parse-pe-header.yml`, `resolve-function-by-parsing-pe-exports.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**resolve function by parsing PE exports**|**load-code**|**load-code/pe**|`resolve-function-by-parsing-pe-exports.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**run PowerShell expression**|**load-code**|**load-code/PowerShell**|`run-powershell-expression.yml`|Bu ad alanı altındaki tüm kuralları kontrol etmek için buraya tıklayın.|
|**schedule task via at**|**persistence**|**scheduled-tasks**|`schedule-task-via-at.yml`|Daha fazla kural için **TLN**'i kontrol edebilirsiniz.|
|**schedule task via schtasks**|**persistence**|**scheduled-tasks**|`schedule-task-via-schtasks.yml`|Daha fazla kural için **TLN**'i kontrol edebilirsiniz.|

Bunu daha fazla açıklamak için tablodaki ilk yetenek olan "**reference anti-VM strings**" öğesini kontrol edelim. **YML** formatındaki ilgili kuralların `reference-anti-vm-strings.yml` olduğunu not ediyoruz. Bu, **anti-vm/vm-detection** ad alanı altındadır ve bu da **Anti-Analysis Top-Level Namespace** altındadır. Bu bize, **CAPA**'nın `reference-anti-vm-strings.yml` kural dosyasını kullanarak, potansiyel olarak kötü amaçlı yazılımın **VMware**'e özgü kayıt defteri anahtarlarını, **VMware** araçlarının varlığını veya diğer **VM** ile ilgili öğeleri aradığını tanımlayabildiğini söyler. Kötü amaçlı yazılımlar genellikle tespitten kaçınmak için bu davranışı sergiler. Bu yüzden **CAPA** bunu işaretlemiştir.

Başka bir örneğe bakalım. "**schedule task via schtasks**" öğesine bakalım. **YML** formatındaki ilgili kuralların `schedule-task-via-schtasks.yml` olduğunu not ediyoruz. Bu, **scheduled-tasks** ad alanı altındadır ve bu da **persistence Top-Level Namespace** altındadır. Bu bize, **CAPA**'nın Windows işletim sistemi içindeki zamanlanmış görevlerle ilgili davranışları tanımlayabildiğini söyler. Yürütülebilir dosyanın, `schedule-task-via-schtasks.yml` içinde tanımlanan kuralı kullanarak kalıcılığı (**persistence**) sürdürmek için kendisini bir zamanlanmış görev olarak kaydettiğini gösteren desenleri tanımış olabilir.

Bekle bir dakika! Bir şey fark ettin mi? Doğru! **Capability** altındaki öğe, **Rules** altındaki **YML** dosyalarıyla aynı isme sahiptir, sadece boşluklar arasında bir tire (-) karakteri eklenmiştir! Basitçe çünkü **Capability**, kuralın adıdır.

Şimdi burada bazı istisnaları not etmek istiyoruz. **Capability** veya kuralların kendi **Namespace**'i altında bulunmadığı yerlerde; yukarıdaki tablodan **reference cryptocurrency strings** yeteneğini ele alalım; bu **Impact Top-Level Namespace** altında olmalıydı, değil mi? Ancak klasörleri incelerseniz ilgili kuralları orada bulamazsınız. Bu kural **Nursery TLN** altında bulunacaktır. Burası, henüz tam olarak cilalanmamış kurallar için geçici tutma yeridir.

Artık **Capability** ve **Namespace** içerikleri hakkında iyi bir genel bakışa ve anlayışa sahip olduğumuza göre, önceki görevlerdeki örnek sonucu açıklayabilmeliyiz. Öyleyse, sonuçlardan birini kullanarak hızlı bir tekrar yapalım, ne dersiniz?

Plaintext

```
Malware Behavior Catalogue
┌───────────────────────────────────────────┬───────────────────────────────────────────┐
│ Capability                                │ Namespace                                 │
├───────────────────────────────────────────┼───────────────────────────────────────────┤
│ reference Base64 string                   │ data-manipulation/encoding/base64         │
└───────────────────────────────────────────┴───────────────────────────────────────────┘
```

Yukarıdaki sonucun açıklaması şöyledir. Aşağıdaki tabloyu inceleyin.

|Etiket (Label)|Değer (Value)|Açıklama (Explanation)|
|---|---|---|
|**Capability**|**reference base64 string**|Kötü amaçlı yazılım, bir **base64** şeması kullanarak verileri kodlama yeteneğine sahiptir.|
|**Top-Level Namespace**|**data-manipulation**|Yürütülebilir dosyalar içindeki verilerin değiştirilmesini içeren davranışları düzenleyen bir dizi kural içerir. Bu yön, **String Encryption** ve **Data Encoding** gibi eylemleri kapsayan kötü amaçlı yazılım davranışının "veri dönüştürme" bileşeni olarak kabul edilebilir.|
|**Namespace**|**encoding/base64**|Bu ad alanı, **Base64** ve **XOR** kullanarak verileri kodlamak ve çözmek için kurallardan oluşur.|
|**Rule YAML File Matched?**|`reference-base64-string.yml`|Yeteneğin adının, boşluklar arasında ek bir tire (-) karakteri ile kuralın adı olduğunu unutmayın.|

bu bilgiyi bildiğinizde, bu dosyanın **base64** kodlama şemasını kullanabileceğini söyleyebilirsiniz!