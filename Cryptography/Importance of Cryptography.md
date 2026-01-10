Kriptografinin temel amacı, saldırganların (adversaries) bulunduğu bir ortamda **güvenli iletişimi** sağlamaktır. "Güvenli" terimi, iletilen verinin hem gizliliğini hem de bütünlüğünü kapsar. Kriptografi; üçüncü tarafların veya saldırganların mesaj içeriklerini ifşa edememesi veya değiştirememesi için geliştirilen tekniklerin uygulanması ve incelenmesi olarak tanımlanabilir.

---

## Kriptografinin Temel Amaçları

Kriptografi; **gizlilik (confidentiality)**, **bütünlük (integrity)** ve **kimlik doğrulama (authenticity)** kavramlarını korumak için kullanılır. Günümüzde kriptografiyi farkında olmadan her gün kullanıyoruz:

- **Web Girişleri:** TryHackMe gibi platformlara giriş yaparken, kimlik bilgileriniz şifrelenerek sunucuya gönderilir; böylece bağlantınızı izleyen biri bilgilerinizi ele geçiremez.
    
- **SSH Bağlantıları:** SSH üzerinden bir sunucuya bağlandığınızda, istemci ve sunucu arasında şifreli bir tünel kurulur.
    
- **Online Bankacılık:** Tarayıcınız, bankanızın sunucu sertifikasını kontrol ederek bir saldırganla değil, gerçek banka sunucusuyla iletişim kurduğunuzu teyit eder.
    
- **Dosya Bütünlüğü:** Bir dosya indirdiğinizde, dosyanın orijinaliyle aynı olup olmadığını doğrulamak için **hash fonksiyonları** kullanılır.
    

---

## Yasal Düzenlemeler ve Standartlar

Kriptografi sadece teknik bir tercih değil, çoğu sektörde yasal bir zorunluluktur. Dijital dünyada verilerin korunması için belirli standartlara uyulması gerekir:

### PCI DSS (Ödeme Kartı Sektörü Veri Güvenliği Standardı)

Kredi kartı bilgilerini işleyen firmalar bu standarda uymak zorundadır. **PCI DSS**, verilerin hem depolanırken (**at rest**) hem de iletilirken (**in motion**) şifrelenmesini şart koşar.

### Sağlık Verileri ve Bölgesel Düzenlemeler

Tıbbi kayıtların korunması için gereken standartlar ülkeden ülkeye değişiklik gösterir:

- **ABD:** HIPAA ve HITECH.
    
- **Avrupa Birliği:** GDPR (General Data Protection Regulation).
    
- **Birleşik Krallık:** DPA (Data Protection Act).
    

Bu yasalar ve düzenlemeler, kriptografinin dijital altyapının vazgeçilmez bir parçası olduğunu ve genellikle kullanıcıdan gizli bir şekilde arka planda çalışması gerektiğini göstermektedir.