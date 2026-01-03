---

### Müşteri Hedeflerini ve Kapsamını Belirleme

Operasyonlar oldukça karmaşık ve bürokratik olabilir. Başarılı bir operasyonun anahtarı, net bir şekilde tanımlanmış müşteri hedefleri veya amaçlarıdır. Müşteri hedefleri, hem müşterinin hem de **red team**'in beklentileri karşılıklı olarak anlaması için her iki taraf arasında tartışılmalıdır. Belirlenen hedefler, operasyonun geri kalan belgeleri ve planlaması için temel oluşturur.

Net ve somut hedefler ve beklentiler olmadan, çok plansız ve programsız bir operasyona hazırlanıyor olursunuz. Hedefler, operasyonun geri kalanı için tonu belirler.

Bir müşterinin hedeflerini değerlendirirken ve operasyon detaylarını planlarken, genellikle değerlendirmenin ne kadar odaklı olduğuna karar vermeniz gerekir.

Operasyonlar, genel bir dahili/ağ sızma testi veya odaklanmış bir **adversary emulation** (düşman taklidi) olarak kategorize edilebilir. Odaklanmış bir **adversary emulation**, bir operasyon içinde taklit edilecek belirli bir **APT** (Gelişmiş Kalıcı Tehdit) grubunu tanımlar. Bu genellikle, şirketin çalıştığı sektörü (örneğin, finans kurumları ve **APT38**) hedef alan gruplara göre belirlenir. Dahili veya ağ sızma testi de benzer bir yapıyı takip eder, ancak genellikle daha az odaklıdır ve daha standart **TTP**'leri kullanır. Yaklaşımın detayları, müşteri hedefleri tarafından tanımlanan operasyonun duruma göre değişir.

Müşteri hedefleri, operasyonun genel kurallarını ve kapsamını da etkileyecektir. Bu konulara Görev 6'da daha detaylı değinilecektir.

Müşteri hedefleri, yalnızca müşterinin operasyondan beklediği amaçların temel bir tanımını sunar. Spesifik operasyon planları, müşteri hedeflerini genişletecek ve operasyonun detaylarını belirleyecektir. Operasyon planları bu odada daha sonra ele alınacaktır.

Hassas ve şeffaf bir operasyonun bir sonraki temel taşı, iyi tanımlanmış bir **kapsamdır (scope)**. Bir operasyonun kapsamı, organizasyona ve altyapısının durumuna göre değişiklik gösterecektir. Bir müşterinin kapsamı, tipik olarak **yapamayacağınız** veya **hedefleyemeyeceğiniz** şeyleri tanımlar; ayrıca **yapabileceğiniz** veya **hedefleyebileceğiniz** şeyleri de içerebilir. Müşteri hedefleri, hizmeti sağlayan ekiple birlikte tartışılıp belirlenebilirken, bir kapsam yalnızca müşteri tarafından belirlenmelidir. Bazı durumlarda, **red team** bir operasyonu etkilemesi durumunda kapsamla ilgili bir şikayetini dile getirebilir. Müşterilerin, ağları ve bir değerlendirmenin olası sonuçları hakkında net bir anlayışa sahip olmaları gerekir.

Kapsamın ayrıntıları ve ifadesi her zaman farklı görünecektir, aşağıda bir müşterinin kapsam metninde olabilecek bir örnek verilmiştir:

- Veri sızdırmak yasaktır (**No exfiltration of data**).
    
- Üretim sunucuları yasak bölgedir (**Production servers are off-limits**).
    
- 10.0.3.8/18 kapsam dışındadır.
    
- 10.0.0.8/20 kapsam içindedir.
    
- Hiçbir koşulda sistemin kapalı kalmasına izin verilmez (**System downtime is not permitted**).
    
- **PII** (Kişisel Tanımlayıcı Bilgiler) sızdırmak yasaktır.
    

Bir **red team** perspektifinden bir müşterinin hedeflerini veya kapsamını analiz ederken, daha derin anlamı ve sonuçları anlamak esastır. Analiz yaparken, ekibinizin sorunlara/hedeflere nasıl yaklaşacağını her zaman dinamik bir şekilde anlamalısınız. Gerekirse, operasyon planlarınızı yalnızca müşteri hedefleri ve kapsamını okuyarak yazmaya başlamalısınız.





Aşağıda, güçlü bir güvenlik duruşuna sahip, olgun bir organizasyonun müşteri hedefleri için bir örnek yer almaktadır.

**Örnek 1 - Global Enterprises:**

### Hedefler:

1. Sistem yanlış yapılandırmalarını (**misconfigurations**) ve ağ zayıflıklarını belirlemek. Dış sistemlere odaklanmak.
    
2. **Endpoint Detection and Response (EDR)** sistemlerinin etkinliğini belirlemek.
    
3. Genel güvenlik duruşunu ve yanıt verme kabiliyetini değerlendirmek. **SIEM** ve tespit önlemleri.
    
4. İyileştirme (**Remediation**) çalışmalarını değerlendirmek.
    
5. **DMZ** ve dahili sunucuların segmentasyonunu (**segmentation**) test etmek.
    
6. Sistem kesintisi (**downtime**) ve süresine bağlı olarak beyaz kartların (**white cards**) kullanımına izin vermek.
    
7. Veri ifşası ve sızmasının (**data exfiltration**) etkisini değerlendirmek.
    

### Kapsam:

1. Sistem kesintisi hiçbir koşulda yasaktır. Her türlü **DDoS** veya **DoS** saldırısı yasaktır.
    
2. Zararlı yazılım kullanımı yasaktır; buna **ransomware** ve diğer varyasyonları dahildir.
    
3. **PII**'nin (Kişisel Tanımlayıcı Bilgiler) sızdırılması yasaktır. Keyfi veri sızdırma (arbitrary exfiltration data) kullanılabilir.
    
4. 10.0.4.0/22 içindeki sistemlere yönelik saldırılara izin verilir.
    
5. 10.0.12.0/22 içindeki sistemlere yönelik saldırılar yasaktır.
    
6. Bean Enterprises, **DMZ** ve kritik/üretim sistemleriyle olan etkileşimleri yakından izleyecektir.
    
7. "*.bethechange.xyz" ile olan her türlü etkileşim yasaktır.
    
8. "*.globalenterprises.thm" ile olan tüm etkileşimlere izin verilir.
    
