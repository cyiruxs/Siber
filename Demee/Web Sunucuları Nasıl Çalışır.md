### **Web Sunucusu Nedir?**

Bir **web sunucusu**, **gelen bağlantıları dinleyen ve HTTP protokolünü kullanarak web içeriğini istemcilere ileten bir yazılımdır**.

**En yaygın web sunucuları şunlardır:**

- **Apache**
- **Nginx**
- **IIS (Internet Information Services)**
- **NodeJS**

Web sunucusu, **dosyalarını belirli bir kök dizinden (root directory) sunar**. Bu dizin, yazılım ayarlarında belirtilir.

Örneğin:

- **Linux’ta (Apache ve Nginx)** → `/var/www/html`
- **Windows’ta (IIS)** → `C:\inetpub\wwwroot`

Eğer bir istemci **[http://www.example.com/picture.jpg](http://www.example.com/picture.jpg)** dosyasını talep ederse, sunucu **/var/www/html/picture.jpg** dosyasını yerel diskinden gönderir.

---

### **Sanal Hostlar (Virtual Hosts)**

Bir **web sunucusu**, **farklı alan adlarına sahip birden fazla web sitesini barındırabilir**. Bunu yapabilmek için **sanal hostları (Virtual Hosts)** kullanır.

**Nasıl Çalışır?**

1. Web sunucusu, **HTTP başlıklarındaki (headers) alan adını kontrol eder**.
2. **Konfigürasyon dosyalarındaki sanal hostları (Virtual Hosts) karşılaştırır**.
3. **Eğer eşleşen bir sanal host varsa**, ilgili web sitesini sunar.
4. **Eğer eşleşme yoksa**, varsayılan siteyi gösterir.

Örneğin, aşağıdaki gibi bir yapılandırma olabilir:

- **one.com** → `/var/www/website_one`
- **two.com** → `/var/www/website_two`

**Bir web sunucusunda barındırılabilecek web sitesi sayısında bir sınır yoktur.**

---

### **Statik vs Dinamik İçerik**

#### **Statik İçerik**

- **Hiç değişmeyen içeriktir**.
- Örnekler: **resimler, JavaScript, CSS dosyaları ve sabit HTML sayfaları**.
- Web sunucusu **dosyayı direkt olarak istemciye gönderir**, üzerinde değişiklik yapılmaz.

#### **Dinamik İçerik**

- **Kullanıcıdan gelen isteklere göre değişebilen içeriktir**.
- Örneğin:
    - **Bir blogun ana sayfası**, en son yazıları gösterir.
    - **Bir arama sayfası**, girilen kelimeye göre farklı sonuçlar döndürür.
- **Bu değişiklikler, Backend (Arka Uç) tarafından işlenir**.
- **HTML kaynağında Backend işlemleri görülmez**, çünkü kullanıcıya sadece **işlenmiş sonuç** gösterilir.

---

### **Backend ve Betik Dilleri (Scripting & Backend Languages)**

**Backend dilleri**, web sitelerini **interaktif hale getiren programlama dilleridir**.

**Bazı yaygın Backend dilleri şunlardır:**

- **PHP**
- **Python**
- **Ruby**
- **NodeJS**
- **Perl**

Bu diller **veritabanlarıyla iletişim kurabilir**, **kullanıcıdan gelen verileri işleyebilir** ve **dış servislerle etkileşime girebilir**.

#### **PHP ile Basit Bir Örnek**

Eğer **[http://example.com/index.php?name=adam](http://example.com/index.php?name=adam)** adresine istek gönderilirse ve `index.php` şu şekilde yazılmışsa:

```php
<html><body>Hello <?php echo $_GET["name"]; ?></body></html>
```

Bu, istemciye şu şekilde döndürülür:

```html
<html><body>Hello adam</body></html>
```

Dikkat ederseniz, istemci **PHP kodunu göremez**, çünkü bu işlem **Backend'de gerçekleşir**.

**Ancak!** Dinamik içerik oluşturan web uygulamaları **güvenli bir şekilde geliştirilmezse, saldırılara açık hale gelebilir**. 