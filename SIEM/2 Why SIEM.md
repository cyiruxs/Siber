## SIEM: Veri Selini Yönetmek ve Değerli Sonuçlar Çıkarmak

Peki, bu veri selini nasıl daha verimli yönetebilir ve değerli sonuçlar elde edebiliriz? İşte burada **SIEM** devreye girer. **Security Information and Event Management** (SIEM), çeşitli **log** kaynaklarından **log** toplayan, bunların formatlarını tutarlı bir hale getiren (**standardizes**), onları birbiriyle ilişkilendiren (**correlates**) ve tespit kurallarını (**detection rules**) kullanarak kötü amaçlı faaliyetleri tespit eden bir güvenlik çözümüdür.

### SIEM'in Özellikleri

Bir **SIEM** çözümü sadece önceki görevde tartıştığımız sorunları çözmekle kalmaz, aynı zamanda güvenlik operasyonlarını geliştirecek yetenekler de sağlar. Bir **SIEM**'in sunduğu temel özelliklerden bazılarını ele alalım:

#### Centralized Log Collection (Merkezi Log Toplama)

**SIEM**, tüm kaynaklardan (**endpoints**, sunucular, **firewalls** vb.) **log**'ları toplar ve tek bir yerde merkezileştirir. Bu **log**'lar, hafif aracılar (**lightweight agents**) veya **API**'ler aracılığıyla çekilir ve **SIEM** çözümüne aktarılır. Bu, her makineye **log**'larını analiz etmek için tek tek bağlanma sorununu çözer.

#### Normalization of Logs (Logların Normalizasyonu)

Ham **log**'lar (**raw logs**) farklı format ve boyutlardadır. Bir Windows **log**'u, bir **Linux log**'u ile aynı görünmez. Bir **SIEM** çözümü bu **log**'ları tek bir yerde merkezileştirdiği için, tüm **log**'ların farklı alanlara (**fields**) bölünmesini ve tutarlı bir formatta sunulmasını da sağlar. Bir **log**'un anlaşılmasını kolaylaştırmak için çeşitli alanlara bölünmesine **Parsing**, çeşitli **log** kaynaklarından gelen tüm **log**'ların tutarlı bir formata dönüştürülmesine ise **Normalization** denir.

#### Correlation of Logs (Logların İlişkilendirilmesi)

Münferit **log**'lar pek kullanışlı değildir. **SIEM**, farklı kaynaklardan gelen **log**'ları birbiriyle ilişkilendirir (**correlates**) ve aralarındaki ilişkiyi bulur. Bu, paternleri analiz ederek kötü amaçlı faaliyetlerin tanımlanmasına yardımcı olur. Örneğin, 5 dakikalık bir zaman diliminde bir sistemde gerçekleşen şu faaliyetlere göz atalım:

1. Haris, daha önce hiç kullanmadığı bir IP'den **VPN** üzerinden oturum açar.
    
2. Haris, paylaşılan bir sürücüdeki bazı belgelere erişir.
    
3. Haris, bir **PowerShell** betiği çalıştırır.
    
4. Sistem, dışarıya doğru bir ağ bağlantısı (**outbound network connection**) kurar.
    

Bireysel olarak değerlendirildiğinde bu faaliyetler normal görünebilir; ancak **SIEM** çözümü bu faaliyetleri birbiriyle ilişkilendirecek ve bu durum Haris'in ele geçirilmiş **VPN** kimlik bilgilerinden kaynaklanan potansiyel bir veri sızdırma (**data exfiltration**) faaliyetine işaret edebilecektir.

#### Real-time Alerting (Gerçek Zamanlı Uyarı)

**SIEM**, içerdiği kurallara dayanarak kötü amaçlı faaliyetleri tespit eder. Birçok kural **SIEM** ile varsayılan olarak gelir. Bununla birlikte analistler, gelecekteki tespitleri olgunlaştırmak için kendi gereksinimlerine göre yeni **detection rules** (tespit kuralları) oluştururlar. Bu tespit kurallarının koşulları sağlandığında **alert**'ler (uyarılar) tetiklenir ve analistler bilgilendirilir. Analistler daha sonra bu **alert**'leri **SIEM** platformu üzerinden inceleyebilirler.

#### Dashboards and Reporting (Paneller ve Raporlama)

**Dashboards** (paneller), her **SIEM**'in en önemli bileşenleridir. **SIEM**, verileri normalize edildikten ve sisteme aktarıldıktan (**ingested**) sonra analiz için sunar. Bu analizin özeti, birden fazla panel yardımıyla eyleme dönüştürülebilir içgörüler (**actionable insights**) şeklinde sunulur. Her **SIEM** çözümü bazı varsayılan panellerle gelir ve özel panel oluşturma seçeneği sunar. Bir panelde bulunabilecek bilgilerden bazıları şunlardır:

- **Alert Highlights** (Önemli Uyarılar)
    
- **System Notification** (Sistem Bildirimi)
    
- **Health Alert** (Sağlık Uyarısı)
    
- **List of Failed Login Attempts** (Başarısız Giriş Denemeleri Listesi)
    
- **Events Ingested Count** (İşlenen Olay Sayısı)
    
- **Rules triggered** (Tetiklenen Kurallar)
    
- **Top Domains Visited** (En Çok Ziyaret Edilen Alan Adları)
    

Aşağıda **Splunk SIEM**'de hazırlanmış bir panel örneği verilmiştir:

Bu odada ayrıntılı olarak ele almayacağımız çeşitli diğer **SIEM** özellikleri de mevcuttur. Bu özellikler arasında tehdit istihbaratı akışları (**threat intelligence feeds**) ile entegrasyon, kapsamlı veri tutma (**data retention**), güçlü arama yetenekleri ve diğerleri yer almaktadır. Bir sonraki görevde, **log**'larını inceleyerek farklı **log** kaynaklarını tartışacak ve bunların bir **SIEM** çözümüne nasıl aktarıldığını göreceğiz.