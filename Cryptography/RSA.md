RSA, güvensiz kanallar üzerinden güvenli veri iletimini sağlayan bir public-key encryption algoritmasıdır. Güvensiz kanallarda, adversaries (saldırganların) iletişimi gizlice dinlemesi beklenir.

---

### RSA'yı Güvenli Kılan Matematik

RSA, büyük bir sayıyı factoring (çarpanlarına ayırma) işleminin matematiksel zorluğuna dayanır. İki büyük asal sayıyı çarpmak basit bir işlemdir; ancak, devasa bir sayının çarpanlarını bulmak çok daha fazla bilgi işlem gücü gerektirir.

İki asal sayıyı kağıt üzerinde bile çarpmak kolaydır, örneğin: $113 \times 127 = 14351$. Daha büyük asal sayılar için bile bu, elle yapılabilecek makul bir iştir. Şu sayısal örneği inceleyelim:

- **Asal sayı 1:** 982451653031
    
- **Asal sayı 2:** 169743212279
    
- **Çarpımları:** $982451653031 \times 169743212279 = 166764499494295486767649$
    

Öte yandan, hangi iki asal sayının çarpımının $14351$ ettiğini belirlemek oldukça zordur ve $166764499494295486767649$ sayısının çarpanlarını bulmak çok daha büyük bir meydan okumadır.

Gerçek dünya örneklerinde, asal sayılar bu örnektekilerden çok daha büyük olacaktır. Bir bilgisayar $166764499494295486767649$ sayısını kolayca factorise (çarpanlarına ayırma) edebilir; ancak 600'den fazla basamağı olan bir sayıyı factorise edemez. Ve her biri yaklaşık 300 basamaklı iki devasa asal sayının çarpımının, çarpımlarının factorisation işleminden daha kolay olduğu konusunda hemfikir olursunuz.

---

### Sayısal Örnek

Asimetrik şifrelemede encryption, decryption ve key kullanımını tekrar gözden geçirelim. Public key tüm taraflarca bilinir ve encryption için kullanılırken, private key korunur ve decryption için kullanılır.

Aşağıdaki basitleştirilmiş sayısal örnekte RSA algoritmasının işleyişini görüyoruz:

1. Bob iki asal sayı seçer: $p = 157$ ve $q = 199$.
    
2. $n = p \times q = 31243$ olarak hesaplar.
    
3. $\phi(n) = n - p - q + 1 = 31243 - 157 - 199 + 1 = 30888$ ile Bob, $\phi(n)$ ile aralarında asal olacak şekilde $e = 163$ seçer; ayrıca $e \times d = 1 \pmod{\phi(n)}$ olacak şekilde $d = 379$ seçer.
    
    (Örn: $e \times d = 163 \times 379 = 61777$ ve $61777 \pmod{30888} = 1$).
    
4. **Public key** $(n, e)$, yani $(31243, 163)$ ve **private key** $(n, d)$, yani $(31243, 379)$ olur.
    

Alice'in şifrelemek istediği değerin $x = 13$ olduğunu varsayalım:

- Alice, $y = x^e \pmod n = 13^{163} \pmod{31243} = 16341$ hesaplar ve gönderir.
    
- Bob, aldığı değeri $x = y^d \pmod n = 16341^{379} \pmod{31243} = 13$ hesaplayarak deşifre eder. Bu şekilde Bob, Alice'in gönderdiği değeri geri kazanır.
    

---

### CTF'lerde RSA

RSA'nın arkasındaki matematik CTF'lerde (Capture The Flag) sıklıkla karşımıza çıkar; değişkenleri hesaplamanızı veya bunlara dayalı bazı şifrelemeleri kırmanızı gerektirir. RSA CTF zorluklarını çözmek için bazı mükemmel araçlar mevcuttur:

- **RsaCtfTool:** En popüler araçlardan biridir.
    
- **rsatool:** RSA hesaplamaları için kullanılan bir diğer araçtır.
    

CTF'lerde RSA için ana değişkenleri bilmeniz gerekir: **p, q, m, n, e, d ve c.**

- **p ve q:** Büyük asal sayılar.
    
- **n:** p ve q'nun çarpımı.
    
- **Public key:** n ve e.
    
- **Private key:** n ve d.
    
- **m:** Orijinal mesajı, yani plaintext'i temsil eder.
    
- **c:** Şifrelenmiş metni, yani ciphertext'i temsil eder.
    

Crypto CTF zorlukları genellikle size bu değerlerin bir setini sunar ve bayrağı (flag) almak için şifrelemeyi kırmanız ve bir mesajı deşifre etmeniz gerekir.