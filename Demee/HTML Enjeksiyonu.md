### **HTML Enjeksiyonu Nedir?**

**HTML Enjeksiyonu**, süzülmemiş kullanıcı girdisinin sayfada görüntülendiği durumlarda ortaya çıkan bir güvenlik açığıdır. Eğer bir web sitesi, kullanıcı girişlerini düzgün şekilde **temizlemez** ve bu girdileri doğrudan sayfada kullanırsa, bir saldırgan **HTML kodlarını siteye enjekte edebilir**.

![[Pasted image 20250215015754.png]]
### **Kullanıcı Girdilerinin Tehlikesi**

Web sitelerinin **HTML öğeleri (etiketleri)** kullanılarak oluşturulduğunu artık biliyoruz. Sayfanın kaynak kodunu görüntüleyerek bir geliştiricinin **giriş bilgilerini, gizli bağlantıları veya diğer hassas verileri unutarak bırakıp bırakmadığını** görebiliriz.

Eğer bir web sitesi **kullanıcıdan gelen verileri doğrudan sayfada gösterirse**, kullanıcı **HTML veya JavaScript kodları ekleyerek sayfanın görünümünü ve işlevselliğini değiştirebilir**.

Örneğin, bir form alanına `<h1>Hacklendiniz!</h1>` gibi bir kod yazıldığında, bu **sayfanın HTML yapısına eklenir ve saldırganın istediği gibi görüntülenir**.

### **HTML Enjeksiyonunu Önleme**

Bir web sitesinin güvenli olması için **kullanıcı girişlerinin süzülmesi ve zararlı kodların engellenmesi gerekmektedir**.

- Kullanıcı girişlerini **doğrudan sayfada görüntülememek**
- HTML özel karakterlerini (`<`, `>`, `"`, `'`, `&`) **filtrelemek veya dönüştürmek**
- Kullanıcı girdisini işlemeden önce **temizleme (sanitize) işlemi uygulamak**

**Genel Kural:** **Kullanıcı girişine asla güvenmeyin!**