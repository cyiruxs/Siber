# JavaScript Control Flow (Kontrol Akışı) ve Güvenlik İstismarları

JavaScript'te **Control flow** (kontrol akışı), ifadelerin ve kod bloklarının belirli koşullara göre yürütülme sırasını ifade eder. JS; kararlar vermek için `if-else`, `switch` ifadeleri ve eylemleri tekrarlamak için `for`, `while`, `do...while` gibi döngüler (loops) dahil olmak üzere çeşitli kontrol akışı yapıları sağlar. Kontrol akışının doğru kullanımı, bir programın çeşitli durumları etkili bir şekilde yönetebilmesini sağlar.

### Koşullu İfadeler İş Başında (Conditional Statements)

En çok kullanılan koşullu ifadelerden biri, bir koşulun `true` (doğru) veya `false` (yanlış) olarak değerlendirilmesine bağlı olarak farklı kod bloklarını çalıştırmanıza olanak tanıyan `if-else` ifadeleridir.

Bunu pratik olarak test etmek için, ekli VM'nin (Sanal Makine) masaüstünde `age.html` adlı bir dosya oluşturalım ve aşağıdaki kodu yapıştıralım:

HTML

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Age Verification</title>
</head>
<body>
    <h1>Age Verification</h1>
    <p id="message"></p>

    <script>
        // Kullanıcıdan yaş bilgisi alınıyor
        age = prompt("What is your age")
        if (age >= 18) {
            document.getElementById("message").innerHTML = "You are an adult.";
        } else {
            document.getElementById("message").innerHTML = "You are a minor.";
        }
    </script>
</body>
</html>
```

Dosyayı Google Chrome'da açmak için çift tıklayın. Yukarıdaki kodda, bir `prompt` size yaşınızı soracaktır. Eğer yaşınız 18'e eşit veya daha büyükse, "You are an adult." (Yetişkinsiniz) mesajı görüntülenecektir. Aksi takdirde, farklı bir mesaj gösterilecektir. Bu davranış, `age` değişkeninin değerini kontrol eden ve koşula göre uygun mesajı görüntüleyen `if-else` ifadesi tarafından kontrol edilir.

---

### 🔑 Login Formlarını Atlatma (Bypassing Login Forms)

Bir geliştiricinin, yalnızca "admin" kullanıcı adına ve belirli bir değerle eşleşen şifreye sahip kullanıcıların giriş yapmasına izin veren bir kimlik doğrulama (authentication) işlevini JS ile uyguladığını varsayalım. Bunu iş başında görmek için `exercises` klasöründeki `login.html` dosyasını açın.

Dosyaya çift tıklayıp tarayıcınızda açtığınızda, sizden bir kullanıcı adı ve şifre isteyecektir. Doğru kimlik bilgileri girilirse, giriş yaptığınızı onaylayan bir mesaj görüntülenecektir.

---

## 🛠️ Siber Güvenlik ve CTF İpuçları: İstemci Taraflı Güvenlik Riskleri

### 1. Client-Side Authentication (İstemci Taraflı Kimlik Doğrulama)

Metinde bahsedilen `login.html` örneği, ciddi bir güvenlik açığını temsil eder. Eğer kimlik doğrulama işlemleri sadece JavaScript (Client-side) ile yapılıyorsa, bu durum saldırganlar için kolay bir hedeftir.

- **Neden Riskli?**: JavaScript kodları tarayıcıya gönderilir. Bir saldırgan, sayfa kaynağına sağ tıklayıp "İncele" (Inspect) diyerek kaynak kodun içindeki şifreyi görebilir.
    
- **CTF İpucu**: Bir CTF sorusunda karşınıza bir login ekranı gelirse, ilk yapmanız gereken `Ctrl+U` ile kaynak kodunu incelemek veya Chrome Console üzerinden JS değişkenlerini (örneğin `password` veya `isAdmin`) manuel olarak değiştirmeyi denemektir.
    

### 2. Mantıksal Hatalar ve Manipülasyon

Saldırganlar, kontrol akışını şu yöntemlerle manipüle edebilir:

|**Teknik**|**Açıklama**|
|---|---|
|**Variable Overriding**|Konsola `age = 20` yazarak 18 yaş altı kısıtlamasını atlatmak.|
|**Logic Bypassing**|`if` bloğundaki koşulu konsoldan `true` dönecek şekilde modifiye etmek.|
|**Source Code Analysis**|Hardcoded (statik olarak yazılmış) kimlik bilgilerini kodun içinde aramak.|

### 🔍 Örnek İnceleme: Login Kod Analizi

Geliştiricinin muhtemelen kullandığı zayıf yapı şuna benzer:

JavaScript

```
if (username === "admin" && password === "P@ss123") {
    alert("Login Successful!");
} else {
    alert("Access Denied!");
}
```

**Saldırı Yöntemi:** Konsola girip doğrudan `alert("Login Successful!")` fonksiyonunu tetikleyen kod bloğunu inceleyerek şifreyi öğrenebilir veya `if` kontrolünü `if (true)` haline getirebilirsiniz.