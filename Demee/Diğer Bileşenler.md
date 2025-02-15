### **Yük Dengeleyiciler (Load Balancers)**

Bir web sitesi **yüksek trafik almaya başladığında** veya **yüksek erişilebilirlik gerektiren bir uygulama çalıştırdığında**, **tek bir web sunucusu yeterli olmayabilir**. Bu noktada **yük dengeleyiciler (Load Balancers)** devreye girer.

Yük dengeleyiciler iki ana işlevi yerine getirir:

1. **Yüksek trafikli web sitelerinin talepleri karşılamasını sağlamak**
2. **Bir sunucu yanıt vermez hale gelirse, diğer sunuculara yönlendirme yaparak kesintisiz hizmet sunmak**

**Yük Dengeleyici Nasıl Çalışır?**  
Bir kullanıcı, yük dengeleyiciye sahip bir web sitesine istek gönderdiğinde:

- **Önce yük dengeleyici isteği alır** ve
- **İsteği, arkasındaki uygun sunuculardan birine yönlendirir**

Yük dengeleyiciler, isteğin hangi sunucuya gideceğini belirlemek için farklı **algoritmalar** kullanır:

- **Round-Robin** → Gelen istekleri sırayla sunuculara dağıtır.
- **Ağırlıklı (Weighted)** → Sunucuların mevcut yüküne göre en az yoğun olana yönlendirir.

Ayrıca, yük dengeleyiciler **belirli aralıklarla sunucuları kontrol eder** (**health check**). Eğer bir sunucu **yanıt vermezse**, yük dengeleyici o sunucuya istek göndermeyi durdurur ve **diğer sunucuları kullanmaya devam eder**.
![[Pasted image 20250215021310.png]]
---

### **CDN (İçerik Dağıtım Ağları - Content Delivery Networks)**

Bir **CDN (Content Delivery Network)**, **aşırı trafiği azaltmak** ve **içerik dağıtımını hızlandırmak** için kullanılan bir sistemdir.

CDN'ler, **statik dosyaları (JavaScript, CSS, resimler, videolar vb.) dünyanın farklı noktalarındaki sunucularda saklar**. Bir kullanıcı, bu dosyalardan birini talep ettiğinde:

- CDN **en yakın fiziksel sunucuyu belirler** ve
- **İçeriği, kullanıcının bulunduğu yere en yakın sunucudan sunar**

Bu sayede **yüksek hız sağlanır** ve **ana web sunucusunun yükü azalır**.

---

### **Veritabanları (Databases)**

Birçok web sitesi, **kullanıcı bilgilerini saklamak ve geri çağırmak** için **veritabanlarına** ihtiyaç duyar.

Web sunucuları, verileri kaydetmek veya almak için **veritabanlarıyla iletişim kurar**. Veritabanları, **basit bir metin dosyasından**, **birden fazla sunucudan oluşan karmaşık kümelere** kadar değişebilir.

**Yaygın Veritabanı Türleri:**

- **MySQL**
- **MSSQL**
- **MongoDB**
- **PostgreSQL**

Her biri farklı özelliklere ve kullanım senaryolarına sahiptir.

---

### **WAF (Web Uygulama Güvenlik Duvarı - Web Application Firewall)**

Bir **WAF**, **web isteği ile web sunucusu arasına yerleştirilen bir güvenlik katmanıdır**. Temel amacı:

- **Web sunucusunu saldırılara ve hizmet reddi (DDoS) saldırılarına karşı korumak**
- **Gelen istekleri analiz ederek botlar yerine gerçek tarayıcılardan geldiğini doğrulamak**

Ayrıca, **aşırı istek gönderimini sınırlayan ("Rate Limiting")** mekanizmaları kullanarak belirli bir IP'den gelen istekleri saniyede belirli bir sayıda sınırlandırır.

Eğer bir istek **potansiyel bir saldırı olarak değerlendirilirse**, WAF **bu isteği engeller ve sunucuya iletilmesini önler**.
![[Pasted image 20250215021206.png]]