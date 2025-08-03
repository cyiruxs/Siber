### Güvenlik Değerlendirmesi Türleri: Notlar için Özet

#### 1. Zafiyet Değerlendirmeleri (Vulnerability Assessments)

- **Amaç:** Mümkün olduğu kadar çok sistemde, mümkün olduğu kadar çok **güvenlik açığını (vulnerability)** tespit etmek.
    
- **Odak:** Ağdaki her bir **host'u (sunucuyu veya bilgisayarı)** tek bir birim olarak taramak ve güvenlik açıklarını bulmak.
    
- **Süreç:** Çoğunlukla otomatik araçlarla yapılır. Bu yüzden çok fazla teknik bilgi gerektirmez. Saldırganın makinesi güvenlik çözümleri tarafından **allowlist'e (beyaz listeye)** alınabilir, böylece tarama engellenmez.
    
- **Ne Yapılmaz:** Bulunan zafiyetleri **istismar etmeye (exploit)** çalışılmaz. Sadece zafiyetler **tanımlanır**.
    
- **Sonuç:** Şirkete, güvenlik açıklarını düzeltme (remediation) çabalarını nerede yoğunlaştırması gerektiği konusunda bilgi sağlar.
    

---

#### 2. Sızma Testleri (Penetration Tests)

- **Amaç:** Zafiyet değerlendirmesinin üzerine ek olarak, bulunan zafiyetlerin ağın tamamını nasıl etkilediğini anlamak.
    
- **Odak:** Ağdaki her bir host'u tek tek taramanın yanı sıra, zafiyetleri **istismar etmeye** ve bir sistemden diğerine **pivot yapmaya** çalışmak.
    
- **Süreç:**
    
    - Önce zafiyet taraması yapılır.
        
    - Bulunan zafiyetleri **istismar etmeye (exploit)** çalışılır. Bu sayede, güvenlik açıkları olsa bile mevcut diğer güvenlik kontrollerinin (compensatory controls) bu açığı kapatıp kapatmadığı test edilir.
        
    - Ele geçirilen (compromised) bir host'ta **post-exploitation** görevleri yapılır (örneğin, hassas bilgi arama).
        
- **Ne Yapılmaz (Kısmi olarak):** Genellikle çok gürültülü (loud) çalışırlar ve fark edilmeye çok önem vermezler. Zaman kısıtlamaları nedeniyle **IDS/IPS** gibi güvenlik önlemlerini atlatmaya çalışmak yerine, bazen bu güvenlik mekanizmaları devre dışı bırakılabilir. Sosyal mühendislik gibi teknik olmayan saldırı vektörleri genellikle test edilmez.
    
- **Sonuç:** Bir saldırganın ağdaki zafiyetleri nasıl zincirleyebileceği (chaining vulnerabilities) ve belirli hedeflere nasıl ulaşabileceği hakkında daha derin bir bilgi sunar.
    

---

#### 3. Gelişmiş Kalıcı Tehditler ve Neden Normal Pentesting Yeterli Değil? (Advanced Persistent Threats - APTs)

- **Sorun:** Geleneksel sızma testleri, gerçek bir saldırının bazı önemli yönlerini göz ardı eder:
    
    - **Gürültü:** Sızma testi uzmanları fark edilmemek için uğraşmazken, gerçek saldırganlar **gizli kalmaya** çalışır.
        
    - **Teknik Olmayan Vektörler:** Sosyal mühendislik veya fiziksel saldırılar gibi yöntemler genellikle sızma testlerinin dışında kalır.
        
    - **Güvenlik Mekanizmalarını Gevşetme:** Sızma testlerinde verimlilik için bazı güvenlik önlemleri geçici olarak kapatılabilir, ancak gerçek bir saldırıda bu söz konusu değildir.
        
- **Tanım:** **APTs (Gelişmiş Kalıcı Tehditler)**, genellikle devletler veya organize suç grupları tarafından desteklenen, yüksek becerilere sahip saldırgan gruplarıdır. Amaçları kritik altyapı, finans veya hükümet kurumlarıdır. "Kalıcı" denilmesinin sebebi, ele geçirdikleri ağlarda **uzun süreler boyunca fark edilmeden** kalabilmeleridir.
    
- **Çözüm:** Bu sınırlılıklar nedeniyle, gerçekçi bir güvenlik değerlendirmesi sunmak için **Kırmızı Takım (Red Team) testleri** ortaya çıkmıştır. Bu testler, bir APT'ye karşı şirketin ne kadar hazırlıklı olduğunu anlamayı hedefler.
    