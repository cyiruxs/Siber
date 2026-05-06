# SOC Temelleri: Tespit ve Yanıt

SOC ekibinin temel odak noktası, **Detection** (Tespit) ve **Response** (Yanıt) süreçlerini eksiksiz sürdürmektir. SOC ekibi, bu hedefe ulaşmalarına yardımcı olan güvenlik çözümleri formunda bazı kaynaklara sahiptir. Bu çözümler, tüm şirketin ağını ve tüm sistemlerini tek bir merkezi konumdan izlemek için entegre eder. Herhangi bir güvenlik olayını tespit etmek ve yanıtlamak için sürekli izleme gereklidir.

## Detection (Tespit)

- **Zafiyetleri Tespit Etme (Detect vulnerabilities):** Bir **vulnerability** (zafiyet), bir saldırganın kendi izin seviyesinin ötesindeki işlemleri gerçekleştirmek için istismar edebileceği bir zayıflıktır. Bir zafiyet; sunucu veya bilgisayar gibi herhangi bir cihazın yazılımında (işletim sistemi ve programlar) keşfedilebilir. Örneğin SOC, belirli bir yayınlanmış zafiyete karşı yamalanması (patched) gereken bir dizi MS Windows bilgisayar keşfedebilir. Kesin konuşmak gerekirse, zafiyetler doğrudan SOC'un sorumluluğu olmayabilir; ancak giderilmeyen zafiyetler tüm şirketin güvenlik seviyesini etkiler.
    
- **Yetkisiz Faaliyetleri Tespit Etme (Detect unauthorized activity):** Bir saldırganın çalışanlardan birinin kullanıcı adı ve şifresini keşfettiği ve bunları şirket sistemine giriş yapmak için kullandığı durumu düşünün. Bu tür bir yetkisiz faaliyeti, herhangi bir hasara yol açmadan önce hızlıca tespit etmek kritik öneme sahiptir. Coğrafi konum gibi birçok ipucu, bunu tespit etmemize yardımcı olabilir.
    
- **Politika İhlallerini Tespit Etme (Detect policy violations):** Bir **security policy** (güvenlik politikası), bir şirketi güvenlik tehditlerine karşı korumaya yardımcı olmak ve uyumluluğu (compliance) sağlamak için oluşturulmuş bir dizi kural ve prosedürdür. Nelerin ihlal sayılacağı şirketten şirkete değişir; korsan medya dosyaları indirmek ve gizli şirket dosyalarını güvensiz bir şekilde göndermek bunlara örnektir.
    
- **Sızmaları Tespit Etme (Detect intrusions):** **Intrusions** (sızmalar), sistemlere ve ağlara yetkisiz erişimi ifade eder. Senaryolardan biri, bir saldırganın web uygulamamızı başarıyla istismar etmesi (exploiting) olabilir. Bir diğeri ise, bir kullanıcının kötü amaçlı bir siteyi ziyaret etmesi ve bilgisayarına virüs bulaşmasıdır.
    

## Response (Yanıt)

- **Olay Yanıtına Destek (Support with the incident response):** Bir olay (incident) tespit edildiğinde, buna yanıt vermek için belirli adımlar atılır. Bu yanıt, olayın etkisini en aza indirmeyi ve olayın kök neden analizini (**root cause analysis**) gerçekleştirmeyi içerir. SOC ekibi ayrıca olay yanıt ekibinin (**incident response team**) bu adımları gerçekleştirmesine yardımcı olur.
    

---

## SOC'un Üç Sütunu

Bir SOC'un üç sütunu vardır. Tüm bu sütunlarla birlikte bir SOC ekibi olgunlaşır ve farklı olayları verimli bir şekilde tespit edip yanıtlar. Bu sütunlar şunlardır: **People** (İnsan), **Process** (Süreç) ve **Technology** (Teknoloji).

**People**, **Process** ve **Technology** bir SOC ortamında bir arada bulunur. Uygun süreçlerin varlığında, son teknoloji güvenlik araçları üzerinde çalışan profesyonel bireylerden oluşan bir ekip, olgun bir SOC ortamını oluşturan şeydir.