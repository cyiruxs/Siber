## Log Kaynakları ve Karşılaşılan Zorluklar

Bir ağdaki birden fazla cihaz birbiriyle ve çoğu zaman bir **router** (yönlendirici) aracılığıyla internetle iletişim kurar. Aşağıdaki görsel, birden fazla **Linux/Windows** tabanlı **Endpoint**, bir veri sunucusu ve bir web sitesinden oluşan basit bir ağ örneğini göstermektedir.

Bu cihazlar, içlerinde gerçekleşen faaliyetlere dair sürekli olarak **log** üretirler. Bu cihazlara **log source** (günlük kaynağı) da diyebiliriz. Ürettikleri **log**'lar, tüm faaliyetlerin bir izi (**trail**) işlevini görür ve kötü amaçlı faaliyetlerin tanımlanması veya genel sorun giderme (**troubleshooting**) için son derece yararlıdır. Bu **log** kaynakları temel olarak aşağıda tartışılan iki kategoriye ayrılır:

### 1) Host-Centric Log Sources (Ana Bilgisayar Odaklı Log Kaynakları)

Bu **log** kaynakları, **host** içinde gerçekleşen veya **host** ile ilgili olayları yakalar. **Host-centric log** üreten cihazlar arasında Windows, **Linux**, sunucular vb. bulunur. Bazı **host-centric log** örnekleri şunlardır:

- Bir kullanıcının bir dosyaya erişmesi.
    
- Bir kullanıcının kimlik doğrulama (**authenticate**) girişimi.
    
- Bir **process execution** (işlem yürütme) faaliyeti.
    
- Bir işlemin bir **registry key** (kayıt defteri anahtarı) veya değeri eklemesi/düzenlemesi/silmesi.
    
- **PowerShell** yürütme işlemi.
    

### 2) Network-Centric Log Sources (Ağ Odaklı Log Kaynakları)

Ağ ile ilgili **log**'lar, **host**'lar birbiriyle iletişim kurduğunda veya bir web sitesini ziyaret etmek için internete eriştiğinde oluşturulur. **Network-centric log** üreten cihazlar; **firewall**'lar (güvenlik duvarları), **IDS/IPS**, **router**'lar vb. cihazlardır. Bazı **network-centric log** örnekleri şunlardır:

- **SSH** bağlantısı.
    
- **FTP** üzerinden erişilen bir dosya.
    
- Web trafiği.
    
- Bir kullanıcının şirket kaynaklarına **VPN** üzerinden erişmesi.
    
- Ağ dosyası paylaşım faaliyeti (**Network file sharing**).
    

Birlikte, bu **host-centric** ve **network-centric log** kaynakları, bir ağda sürekli olarak sayısız **log** oluşturur.

---

## Log Analizindeki Zorluklar

Şu ana kadar, bu **log** kaynaklarının **log** ürettiği, bizim de bunları analiz edip kötü amaçlı faaliyetleri belirlediğimiz oldukça basit bir süreç gibi görünebilir. Ancak bu o kadar kolay değildir ve bazı zorlukları vardır:

- **Sayıca Fazla Log Kaynağı:** Bir ağda, saniyede yüzlerce olay üreten çok sayıda **log source** vardır. Bu **log**'lar farklı cihazlara dağılmıştır ve bir **incident** durumunda her cihazdaki **log**'ları tek tek incelemek yorucu olabilir.
    
- **Merkezi Olmama (No Centralization):** **Log**'lar üretildikleri makinelerde tutulduğu için, birden fazla kaynaktan gelen **log**'ları analiz etmek amacıyla her bir kaynağa **SSH**, **RDP** vb. ile bağlanmanız gerekebilir. Bu çok verimsizdir ve incelemeler sırasında değerli zamanınızın boşa harcanmasına neden olabilir.
    
- **Sınırlı Bağlam (Limited Context):** Münferit **log**'lar bir faaliyetin hikayesinin tamamını anlatamaz. Bir **incident** sırasında, farklı **log** kaynaklarındaki bireysel faaliyetler zararsız görünebilir. Ancak bu **log**'lar birbiriyle ilişkilendirilirse (**correlated**), bambaşka bir hikaye ortaya çıkarabilir. Örneğin, bir sistemde genel olarak normal bir faaliyet olan bir dosya erişim olayı gözlemlediniz. Ancak farklı **log** kaynaklarını ilişkilendirirseniz, bu dosyaya erişen kullanıcının, ağdaki başka bir makineyi ele geçirdikten sonra **lateral movement** (yanal hareket) yoluyla bu makineye eriştiğini öğrenebilirsiniz.
    
- **Sınırlı Analiz Kapasitesi:** **Log** kaynakları saniyede sayısız **log** üretir ve anormal faaliyetleri belirlemek için tüm cihazlardan gelen tüm **log**'ları manuel olarak analiz etmek insanlar için neredeyse imkansızdır. Gerçekçi olmak gerekirse, analistler devasa sayıdaki **log** arasında birçok önemli kaydı gözden kaçıracaktır.
    
- **Format Sorunları:** Farklı **log** kaynakları çeşitli formatlarda **log** üretir. Analistlerin bunları analiz edebilmek için tüm bu formatları bilmesi gerekir; bu da özellikle bir ağdaki çok sayıda kaynakla uğraşırken son derece zor olabilir.