
---

### OSI Modeli Hakkında Genel Bilgi

OSI (Açık Sistemler Arası Bağlantı) modeli, Uluslararası Standardizasyon Örgütü (ISO) tarafından geliştirilen ve bir bilgisayar ağındaki iletişimin nasıl gerçekleşmesi gerektiğini tanımlayan **kavramsal bir modeldir**. Başka bir deyişle, OSI modeli bilgisayar ağı iletişimleri için bir çerçeve sunar. Bu model teorik olsa da, ağ kavramlarını daha derinlemesine anlamak için öğrenilmesi ve anlaşılması hayati önem taşır. OSI modeli yedi katmandan oluşur:

- Fiziksel Katman
    
- Veri Bağlantı Katmanı
    
- Ağ Katmanı
    
- Taşıma Katmanı
    
- Oturum Katmanı
    
- Sunum Katmanı
    
- Uygulama Katmanı
    

Numaralandırma, fiziksel katmanın 1. katman, en üst katman olan uygulama katmanının ise 7. katman olarak başlamasıyla yapılır. Katmanları aşağıdan yukarıya doğru hatırlamanıza yardımcı olmak için "Pizzayı Dışarıya Atmayın Lütfen" gibi bir anımsatıcı kullanabilirsiniz. Bu, onları ezberlemenize yardımcı olursa, internette başka kolay hatırlanabilir kısaltmaları da kontrol edebilirsiniz. OSI modelinin katmanlarını numaralarıyla birlikte hatırlamak önemlidir; aksi takdirde "3. katman anahtarı" veya "7. katman güvenlik duvarı" gibi terimleri anlamakta zorlanırsınız.

---

### Katman 1: Fiziksel Katman

**Fiziksel katman**, veya 1. katman, cihazlar arasındaki fiziksel bağlantıyla ilgilenir; bu, kablo gibi ortamı ve 0 ve 1 gibi ikili rakamların tanımını içerir. Veri iletimi elektriksel, optik veya kablosuz bir sinyal aracılığıyla olabilir. Sonuç olarak, fiziksel ortamımıza bağlı olarak veri kablolarına veya antenlere ihtiyacımız vardır.

Aşağıdaki illüstrasyonda gösterilen Ethernet kablosu ve optik fiber kabloya ek olarak, fiziksel katman ortamı örnekleri arasında WiFi radyo bantları, 2.4 GHz bandı, 5 GHz bandı ve 6 GHz bandı bulunur.

---

### Katman 2: Veri Bağlantı Katmanı

Fiziksel katman sinyalimizi iletmek için bir ortam tanımlar. Veri bağlantı katmanı, yani 2. katman, aynı ağ kesimindeki düğümler arasında veri aktarımını sağlayan **protokolü temsil eder**. Daha basit terimlerle ifade edelim. Veri bağlantı katmanı, aynı ağ kesimindeki farklı sistemler arasında nasıl iletişim kurulacağına dair bir anlaşmayı tanımlar. Bir ağ kesimi, bilgi aktarımı için paylaşılan bir ortam veya kanal kullanan bir grup ağa bağlı cihazı ifade eder. Örneğin, on bilgisayarın bir ağ anahtarına bağlı olduğu bir şirket ofisini düşünün; bu bir ağ kesimidir.

2. katman örnekleri arasında **Ethernet** (yani 802.3) ve **WiFi** (yani 802.11) bulunur. Ethernet ve WiFi adresleri altı bayttır. Adreslerine **MAC adresi** denir, burada MAC, Media Access Control anlamına gelir. Genellikle her iki onaltılık basamak (bir bayt) arasına bir iki nokta üst üste konularak onaltılık formatta ifade edilirler. En soldaki üç bayt satıcıyı tanımlar.
    

Gerçek ağ iletişiminde Ethernet veya WiFi üzerinden her karede iki MAC adresi görmeyi bekleriz. Aşağıdaki ekran görüntüsündeki paket şunu gösterir:

- Sarı renkle vurgulanan hedef veri-bağlantı adresi (MAC adresi)
    
- Mavi renkle vurgulanan kaynak veri-bağlantı adresi (MAC adresi)
    
- Kalan bitler gönderilen veriyi gösterir
    

---

### Katman 3: Ağ Katmanı

Veri bağlantı katmanı, aynı ağ kesimindeki iki düğüm arasında veri göndermeye odaklanır. Ağ katmanı, yani 3. katman, **farklı ağlar arasında veri göndermekle ilgilidir**. Daha teknik terimlerle, ağ katmanı mantıksal adreslemeyi ve yönlendirmeyi, yani çeşitli ağlar arasında ağ paketlerini aktarmak için bir yol bulmayı yönetir.

Veri bağlantı katmanında, on bilgisayarı olan bir şirket ofisi örneği verdik, burada veri bağlantı katmanı aralarındaki bağlantıyı sağlamaktan sorumludur. Bu şirketin çeşitli şehirler, ülkeler ve hatta kıtalar arasında dağıtılmış birden fazla ofisi olduğunu varsayalım. Ağ katmanı, farklı ofisleri birbirine bağlamaktan sorumludur.

Aşağıdaki ağ, bilgisayar A ve B'nin farklı ağlarda olmalarına rağmen bağlı olduğunu gösterir. İki bilgisayarı bağlayan iki yol olduğunu da fark edebilirsiniz; ağ katmanı, ağ paketlerini daha iyi gördüğü yoldan yönlendirecektir.

Ağ katmanı örnekleri arasında **Internet Protokolü (IP)**, **Internet Kontrol Mesaj Protokolü (ICMP)** ve **IPSec ve SSL/TLS VPN** gibi Sanal Özel Ağ (VPN) protokolleri bulunur.

---

### Katman 4: Taşıma Katmanı

4. katman olan **taşıma katmanı**, farklı ana bilgisayarlardaki çalışan uygulamalar arasında **uçtan uca iletişimi** sağlar. Web tarayıcınız, TryHackMe web sunucusuna taşıma katmanı üzerinden bağlıdır ve akış kontrolü, segmentasyon ve hata düzeltme gibi çeşitli işlevleri destekleyebilir.
    
5. katman örnekleri **İletim Kontrol Protokolü (TCP)** ve **Kullanıcı Datagram Protokolü (UDP)**'dir.
    

---

### Katman 5: Oturum Katmanı

**Oturum katmanı**, farklı ana bilgisayarlarda çalışan uygulamalar arasındaki iletişimi **kurmaktan, sürdürmekten ve senkronize etmekten** sorumludur. Bir oturum kurmak, uygulamalar arasında iletişimi başlatmak ve oturum için gerekli parametreleri müzakere etmek anlamına gelir. Veri senkronizasyonu, verilerin doğru sırada iletilmesini sağlar ve iletim hataları durumunda kurtarma mekanizmaları sunar.

Oturum katmanı örnekleri **Ağ Dosya Sistemi (NFS)** ve **Uzak Yordam Çağrısı (RPC)**'dir.

---

### Katman 6: Sunum Katmanı

**Sunum katmanı**, verinin uygulama katmanının anlayabileceği bir biçimde iletilmesini sağlar. 6. katman, **veri kodlaması, sıkıştırması ve şifrelemesini** yönetir. Kodlamaya bir örnek, ASCII veya Unicode gibi karakter kodlamasıdır.

Sunum katmanında çeşitli standartlar kullanılır. Bir görüntüyü e-posta ile göndermek istediğimiz senaryoyu düşünün. İlk olarak, resimlerimizi kaydetmek için **JPEG, GIF ve PNG** kullanırız; ayrıca, kullanıcıdan e-posta istemcisi tarafından gizlenmiş olsa da, dosyayı e-postamıza eklemek için **MIME** (Multipurpose Internet Mail Extensions) kullanırız. MIME, ikili bir dosyayı 7 bitlik ASCII karakterleri kullanarak kodlar.

---

### Katman 7: Uygulama Katmanı

**Uygulama katmanı**, doğrudan son kullanıcı uygulamalarına ağ hizmetleri sunar. Web tarayıcınız, bir dosya istemek, bir form göndermek veya bir dosya yüklemek için **HTTP** protokolünü kullanır.

Uygulama katmanı en üst katmandır ve farklı uygulamalar kullanırken birçok protokolüyle karşılaşmış olabilirsiniz. 7. katman protokolleri örnekleri **HTTP, FTP, DNS, POP3, SMTP ve IMAP**'dir. Hepsine aşina değilseniz endişelenmeyin.

---

### Özet

ISO OSI modeli hakkında ilk kez okumak göz korkutucu olabilir; ancak, ağ protokolleri üzerine çalışmanız ilerledikçe kolaylaşır. Çalışmalarınıza yardımcı olmak için, ISO OSI katmanlarını aşağıdaki tabloda özetledik.

|Katman Numarası|Katman Adı|Ana İşlevi|Örnek Protokoller ve Standartlar|
|---|---|---|---|
|Katman 7|Uygulama katmanı|Uygulamalara hizmet ve arayüzler sağlar|HTTP, FTP, DNS, POP3, SMTP, IMAP|
|Katman 6|Sunum katmanı|Veri kodlaması, şifrelemesi ve sıkıştırması|Unicode, MIME, JPEG, PNG, MPEG|
|Katman 5|Oturum katmanı|Oturumları kurma, sürdürme ve senkronize etme|NFS, RPC|
|Katman 4|Taşıma katmanı|Uçtan uca iletişim ve veri segmentasyonu|UDP, TCP|
|Katman 3|Ağ katmanı|Ağlar arasında mantıksal adresleme ve yönlendirme|IP, ICMP, IPSec|
|Katman 2|Veri bağlantı katmanı|Bitişik düğümler arasında güvenilir veri aktarımı|Ethernet (802.3), WiFi (802.11)|
|Katman 1|Fiziksel katman|Fiziksel veri iletim ortamı|Elektriksel, optik ve kablosuz sinyaller|