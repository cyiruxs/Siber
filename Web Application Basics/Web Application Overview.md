Bir web uygulamasını bir gezegen olarak hayal edin. Astronotlar, bir gezegenin yüzeyini keşfetmek için ona seyahat ederler; bu, birisinin bir web uygulamasını keşfetmek veya içinde gezinmek için bir **web browser** kullanmasına benzer. Bir gezegenin sadece yüzeyini görsek de, yüzeyin altında pek çok şey olup biter. Tüm gezegeni, **web server** yüzeyinin altında pek çok şeyin döndüğü bir yapı olarak düşünebilirsiniz, ancak genellikle görebildiğimiz tek şey web sayfalarının veya uygulamaların yüzeyidir. Şimdi bir web uygulamasını oluşturan çeşitli bileşenleri inceleyeceğiz.

---

## Front End

**Front End**, bir astronotun doğa kanunlarına göre görebildiği ve etkileşime girebildiği gezegenin yüzeyine benzer olarak düşünülebilir. Bir web uygulamasında kullanıcı, bunu yapmak için **HTML**, **CSS** ve **JavaScript** gibi bir dizi teknolojiyle etkileşime girer.

- **HTML (Hypertext Markup Language):** Web uygulamalarının temel bir yönüdür. Bir **web browser**'a neyi ve nasıl görüntüleyeceğini talimat veren bir dizi komut veya koddur. Gezegende yaşayan basit organizmalarla kıyaslanabilir; bu organizmaların, basit organizmaların nasıl bir araya getirileceğine dair talimatlar olan bir **DNA**'sı vardır.
    
- **CSS (Cascading Style Sheets):** Web uygulamalarında belirli renkler, metin türleri ve düzenler gibi standart bir görünümü tanımlar. **DNA** analojisine devam edersek, bunlar basit organizmanın rengini, şeklini, boyutunu ve dokusunu tanımlayan **DNA** parçalarıyla kıyaslanabilir.
    
- **JS (JavaScript):** Web uygulaması **front end**'inin bir parçasıdır ve **web browser** içinde daha karmaşık faaliyetlere olanak tanır. **HTML**, neyin görüntüleneceğine dair basit bir talimat seti olarak kabul edilebilirken, **JavaScript**, neyin görüntüleneceği konusunda seçimler ve kararlar yapılmasına olanak tanıyan daha gelişmiş bir talimat setidir. Gezegen analojisinde **JavaScript**, bir şeyin kendisiyle ne şekilde etkileşime girdiğine bağlı olarak kararlar verilmesini sağlayan gelişmiş bir organizmanın beyni olarak düşünülebilir.
    

---

## Back End

Bir web uygulamasının **Back End**'i, bir **web browser** içinde görmediğiniz ancak web uygulamasının çalışması için önemli olan şeylerdir. Bir gezegende bunlar görsel olmayan şeylerdir: Bir binayı ayakta tutan yapılar, hava ve ayakları yerde tutan yerçekimi.

- **Database:** Bilgilerin saklanabildiği, değiştirilebildiği ve geri çağrılabildiği yerdir. Bir web uygulaması, bir ziyaretçinin neyin gösterilip gösterilmeyeceğine dair tercihlerini saklamak ve geri çağırmak isteyebilir; bu bir **database** içinde saklanır. Bir gezegende, konumlar hakkındaki bilgileri haritalarda saklayan, günlüğe notlar yazan veya kitapları bir kütüphaneye, dosyaları bir dosya dolabına koyan daha gelişmiş sakinler olabilir.
    
- **Infrastructure:** Web uygulamasını destekleyen **web servers**, **application servers**, **storage**, çeşitli **networking** cihazları ve diğer yazılımlar gibi Web Uygulamalarını destekleyen birçok diğer altyapı bileşeni vardır. Bir gezegende bunlar mevcut yollar, o yollarda giden arabalar ve arabalara güç veren yakıttır.
    
- **WAF (Web Application Firewall):** Web uygulamaları için isteğe bağlı bir bileşendir. Tehlikeli isteklerin **Web Server**'dan uzaklaştırılmasına yardımcı olur ve bir koruma öğesi sağlar. Bu, bir gezegenin atmosferinin sakinlerini zararlı UV ışınlarından nasıl koruyabildiğine benzer olarak düşünülebilir.
    

---

## Özet (Summary)

Bir web uygulamasını sunmak için dahil olan birçok bileşen vardır. **HTML**, **CSS** ve **JavaScript** gibi **Front End** bileşenleri tarayıcı içindeki deneyime odaklanır. **Web Server**, **Database** veya **WAF** gibi **Back End** bileşenleri, web uygulamasının çalışmasını sağlayan yüzeyin altındaki motordur. Bu basit giriş, gelecek görevlerde üzerine inşa edilecektir.

---

# 🚀 Ek Bilgiler ve Siber Güvenlik Perspektifi

Bir siber güvenlik uzmanı veya CTF oyuncusu için bu yapıyı anlamak, saldırı yüzeyini (**Attack Surface**) belirlemek adına kritiktir.

### 📊 Bileşen Karşılaştırma Tablosu

|**Bileşen**|**Analoji**|**Güvenlik Odağı**|**Yaygın Saldırı Türleri**|
|---|---|---|---|
|**Front End**|Yüzey / Görünüm|Client-Side Security|XSS, CSRF, Clickjacking|
|**Back End**|Çekirdek / Motor|Server-Side Security|SQLi, RCE, IDOR, LFI/RFI|
|**Database**|Kütüphane / Arşiv|Veri Gizliliği|SQL Injection, NoSQL Injection|
|**WAF**|Atmosfer / Kalkan|Filtreleme|WAF Bypass, Payloading|

### 🔍 Görselleştirme: Web Uygulama Akışı (Mermaid)

Kod snippet'i

```
graph TD
    User((Kullanıcı/Astronot)) -->|Tarayıcı üzerinden istek| FrontEnd[Front End: HTML/CSS/JS]
    FrontEnd -->|Filtreleme| WAF{WAF: Güvenlik Duvarı}
    WAF -- Temiz --> WebServer[Web Server / Infrastructure]
    WAF -- Zararlı --> Block[Engelleme / Log]
    WebServer -->|Sorgu| DB[(Database)]
    DB -->|Veri| WebServer
    WebServer -->|Yanıt| FrontEnd
    FrontEnd -->|Görsel Sunum| User
```

---

### 🚩 CTF & Siber Güvenlik İpuçları

> [!TIP] **İpucu 1: Client-Side Güvenliğe Güvenmeyin**
> 
> JavaScript (JS) gezegenin beynidir ancak bu beyin kullanıcının kontrolündeki bir cihazda çalışır. Bir CTF sorusunda eğer girdi doğrulaması (input validation) sadece JavaScript ile yapılıyorsa, bu doğrulamayı tarayıcı üzerinden devre dışı bırakabilir veya isteği doğrudan **Burp Suite** ile yakalayıp manipüle edebilirsiniz.

> [!CAUTION] **İpucu 2: Database ve SQL Injection**
> 
> Eğer gezegenin kütüphanesine (Database) erişmek için kullanılan formlar yeterince filtrelenmiyorsa, saldırganlar özel karakterler (örn: `' OR 1=1 --`) kullanarak tüm kütüphaneyi ele geçirebilir. Bu, sızma testlerinde en sık karşılaşılan yüksek riskli açıklardan biridir.

> [!IMPORTANT] **İpucu 3: WAF Bypass**
> 
> WAF, zararlı UV ışınlarını (istekleri) engeller ancak bazen "bulutların" arasından sızmak mümkündür. Karakter kodlama (encoding), büyük-küçük harf değişimi veya HTTP parametre kirliliği (HPP) teknikleri, WAF'ı atlatmak için sıkça kullanılır.

> [!NOTE] **İpucu 4: Bilgi Toplama (Reconnaissance)**
> 
> **Infrastructure** katmanında hangi yolların (portlar) ve arabaların (servis sürümleri) kullanıldığını bilmek saldırı için şarttır. `Nmap` veya `Wappalyzer` gibi araçlar kullanarak hedef gezegenin hangi teknolojilerle (Apache, Nginx, PHP, Python vb.) inşa edildiğini öğrenebilirsiniz.