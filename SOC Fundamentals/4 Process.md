SOC ekibinde çalışan farklı bireylerin rollerini ve sorumluluklarını tartıştık. Her rolün, tıpkı Level 1 SOC Analistlerinin alert triage (uyarı önceliklendirme) gerçekleştirmek ve zararlı olup olmadığını belirlemek için ilk müdahale ekipleri (first responders) olarak gördüğümüz rolü gibi, kendine özgü  süreçleri (**Processes**) vardır. Şimdi bir SOC'da yer alan bazı önemli süreçleri tartışalım.

### Alert Triage (Uyarı Önceliklendirme)

**Alert triage**, SOC ekibinin temelidir. Herhangi bir uyarıya verilen ilk yanıt, triage işlemini gerçekleştirmektir. Triage, belirli bir uyarının analiz edilmesine odaklanır. Bu, uyarının ciddiyetini (**severity**) belirler ve onu önceliklendirmemize yardımcı olur. Alert triage, tamamen 5N (5 Ws) sorularını yanıtlamakla ilgilidir. Bu 5N (5 Ws) nedir?

Aşağıda, bir uyarının triage işlemi sırasında yanıtlanması gereken bazı sorular yer almaktadır.

**Alert:** Malware detected on Host: GEORGE PC

|5 Ws (5N)|Answers (Yanıtlar)|
|---|---|
|**What? (Ne?)**|Kurum ağı içindeki hostlardan birinde kötü amaçlı bir dosya tespit edildi.|
|**When? (Ne Zaman?)**|Dosya 5 Haziran 2024 tarihinde saat 13:20'de tespit edildi.|
|**Where? (Nerede?)**|Dosya "GEORGE PC" isimli hostun dizininde tespit edildi.|
|**Who? (Kim?)**|Dosya, kullanıcı George için tespit edildi.|
|**Why? (Neden?)**|İnceleme sonucunda, dosyanın korsan yazılım satan bir web sitesinden indirildiği anlaşıldı. Kullanıcıyla yapılan görüşme, bir yazılımı ücretsiz kullanmak istedikleri için dosyayı indirdiklerini ortaya çıkardı.|

---

### Reporting (Raporlama)

Tespit edilen zararlı uyarıların, zamanında yanıt verilmesi ve çözüme kavuşturulması için üst düzey analistlere eskale edilmesi (**escalated**) gerekir. Bu uyarılar **tickets** (destek kayıtları) olarak eskale edilir ve ilgili kişilere atanır. Rapor, derinlemesine bir analizle birlikte tüm 5N (5 Ws) sorularını ele almalı ve faaliyetin kanıtı olarak ekran görüntüleri kullanılmalıdır.

---

### Incident Response and Forensics (Olay Yanıtı ve Adli Bilişim)

Bazen rapor edilen tespitler, kritik düzeyde yüksek derecede kötü niyetli faaliyetlere işaret eder. Bu senaryolarda, üst düzey ekipler bir **incident response** (olay yanıtı) süreci başlatır. Olay yanıtı süreci, **Incident Response** odasında ayrıntılı olarak tartışılmaktadır. Birkaç kez, ayrıntılı bir **forensics** (adli bilişim) faaliyetinin de gerçekleştirilmesi gerekebilir. Bu adli bilişim faaliyeti, bir sistemden veya ağdan gelen kalıntıları (**artifacts**) analiz ederek olayın kök nedenini (**root cause**) belirlemeyi amaçlar.

---

> [!TIP] Bu süreçler, SOC operasyonlarının sürdürülebilirliği ve güvenliğin proaktif olarak sağlanması için birbirini tamamlayan kritik aşamalardır.