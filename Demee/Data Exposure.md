### **Hassas Veri Açığı (Sensitive Data Exposure) Nedir?**

**Hassas veri açığı**, bir web sitesinin **gizli bilgileri yeterince koruyamaması veya temizlememesi** durumunda ortaya çıkar. Bu bilgiler genellikle **sitelerin ön yüz (frontend) kaynak kodunda** bulunabilir.

### **Web Sitelerindeki Açık Veri Tehlikesi**

Web sitelerinin **kaynak kodları (HTML, JavaScript)** incelendiğinde, geliştiricinin **unutmuş olabileceği hassas bilgiler** ortaya çıkabilir. Bunlar şunlar olabilir:

- **Gömülü giriş bilgileri (kullanıcı adı, şifre)**
- **Özel bölümlere giden gizli bağlantılar**
- **API anahtarları veya diğer hassas erişim bilgileri**


![[html_source.png]]
### **Hassas Verilerin Kullanılması ve Güvenlik Riskleri**

Bir saldırgan, bu bilgileri kullanarak **web uygulamasında daha fazla erişim sağlayabilir**. Örneğin:

- HTML yorumları içinde **geçici giriş bilgileri** bulunabilir.
- Kaynak kodda saklı bir bağlantı ile, **özel veya yönetici panellerine doğrudan erişim sağlanabilir**.

Eğer bir saldırgan bu bilgileri ele geçirirse, **uygulamanın diğer bileşenlerine veya arka uç sistemlerine (backend) erişim sağlayabilir**.

### **Web Uygulaması Güvenlik Testi Yaparken İlk Adım**

Bir web uygulamasının güvenliğini test ederken **ilk yapılması gerekenlerden biri, sayfanın kaynak kodunu incelemektir**. Bunu yapmak için:

- **Chrome:** Sayfada sağ tıklayıp **"View Page Source"** seçeneğine tıklayın.
- **Safari:** Sağ tıklayıp **"Show Page Source"** seçeneğine tıklayın.

**Özellikle giriş bilgileri veya gizli bağlantılar olup olmadığını kontrol edin!**