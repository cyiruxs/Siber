# OSI (Open Systems Interconnection) Modeli

Başlamadan önce, OSI modelinin ilk başta karmaşık görünebileceğini belirtelim. Kriptik kısaltmalarla karşılaşırsanız endişelenmeyin; OSI model katmanlarını örneklerle açıklıyoruz. Bu modülün sonunda bu görev size çocuk oyuncağı gibi gelecektir.

OSI (Open Systems Interconnection) modeli, **International Organization for Standardization (ISO)** tarafından geliştirilmiş, bilgisayar ağlarında iletişimin nasıl gerçekleşmesi gerektiğini tanımlayan kavramsal bir modeldir. Başka bir deyişle, OSI modeli bilgisayar ağları için bir iletişim çerçevesi tanımlar. Teorik bir model olmasına rağmen, ağ kavramlarını daha derinlemesine anlamaya yardımcı olduğu için öğrenilmesi ve anlaşılması önemlidir.

OSI modeli yedi katmandan oluşur:

- Physical Layer
    
- Data Link Layer
    
- Network Layer
    
- Transport Layer
    
- Session Layer
    
- Presentation Layer
    
- Application Layer
    

Numaralandırma, **Physical Layer = Layer 1** olacak şekilde başlar ve en üst katman olan **Application Layer = Layer 7** ile biter. Katmanları alttan üste doğru hatırlamak için şu mnemonic kullanılabilir:

> **Please Do Not Throw Spinach Pizza Away**

Katmanları ve katman numaralarını bilmek önemlidir; aksi hâlde “layer 3 switch” veya “layer 7 firewall” gibi terimleri anlamakta zorlanabilirsiniz.

---

## Layer 1: Physical Layer

Physical Layer, yani Layer 1, cihazlar arasındaki fiziksel bağlantıyla ilgilenir. Buna kullanılan ortam (medium) ve binary digits olan 0 ve 1’in tanımı dahildir. Veri iletimi elektriksel, optik veya wireless sinyallerle yapılabilir. Bu nedenle kullanılan fiziksel ortama bağlı olarak data cables veya antennas gereklidir.

Ethernet cable ve optical fibre cable dışında, Physical Layer örnekleri arasında WiFi radio bands bulunur. Bunlar:

- 2.4 GHz band
    
- 5 GHz band
    
- 6 GHz band
    

---

## Layer 2: Data Link Layer

Physical Layer sinyalin iletileceği ortamı tanımlar. **Data Link Layer (Layer 2)** ise aynı network segment üzerindeki node’lar arasında veri transferini sağlayan protokolleri temsil eder. Daha basit bir ifadeyle, Data Link Layer aynı network segment üzerindeki sistemlerin nasıl iletişim kuracağına dair bir anlaşmayı tanımlar.

Network segment, bilgi transferi için ortak bir medium veya channel kullanan ağ cihazları grubunu ifade eder. Örneğin, bir ofiste bir switch’e bağlı on bilgisayar bir network segment oluşturur.

Layer 2 örnekleri şunlardır:

- Ethernet (802.3)
    
- WiFi (802.11)
    

Ethernet ve WiFi adresleri altı byte uzunluğundadır ve **MAC address** olarak adlandırılır. MAC, _Media Access Control_ anlamına gelir. MAC address’ler genellikle her iki hexadecimal digit arasında iki nokta olacak şekilde ifade edilir. Sol taraftaki ilk üç byte, network interface’i üreten vendor’ı tanımlar.

Gerçek ağ iletişiminde, Ethernet veya WiFi üzerinden iletilen her frame içinde iki MAC address bulunur:

- Destination data-link address (MAC address)
    
- Source data-link address (MAC address)
    

Geri kalan bitler iletilen veriyi içerir.

---

## Layer 3: Network Layer

Data Link Layer, aynı network segment üzerindeki iki node arasında veri gönderimine odaklanır. **Network Layer (Layer 3)** ise verinin farklı network’ler arasında gönderilmesiyle ilgilenir. Daha teknik bir ifadeyle, Network Layer **logical addressing** ve **routing** işlemlerini yönetir; yani network packet’larının farklı network’ler arasında hangi yol üzerinden iletileceğini belirler.

Data Link Layer için tek bir ofiste bulunan ve aynı switch’e bağlı on bilgisayardan oluşan bir network segment örneği verilmişti. Bu şirketin farklı şehirlerde, ülkelerde veya kıtalarda bulunan birden fazla ofisi olduğunu varsayalım. Network Layer, bu farklı ofisleri birbirine bağlamaktan sorumludur.

Bir network diyagramında, A ve B bilgisayarlarının farklı network’lerde olmalarına rağmen birbirleriyle bağlantılı olduğu ve aralarında birden fazla yol bulunduğu görülebilir. Network Layer, network packet’larını uygun gördüğü yol üzerinden yönlendirir.

Layer 3 örnekleri şunlardır:

- Internet Protocol (IP)
    
- Internet Control Message Protocol (ICMP)
    
- Virtual Private Network (VPN) protocols
    
    - IPSec
        
    - SSL/TLS VPN
        

---

## Layer 4: Transport Layer

**Transport Layer (Layer 4)**, farklı host’lar üzerinde çalışan uygulamalar arasında end-to-end communication sağlar. Web browser, bir web server’a Transport Layer üzerinden bağlanır. Bu katman; flow control, segmentation ve error correction gibi işlevleri destekler.

Layer 4 örnekleri:

- Transmission Control Protocol (TCP)
    
- User Datagram Protocol (UDP)
    

---

## Layer 5: Session Layer

**Session Layer**, farklı host’lar üzerinde çalışan uygulamalar arasındaki iletişimi kurmak, sürdürmek ve senkronize etmekten sorumludur. Session establishment, uygulamalar arasındaki iletişimin başlatılmasını ve gerekli parametrelerin belirlenmesini ifade eder. Data synchronisation, verinin doğru sırayla iletilmesini sağlar ve iletim hataları durumunda recovery mekanizmaları sunar.

Layer 5 örnekleri:

- Network File System (NFS)
    
- Remote Procedure Call (RPC)
    

---

## Layer 6: Presentation Layer

**Presentation Layer**, verinin Application Layer tarafından anlaşılabilir bir formatta iletilmesini sağlar. Layer 6; data encoding, compression ve encryption işlemlerini gerçekleştirir. Encoding’e örnek olarak ASCII veya Unicode character encoding verilebilir.

Presentation Layer’da çeşitli standartlar kullanılır. Örneğin, bir image e-posta ile gönderilmek istendiğinde JPEG, GIF veya PNG formatları kullanılır. Ayrıca, kullanıcıdan gizli olacak şekilde email client tarafından **MIME (Multipurpose Internet Mail Extensions)** kullanılır. MIME, binary dosyaları 7-bit ASCII karakterler kullanarak encode eder.

---

## Layer 7: Application Layer

**Application Layer**, network servislerini doğrudan end-user applications’a sağlar. Bir web browser, HTTP protocol’ünü kullanarak bir dosya isteyebilir, form gönderebilir veya dosya yükleyebilir.

Application Layer en üst katmandır ve günlük kullanımda birçok protocol bu katmanda yer alır.

Layer 7 örnekleri:

- HTTP
    
- FTP
    
- DNS
    
- POP3
    
- SMTP
    
- IMAP
    

---

## Özet

OSI modelini ilk kez okumak zorlayıcı olabilir; ancak networking protocol’leri öğrenildikçe daha anlaşılır hâle gelir. Aşağıdaki tabloda ISO OSI katmanları özetlenmiştir.

|Layer Number|Layer Name|Main Function|Example Protocols and Standards|
|---|---|---|---|
|Layer 7|Application Layer|Application’lara servis sağlama|HTTP, FTP, DNS, POP3, SMTP, IMAP|
|Layer 6|Presentation Layer|Encoding, encryption, compression|Unicode, MIME, JPEG, PNG, MPEG|
|Layer 5|Session Layer|Session yönetimi|NFS, RPC|
|Layer 4|Transport Layer|End-to-end communication|TCP, UDP|
|Layer 3|Network Layer|Logical addressing ve routing|IP, ICMP, IPSec|
|Layer 2|Data Link Layer|Adjacent node’lar arası veri transferi|Ethernet (802.3), WiFi (802.11)|
|Layer 1|Physical Layer|Fiziksel iletim ortamı|Electrical, optical, wireless|