Kapsülleme (Encapsulation), her katmanın kendi amaçlanan işlevine odaklanmasını sağlayan temel bir kavramdır. Aşağıdaki adımlarda bu süreci görebilirsin:

- **Application data (Uygulama verisi):** Her şey, kullanıcının göndermek istediği veriyi uygulamaya girmesiyle başlar. Örneğin, bir e-posta veya anlık mesaj yazıp gönder düğmesine basarsınız. Uygulama bu veriyi formatlar ve kullanılan uygulama protokolüne göre bir alt katman olan **transport layer**'ı kullanarak göndermeye başlar.
    
- **Transport protocol segment or datagram (Transport protokolü segmenti veya datagramı):** **TCP** veya **UDP** gibi **transport layer** protokolleri, uygun başlık (header) bilgilerini ekleyerek **TCP segment** (veya **UDP datagram**) yapısını oluşturur. Bu segment, bir alt katman olan **network layer**'a gönderilir.
    
- **Network packet (Network paketi):** **Network layer** (yani **Internet layer**), alınan **TCP segment** veya **UDP datagram** yapısına bir **IP header** ekler. Ardından, bu **IP packet** bir alt katman olan **data link layer**'a iletilir.
    
- **Data link frame (Data link çerçevesi):** Ethernet veya WiFi, **IP packet**'i alır ve uygun başlık (header) ve kuyruk (trailer) bilgilerini ekleyerek bir **frame** oluşturur.
    

Özetle; **application data** ile başlarız. **Transport layer**'da, bir **TCP segment** veya **UDP datagram** oluşturmak için **TCP** veya **UDP header** ekleriz. Tekrar, **network layer**'da, internet üzerinden yönlendirilebilecek bir **IP packet** elde etmek için uygun **IP header**'ı ekleriz. Son olarak, **link layer**'da bir WiFi veya Ethernet **frame** yapısı elde etmek için uygun başlık ve kuyruk bilgilerini ekleriz.
![[Pasted image 20251227164813.png]]

