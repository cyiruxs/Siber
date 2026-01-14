Analog" dünyada, bir banka hesabı açarken veya kütüphaneye üye olurken belgeleri imzalamanız istenir. Bu imza, şartları kabul ettiğinizi onaylar veya bir işlemi yetkilendirir. Dijital dünyada ise kalemle atılan imzanın yerini **Digital Signature** (Dijital İmza) alır.

---

## Dijital İmza Nedir?

Dijital imzalar, bir dijital mesajın veya belgenin **kimliğini (authenticity)** ve **bütünlüğünü (integrity)** doğrulamak için kullanılır.

- **Kimlik Doğrulama:** Dosyayı kimin oluşturduğunu veya değiştirdiğini bilmemizi sağlar.
    
- **Bütünlük:** Dosyanın iletim sırasında değiştirilmediğini kanıtlar.
    

Asimetrik kriptografi kullanılarak, imzanızı **private key** (özel anahtar) ile oluşturursunuz; bu imza herkesin erişebildiği **public key** (açık anahtar) ile doğrulanır. Sadece sizde bulunan private key ile atılan bu imza, yasal olarak birçok ülkede ıslak imza ile aynı değere sahiptir.

### Dijital İmza Nasıl Çalışır?

En güvenli yöntem, belgenin bir **hash** (özet) değerini alıp bu özeti private key ile şifrelemektir. Süreç şu şekilde işler:

1. **Bob**, belgenin hash değerini hesaplar ve bunu kendi private key'i ile şifreler (imzalar).
    
2. Orijinal belgeyi ve bu imzalı hash'i **Alice**'e gönderir.
    
3. **Alice**, Bob'un public key'ini kullanarak imzalı hash'i çözer.
    
4. Alice, aldığı belgenin kendi tarafında hash'ini hesaplar.
    
5. Eğer Alice'in hesapladığı hash ile çözülen hash birbirine uyuyorsa, belge hem Bob'dan gelmiştir hem de yolda değişmemiştir.
    

---

## Sertifikalar: Kim Olduğunuzu Kanıtlayın!

Sertifikalar, açık anahtar kriptografisinin ve dijital imzaların en önemli uygulama alanlarından biridir. En yaygın kullanımı **HTTPS** protokolüdür.

Tarayıcınızın, bağlandığınız sunucunun gerçekten `tryhackme.com` olduğunu nasıl anladığını merak ettiniz mi? Cevap **Sertifikalar**da gizlidir.

### Güven Zinciri (Chain of Trust)

Sertifikalar, bir **CA** (Certificate Authority - Sertifika Makamı) ile başlayan bir güven zincirine dayanır.

- Cihazınız ve tarayıcınız, yüklendiği andan itibaren belirli kök (root) CA'lara otomatik olarak güvenir.
    
- Bir web sitesinin sertifikası bir kuruluş tarafından imzalanır, o kuruluş bir CA tarafından onaylanır ve o CA tarayıcınız tarafından güvenilirdir. Bu sayede tarayıcınız o web sitesine güvenir.
    

### Kendi Sertifikanızı Almak

Eğer bir web siteniz varsa ve HTTPS kullanmak istiyorsanız bir **TLS sertifikasına** ihtiyacınız vardır:

- Yıllık bir ücret karşılığında çeşitli sertifika makamlarından satın alabilirsiniz.
    
- **Let's Encrypt** gibi servisleri kullanarak, sahip olduğunuz alan adları için ücretsiz olarak TLS sertifikası alabilirsiniz.