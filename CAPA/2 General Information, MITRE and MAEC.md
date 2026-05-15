## Dosya Bilgileri Bloğu

Raporun ilk bloğu dosya hakkında temel teknik detayları sunar:

- **Kriptografik Algoritmalar:** Dosyanın bütünlüğünü ve kimliğini doğrulamak için kullanılan **md5**, **sha1** ve **sha256** özet değerleri.
    
- **Analysis:** CAPA'nın analizi nasıl gerçekleştirdiğini belirtir (örneğin; **static**).
    
- **OS:** Tanımlanan yeteneklerin hangi işletim sistemi bağlamında geçerli olduğunu gösterir (örneğin; **windows**).
    
- **Format:** Dosyanın biçimi (örneğin; **pe** - Portable Executable).
    
- **Arch:** Dosyanın hangi mimari ile ilişkili olduğunu belirtir (örneğin; **i386** - x86 mimarisi).
    
- **Path:** Analiz edilen dosyanın bulunduğu dizin yolu.
    

---

## MITRE ATT&CK

**MITRE ATT&CK**, siber saldırganların bir saldırının her aşamasında kullandıkları taktik ve teknikleri belgeleyen küresel bir bilgi deposudur. CAPA, çıktılarını bu formatta sunarak analistlerin dosya davranışlarını saldırganların "oyun planı" ile eşleştirmesine yardımcı olur.

### Çıktı Formatı ve Örnekler

|**Format**|**Örnek**|**Açıklama**|
|---|---|---|
|Tactic::Technique::ID|**DEFENSE EVASION**::Obfuscated Files or Information::**T1027**|**Tactic:** Savunma Atlatma<br><br>  <br><br>**Technique:** Gizlenmiş Dosyalar veya Bilgiler<br><br>  <br><br>**ID:** T1027|
|Tactic::Technique::Sub-Technique::ID|**DEFENSE EVASION**::Obfuscated Files::Indicator Removal from Tools::**T1027.005**|**Sub-Technique:** Araçlardan Gösterge Kaldırma<br><br>  <br><br>**Sub-ID:** 005|

---

## MAEC (Malware Attribute Enumeration and Characterization)

**MAEC**, kötü amaçlı yazılımların karmaşık ayrıntılarını (davranışlar, yapıtlar ve bağlantılar) kodlamak ve iletmek için tasarlanmış özel bir dildir. CAPA tarafından en sık kullanılan iki ana **MAEC** değeri şunlardır:

### MAEC Kategorileri ve Değerleri

|**MAEC Değeri**|**Açıklama**|**Gösterdiği Davranışlar (Örnek)**|
|---|---|---|
|**Launcher**|Malign davranışlara benzer eylemleri tetikleyen davranışlar sergiler.|Ek yüklerin (**payload**) bırakılması, kalıcılık (**persistence**) mekanizmalarının etkinleştirilmesi, C2 sunucularına bağlanma.|
|**Downloader**|Diğer dosyaları indiren ve yürüten davranışlar sergiler.|İnternetten ek kaynaklar çekme, güncellemeleri alma, ikincil aşamaları (**secondary stages**) yürütme.|