# Asimetrik Kriptografi ile Anahtar Değişimi

**Symmetric encryption** için anahtar değişimi yapmak, **asymmetric cryptography**’nin yaygın bir kullanım alanıdır. Asimetrik şifreleme, simetrik şifrelemeye kıyasla **nispeten yavaştır**; bu nedenle asimetrik şifrelemeyi, simetrik şifreleme **cipher**’larını ve **key**’lerini müzakere etmek ve üzerinde anlaşmak için kullanırız.

Ancak asıl soru şudur:  
**Anahtarı, başkalarının dinleyip görebileceği şekilde iletmeden sunucu ile nasıl paylaşırsınız?**

---

## 🔒 Kilitli Kutu Analojisi

### Analogy

İletişim kurmak için gizli bir **secret code**’unuz ve bu kodun nasıl kullanılacağına dair talimatlarınız olduğunu hayal edin. Soru şudur: Bu talimatları, kimsenin okuyamayacağı şekilde arkadaşınıza nasıl gönderebilirsiniz?

Cevap göründüğünden daha basittir: Arkadaşınızdan bir **lock (kilit)** isteyebilirsiniz. Bu kilidin anahtarı yalnızca arkadaşınızda olsun ve sizin de bu kilitle kilitlenebilen, kırılmaz bir **box (kutu)**’ya sahip olduğunuzu varsayalım.

Talimatları kilitli bir kutunun içine koyup arkadaşınıza gönderirseniz, kutu ona ulaştığında kilidi açabilir ve talimatları okuyabilir. Bundan sonra, başkalarının dinlemesi riski olmadan gizli kodu kullanarak iletişim kurabilirsiniz.

---

## Analojinin Kriptografik Karşılığı

Bu metaforda:

- **Secret code**, bir **symmetric encryption cipher and key**’i temsil eder.
    
- **Lock**, sunucunun **public key**’ini temsil eder.
    
- **Lock’s key**, sunucunun **private key**’ini temsil eder.
    

|Analogy|Cryptographic System|
|---|---|
|Secret Code|Symmetric Encryption Cipher and Key|
|Lock|Public Key|
|Lock’s Key|Private Key|

Bu nedenle, asimetrik kriptografiyi yalnızca **bir kez** kullanmanız yeterlidir; böylece performansı olumsuz etkilemez. Ardından, iletişimi gizli bir şekilde **symmetric encryption** kullanarak sürdürebilirsiniz.

---

## Gerçek Dünya

Gerçek hayatta, konuştuğunuz kişinin gerçekten söylediği kişi olduğunu doğrulamak için **daha fazla kriptografiye** ihtiyaç vardır. Bu doğrulama işlemi, **digital signatures** ve **certificates** kullanılarak gerçekleştirilir. Bunları bu bölümün ilerleyen kısımlarında ele alacağız.

---

İstersen bunu:

- **TLS / HTTPS el sıkışması (handshake)** ile ilişkilendirebilirim,
    
- **Public Key Infrastructure (PKI)** bağlamında genişletebilirim,
    
- ya da **Obsidian için linkli kavram notları** haline getirebilirim.