**Burp Suite**'teki **Target** sekmesi, testimizin kapsamı (scope) üzerinde kontrol sağlamaktan çok daha fazlasını sunar. Üç alt sekmeden oluşur:

- **Site map:** Bu alt sekme, hedeflediğimiz web uygulamalarını bir ağaç yapısı (tree structure) içinde haritalandırmamıza olanak tanır. **Proxy** aktifken ziyaret ettiğimiz her sayfa site haritasında görüntülenecektir. Bu özellik, web uygulamasında sadece gezinerek otomatik olarak bir site haritası oluşturmamızı sağlar. **Burp Suite Professional**'da, site haritasını hedef üzerinde otomatik tarama (**automated crawling**) yapmak, sayfalar arasındaki bağlantıları keşfetmek ve sitenin mümkün olduğunca büyük bir kısmını haritalandırmak için de kullanabiliriz. **Burp Suite Community** ile bile, ilk numaralandırma (**enumeration**) adımlarımız sırasında veri toplamak için site haritasından yararlanabiliriz. Web uygulaması tarafından erişilen tüm **API** endpoint'leri site haritasında yakalanacağı için, özellikle **API**'leri haritalandırmak için kullanışlıdır.
    
- **Issue definitions:** Burp Community, **Burp Suite Professional**'da bulunan tam zafiyet tarama işlevini içermese de, tarayıcının aradığı tüm zafiyetlerin listesine hala erişimimiz vardır. **Issue definitions** bölümü, açıklamalar ve referanslarla tamamlanmış kapsamlı bir web zafiyetleri listesi sunar. Bu kaynak, raporlarda zafiyetlere atıfta bulunmak veya manuel test sırasında tespit edilmiş olabilecek belirli bir zafiyeti tanımlamaya yardımcı olmak için değerli olabilir.
    
- **Scope settings:** Bu ayar, **Burp Suite**'teki hedef kapsamını (target scope) kontrol etmemizi sağlar. Testimizin kapsamını tanımlamak için belirli domain'leri/IP'leri dahil etmemize veya hariç tutmamıza olanak tanır. Kapsamı yöneterek, özellikle hedeflediğimiz web uygulamalarına odaklanabilir ve gereksiz trafiği yakalamaktan kaçınabiliriz.
    

Genel olarak **Target** sekmesi, kapsam belirlemenin ötesinde web uygulamalarını haritalandırmamıza, hedef kapsamımızı ince ayar yaparak belirlememize ve referans amaçlı kapsamlı bir web zafiyetleri listesine erişmemize olanak tanıyan özellikler sunar.

### Challenge (Meydan Okuma)

`http://MACHINE_IP/` adresindeki siteye bir göz atın — modül boyunca bunu çok kullanacağız. Ana sayfada bağlantısı verilen diğer tüm sayfaları ziyaret edin, ardından site haritanızı (**sitemap**) kontrol edin — bir endpoint çok sıra dışı olarak göze çarpmalıdır!

Bunu tarayıcınızda ziyaret edin (veya o endpoint için site haritası girişinin "Response" bölümünü kullanın).