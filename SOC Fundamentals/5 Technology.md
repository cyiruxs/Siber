Doğru **People** (İnsan) ve **Processes** (Süreçler) yapısına sahip olmak, tespit ve yanıt için güvenlik çözümleri olmadan asla yeterli olmayacaktır. **SOC** sütunlarındaki **Technology** (Teknoloji) kısmı, güvenlik çözümlerini ifade eder. Bu güvenlik çözümleri, **SOC** ekibinin tehditleri tespit etme ve yanıtlama konusundaki manuel çabasını verimli bir şekilde en aza indirir.

Bir kurumun ağı birçok cihaz ve uygulamadan oluşur. Bir güvenlik ekibi olarak, her bir cihaz veya uygulamadaki tehditleri bireysel olarak tespit etmek ve yanıtlamak, önemli ölçüde çaba ve kaynak gerektirecektir. Güvenlik çözümleri, ağda bulunan cihazların veya uygulamaların tüm bilgilerini merkezileştirir ve tespit ile yanıt yeteneklerini otomatikleştirir.

Gelin bu güvenlik çözümlerinden bazılarını kısaca anlayalım:

---

### Güvenlik Teknolojileri

- **SIEM:** **Security Information and Event Management** (SIEM), hemen hemen her **SOC** ortamında kullanılan popüler bir araçtır. Bu araç, **log sources** (günlük kaynakları) olarak adlandırılan çeşitli ağ cihazlarından günlükleri (**logs**) toplar. Şüpheli faaliyetleri tanımlamak için mantık içeren **Detection rules** (tespit kuralları) **SIEM** çözümünde yapılandırılır. **SIEM** çözümü, bunları birden fazla günlük kaynağıyla ilişkilendirdikten (**correlating**) sonra bize tespitleri sağlar ve kurallardan herhangi biriyle eşleşme olması durumunda bizi uyarır. Modern **SIEM** çözümleri, bu kural tabanlı tespit analizinin ötesine geçerek bize **user behavior analytics** (kullanıcı davranışı analitiği) ve **threat intelligence** (tehdit istihbaratı) yeteneği sağlar. Makine öğrenimi (**Machine learning**) algoritmaları, tespit yeteneklerini geliştirmek için bunu destekler.
    - > **SIEM** çözümü, bir **SOC** ortamında yalnızca **Detection** (Tespit) yetenekleri sağlar.
        
- **EDR:** **Endpoint Detection and Response** (EDR), **SOC** ekibine cihazların faaliyetlerine ilişkin ayrıntılı gerçek zamanlı ve geçmişe dönük görünürlük sağlar. Uç nokta (**endpoint**) düzeyinde çalışır ve otomatik yanıtlar gerçekleştirebilir. **EDR**, uç noktalar için kapsamlı tespit yeteneklerine sahiptir, bu da onları ayrıntılı olarak incelemenize ve birkaç tıklamayla yanıt vermenize olanak tanır.
    
- **Firewall:** Bir **firewall** (güvenlik duvarı), tamamen ağ güvenliği için işlev görür ve dahili ile harici ağlarınız (İnternet gibi) arasında bir bariyer görevi görür. Gelen ve giden ağ trafiğini izler ve yetkisiz her türlü trafiği filtreler. **Firewall** ayrıca, şüpheli trafiği dahili ağa ulaşmadan önce tanımlamamıza ve engellememize yardımcı olan bazı konuşlandırılmış tespit kurallarına sahiptir.
    

---

### Diğer Çözümler ve Seçim Süreci

**SOC** ortamında **Antivirus**, **EPP**, **IDS/IPS**, **XDR**, **SOAR** ve daha fazlası gibi çeşitli diğer güvenlik çözümleri de benzersiz roller oynar. **SOC**'da hangi **Technology**'nin (Teknoloji) devreye alınacağına dair karar, tehdit yüzeyi (**threat surface**) ve kurumdaki mevcut kaynakların dikkatli bir şekilde değerlendirilmesinden sonra verilir.

---

> [!TIP] Teknoloji, insan uzmanlığı ve tanımlanmış süreçlerle birleştiğinde operasyonel mükemmelliğe ulaşılır.