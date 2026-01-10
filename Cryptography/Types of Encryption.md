Modern şifreleme yöntemleri temel olarak iki ana kategoriye ayrılır: **Symmetric** (Simetrik) ve **Asymmetric** (Asimetrik).

---

## Symmetric Encryption (Simetrik Şifreleme)

Simetrik şifrelemede, veriyi şifrelemek ve deşifre etmek için **aynı anahtar** kullanılır. Bu yönteme **gizli anahtar kriptografisi** de denir.

- **En Büyük Zorluk:** Anahtarın paylaşımıdır. Eğer anahtarı güvenli olmayan bir kanal (örneğin e-posta) üzerinden gönderirseniz, bu kanalı izleyen herkes anahtarı ele geçirebilir ve şifreli mesajı çözebilir. Anahtarı paylaşmak için genellikle yüz yüze görüşmek veya "bant dışı" (out-of-band) güvenli yollar kullanmak gerekir.
    
- **Örnekler:**
    
    - **DES (Data Encryption Standard):** 1977'de standartlaştı. 56 bitlik anahtarı artık çok zayıf kabul ediliyor (1999'da 24 saatten kısa sürede kırıldı).
        
    - **3DES (Triple DES):** DES'in üç kez uygulanmış halidir. Geçici bir çözüm olarak kullanıldı ancak 2019'da kullanımdan kaldırılması (deprecated) önerildi.
        
    - **AES (Advanced Encryption Standard):** 2001'de kabul edilen güncel standarttır. 128, 192 veya 256 bitlik anahtarlar kullanır ve günümüzde oldukça güvenlidir.
        

---

## Asymmetric Encryption (Asimetrik Şifreleme)

Asimetrik şifreleme, birbiriyle matematiksel olarak ilişkili **iki farklı anahtar** kullanır: **Public Key** (Açık Anahtar) ve **Private Key** (Gizli Anahtar). Buna **açık anahtar kriptografisi** de denir.

- **Nasıl Çalışır?** Herkesin erişebileceği bir Public Key vardır. Biri size gizli bir mesaj göndermek istediğinde, bu mesajı sizin _Public Key_'inizle şifreler. Bu mesajı sadece sizin sahip olduğunuz ve gizli tuttuğunuz _Private Key_ çözebilir.
    
- **Özellikleri:**
    
    - Simetrik şifrelemeye göre daha **yavaştır**.
        
    - Daha **büyük anahtar boyutları** gerektirir (Örneğin, 256 bitlik bir AES anahtarının güvenliğine ulaşmak için yaklaşık 3072 bitlik bir RSA anahtarı gerekir).
        
    - **ECC (Elliptic Curve Cryptography)**, RSA'ya göre daha kısa anahtarlarla benzer güvenlik seviyesi sunduğu için modern sistemlerde (mobil cihazlar vb.) tercih edilir.
        
- **Örnekler:** RSA, Diffie-Hellman ve ECC.
    

---

## Terimler Özeti

- **Alice ve Bob:** Kriptografi örneklerinde güvenli iletişim kurmaya çalışan iki hayali karakterdir.
    
- **Symmetric Encryption:** Aynı anahtar kullanılır; anahtarın gizliliği kritiktir.
    
- **Asymmetric Encryption:** İki farklı anahtar kullanılır; Public Key herkesle paylaşılabilir, Private Key gizli tutulur.
    

---

### Karşılaştırma Tablosu

| **Özellik**        | **Simetrik Şifreleme**           | **Asimetrik Şifreleme**             |
| ------------------ | -------------------------------- | ----------------------------------- |
| **Anahtar Sayısı** | Tek bir ortak anahtar            | İki anahtar (Public & Private)      |
| **Hız**            | Çok hızlı                        | Daha yavaş                          |
| **Kullanım Alanı** | Büyük veri yığınlarını şifreleme | Anahtar değişimi ve dijital imzalar |
| **Anahtar Boyutu** | Kısa (örn. 256 bit)              | Uzun (örn. 2048-4096 bit)           |