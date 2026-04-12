Özünde **Burp Suite**, web uygulaması sızma testi (penetration testing) gerçekleştirmek için kapsamlı bir çözüm sunmak üzere tasarlanmış, Java tabanlı bir framework'tür. Uygulama programlama arayüzlerine (**API**'ler) dayananlar da dahil olmak üzere, web ve mobil uygulamaların uygulamalı güvenlik değerlendirmeleri için endüstri standardı araç haline gelmiştir.

Basitçe ifade etmek gerekirse **Burp Suite**, bir tarayıcı ile bir web sunucusu arasındaki tüm **HTTP/HTTPS** trafiğini yakalar ve manipüle edilmesine olanak tanır. Bu temel yetenek, framework'ün bel kemiğini oluşturur. İstekleri (**requests**) intercept ederek (yolu kesilerek), kullanıcılar bunları ilerleyen bölümlerde inceleyeceğimiz Burp Suite framework'ü içindeki çeşitli bileşenlere yönlendirme esnekliğine sahip olurlar. Web isteklerini hedef sunucuya ulaşmadan önce durdurma (intercept), görüntüleme ve değiştirme veya hatta tarayıcımız tarafından alınmadan önce yanıtları (**responses**) manipüle etme yeteneği, Burp Suite'i manuel web uygulaması testleri için paha biçilemez bir araç haline getirir.

⚠️ **Burp Suite** farklı sürümlerde mevcuttur. Bizim amaçlarımız doğrultusunda, yasal sınırlar dahilinde ticari olmayan kullanım için ücretsiz olarak erişilebilen **Burp Suite Community Edition**'a odaklanacağız. Bununla birlikte, Burp Suite'in gelişmiş özelliklerle birlikte gelen ve lisans gerektiren Professional ve Enterprise sürümlerini de sunduğunu belirtmekte fayda var:

**Burp Suite Professional**, Burp Suite Community'nin kısıtlanmamış bir versiyonudur. Aşağıdaki gibi özelliklerle birlikte gelir:

- Otomatik bir zafiyet tarayıcısı (**vulnerability scanner**).
    
- Hız sınırlaması (**rate limit**) olmayan bir fuzzer/brute-forcer.
    
- Gelecekteki kullanımlar için projeleri kaydetme ve rapor oluşturma.
    
- Diğer araçlarla entegrasyona izin veren yerleşik bir **API**.
    
- Daha fazla işlevsellik için yeni uzantılar (**extensions**) eklemeye yönelik sınırsız erişim.
    
- **Burp Suite Collaborator**'a erişim (etkili bir şekilde kendi kendine barındırılan veya Portswigger'a ait bir sunucuda çalışan benzersiz bir istek yakalayıcı sağlar).
    

Kısacası, Burp Suite Professional oldukça güçlü bir araçtır ve bu da onu alandaki profesyoneller için tercih edilen bir seçenek haline getirir.

**Burp Suite Enterprise**, Community ve Professional sürümlerinin aksine, öncelikle sürekli tarama (**continuous scanning**) için kullanılır. Tıpkı Nessus gibi araçların otomatik altyapı taraması gerçekleştirmesine benzer şekilde, web uygulamalarını periyodik olarak güvenlik açıkları için tarayan otomatik bir tarayıcıya sahiptir. Yerel bir makineden manuel saldırılara izin veren diğer sürümlerin aksine, Burp Suite Enterprise bir sunucuda bulunur ve hedef web uygulamalarını potansiyel güvenlik açıkları için sürekli olarak tarar.

Professional ve Enterprise sürümleri için lisans gerektirdiğinden, **Burp Suite Community Edition** tarafından sağlanan temel özellik setine odaklanacağız.