# Packet Dissection

Packet dissection, protocol dissection olarak da bilinir ve mevcut protocol ve field’ları decode ederek packet ayrıntılarını incelemeyi amaçlar. Wireshark, dissection için uzun bir protocol listesi destekler ve ayrıca kendi dissection script’lerinizi de yazabilirsiniz. Dissection hakkında daha fazla detayı burada bulabilirsiniz.

> **Note:**  
> Bu bölüm, Wireshark’ın packet’leri OSI layer’larını kullanarak nasıl parçalara ayırdığını ve bu layer’ların analiz için nasıl kullanılacağını kapsar. OSI modelinin ne olduğu ve nasıl çalıştığı hakkında zaten temel bilgiye sahip olmanız beklenmektedir.

---

## Packet Details

Packet list pane içinde bir packet’a tıklayarak ayrıntılarını açabilirsiniz (double-click ile ayrıntılar yeni bir pencerede açılır). Packet’lar, OSI modeline bağlı olarak 5 ila 7 layer’dan oluşur. Örnek bir capture içindeki bir HTTP packet üzerinden hepsini inceleyeceğiz.

Herhangi bir detaya tıkladığınızda, packet bytes pane içindeki karşılık gelen bölüm vurgulanır.

Packet details pane incelendiğinde, packet’ta yedi farklı layer olduğu görülür:

- frame/packet  
- source [MAC]  
- source [IP]  
- protocol  
- protocol errors  
- application protocol  
- application data  

Aşağıda bu layer’lar daha ayrıntılı şekilde açıklanmaktadır.

---

## The Frame 

Bu bölüm, baktığınız frame/packet’ın ne olduğunu ve OSI modelinin Physical layer’ına özgü detayları gösterir.

---

## Source [MAC] 

Bu bölüm, OSI modelinin Data Link layer’ından source ve destination MAC Address’leri gösterir.

---

## Source [IP] 

Bu bölüm, OSI modelinin Network layer’ından source ve destination IPv4 Address’leri gösterir.

---

## Protocol 
Bu bölüm, kullanılan protocol (UDP/TCP) ile source ve destination port detaylarını gösterir; OSI modelinin Transport layer’ından gelir.

---

## Protocol Errors

Bu, 4. layer’ın devamıdır ve yeniden birleştirilmesi gereken TCP segment’lerine ait özel bölümleri gösterir.

---

## Application Protocol 

Bu bölüm, HTTP, FTP ve SMB gibi kullanılan protocol’e özgü detayları gösterir. OSI modelinin Application layer’ındandır.

---

## Application Data

5. layer’ın bu uzantısı, application’a özgü verileri gösterebilir.
