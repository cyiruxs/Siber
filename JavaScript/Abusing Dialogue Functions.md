JavaScript'in temel amaçlarından biri, kullanıcılarla etkileşime geçmek için diyalog kutuları sağlamak ve web sayfası içeriğini dinamik olarak güncellemektir. JS; bu etkileşimi kolaylaştırmak için `alert`, `prompt` ve `confirm` gibi yerleşik (built-in) fonksiyonlar sunar. Ancak, bu özellikler güvenli bir şekilde uygulanmazsa, saldırganlar bunları **Cross-Site Scripting (XSS)** gibi saldırıları gerçekleştirmek için kötüye kullanabilirler.

Aşağıdaki egzersizleri tarayıcı konsolunuzda (F12 > Console) deneyebilirsiniz.

---

## 1. Alert (Uyarı)

`alert` fonksiyonu, kullanıcıya bilgi veya uyarı iletmek için kullanılan, üzerinde sadece "Tamam" (OK) butonu bulunan bir diyalog kutusu görüntüler.

- **Kullanım:** `alert("Mesajınız");`
    
- **Örnek:** Konsola `alert("Hello THM");` yazıp Enter'a bastığınızda ekranda bir uyarı kutusu belirecektir.
    

---

## 2. Prompt (Girdi İstemi)

`prompt` fonksiyonu, kullanıcıdan veri girişi isteyen bir diyalog kutusu görüntüler. Kullanıcı "Tamam" dediğinde girilen değeri döndürür; "İptal" (Cancel) derse `null` döndürür.

- **Örnek Uygulama:**
    
    JavaScript
    
    ```
    name = prompt("Adınız nedir?");
    alert("Merhaba " + name);
    ```
    

Bu kodu konsola yapıştırdığınızda, önce adınızı soran bir kutu, ardından adınızla sizi selamlayan bir uyarı kutusu göreceksiniz.

---

## 3. Confirm (Onaylama)

`confirm` fonksiyonu, bir mesaj ve "Tamam" ile "İptal" olmak üzere iki buton görüntüler. Kullanıcı "Tamam"ı seçerse `true`, "İptal"i seçerse `false` değeri döner.

- **Örnek:** `confirm("Devam etmek istiyor musunuz?");`
    

---

## 🛡️ Hackerlar Bu İşlevleri Nasıl Kötüye Kullanır?

Kötü niyetli bir aktörden, zararsız görünen ancak içinde JS barındıran bir HTML dosyası aldığınızı hayal edin. Aşağıdaki kod, kullanıcıyı rahatsız etmek amacıyla "Hacked" mesajını 3 kez gösterir:

HTML

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Hacked</title>
</head>
<body>
    <script>
        // Basit bir döngü ile kullanıcıyı darlamak
        for (let i = 0; i < 3; i++) {
            alert("Hacked");
        }
    </script>
</body>
</html>
```

### Siber Güvenlik ve CTF Perspektifi

> [!CAUTION]
> 
> **Client-Side Denial of Service (DoS):**
> 
> Yukarıdaki örnekte döngü sayısı 3 yerine **500** veya sonsuz döngü olarak ayarlanırsa, kullanıcı tarayıcıyı veya sekmeyi kapatmakta çok zorlanacaktır. Bu, kullanıcı deneyimini sabote eden en temel "istemci taraflı hizmet dışı bırakma" saldırısıdır.

|**Fonksiyon**|**Güvenlik Riski**|**Açıklama**|
|---|---|---|
|**alert()**|**XSS Onaylama**|Pentestlerde bir sayfada XSS zafiyeti olup olmadığını kanıtlamak (Proof of Concept) için en çok kullanılan fonksiyondur. Ekranda `alert(1)` görmek, kodun çalıştığını kanıtlar.|
|**prompt()**|**Phishing**|Saldırgan, meşru bir siteye JS enjekte ederek `prompt("Oturum süreniz doldu. Lütfen şifrenizi girin:")` şeklinde sahte bir giriş alanı yaratıp şifre çalabilir.|
|**confirm()**|**Clickjacking**|Kullanıcıyı yanıltarak istemediği bir işleme (örneğin bir dosyayı silme) onay vermesini sağlamak için manipüle edilebilir.|

---

### 🚩 CTF İpucu: XSS PoC (Proof of Concept)

Bir web uygulamasında arama kutusuna veya form alanına `<script>alert(document.cookie)</script>` yazdığınızda, eğer tarayıcı size oturum çerezlerinizi (cookies) bir uyarı kutusunda gösteriyorsa, o web sitesi **Stored** veya **Reflected XSS** saldırısına karşı savunmasız demektir.