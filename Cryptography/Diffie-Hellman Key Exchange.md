Simetrik şifreleme kullanmanın en büyük zorluklarından biri gizli anahtarı paylaşmaktır. Örneğin, iş ortağınıza stratejik belgeler göndermek istiyorsanız, bu şifreyi saldırganların okuyamayacağı veya değiştiremeyeceği güvenli bir kanal üzerinden iletmeniz gerekir.

---

### Diffie-Hellman Key Exchange (Diffie-Hellman Anahtar Değişimi)

**Key exchange** (anahtar değişimi), iki taraf arasında ortak bir sır oluşturmayı amaçlar. Bu yöntem, önceden paylaşılmış bir sırra ihtiyaç duymadan, güvensiz bir kanal üzerinden iki tarafın ortak bir anahtar oluşturmasına olanak tanır. Dışarıdan bir gözlemci bu anahtarı ele geçiremez. Oluşturulan bu anahtar, sonraki iletişimlerde simetrik şifreleme için kullanılır.

Mantığı anlamak için önce renk karışımı analojisine bakalım:

#### Adım Adım Diffie-Hellman Süreci

1. **Public Variables (Genel Değişkenler):** Alice ve Bob, herkesin görebileceği bir büyük asal sayı $p$ ve bir jeneratör $g$ ($0 < g < p$) üzerinde anlaşırlar.
    
    - _Örnek:_ $p = 29$ ve $g = 3$.
        
2. **Private Keys (Gizli Anahtarlar):** Her iki taraf da gizli birer tam sayı seçer.
    
    - Alice $a = 13$ seçer.
        
    - Bob $b = 15$ seçer.
        
    - Bu değerler asla paylaşılmaz.
        
3. **Public Keys (Açık Anahtarlar):** Her iki taraf, kendi gizli anahtarını ve genel değişkenleri kullanarak açık anahtarını hesaplar.
    
    - Alice: $A = g^a \pmod p = 3^{13} \pmod{29} = 19$.
        
    - Bob: $B = g^b \pmod p = 3^{15} \pmod{29} = 26$.
        
4. **Key Exchange (Anahtar Değişimi):** Alice ve Bob bu açık anahtarları ($A$ ve $B$) birbirlerine gönderirler.
    
5. **Shared Secret (Ortak Sır):** Her iki taraf, karşıdan aldığı açık anahtarı kendi gizli anahtarıyla işleyerek ortak anahtarı hesaplar.
    
    - Alice: $B^a \pmod p = 26^{13} \pmod{29} = 10$.
        
    - Bob: $A^b \pmod p = 19^{15} \pmod{29} = 10$.
        
    - Her iki hesaplama da aynı sonucu verir: $g^{ab} \pmod p = 10$. Bu artık onların **shared secret key** (ortak gizli anahtar) değeridir.
        

---

### RSA ve Diffie-Hellman İşbirliği

Diffie-Hellman genellikle **RSA** ile birlikte kullanılır. Diffie-Hellman anahtar üzerinde anlaşmak (**key agreement**) için kullanılırken; RSA dijital imzalar, kimlik doğrulama ve anahtar taşıma için kullanılır. Örneğin RSA, dijital imzalama yoluyla konuştuğunuz kişinin gerçekten Bob olduğunu kanıtlamaya yardımcı olur. Bu, bir saldırganın Bob gibi davranarak araya girdiği **man-in-the-middle** (ortadaki adam) saldırılarını önler.

Özetle, Diffie-Hellman ve RSA, kapsamlı bir güvenlik çözümü sunmak için birçok modern güvenlik protokolüne entegre edilmiştir.