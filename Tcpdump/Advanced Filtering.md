
Paketleri filtrelemenin çok daha fazla yolu vardır. Gerçek hayattaki herhangi bir durumda binlerce hatta milyonlarca paket arasından filtreleme yapmamız gerekir. Görüntülenecek paketleri tam olarak ifade edebilmek vazgeçilmezdir. Örneğin, görüntülenen paketleri belirli bir uzunluktan küçük veya büyük olacak şekilde sınırlandırabiliriz:

- **greater LENGTH**: Uzunluğu belirtilen değerden büyük veya ona eşit olan paketleri filtreler
    
- **less LENGTH**: Uzunluğu belirtilen değerden küçük veya ona eşit olan paketleri filtreler
    

**pcap-filter** kılavuz sayfasını **man pcap-filter** komutunu çalıştırarak incelemeniz önerilir; ancak bu oda kapsamında, TCP flags’a göre paket filtrelemeye imkân tanıyan tek bir gelişmiş seçeneğe odaklanacağız. **TCP flags**’ları anlamak, bu bilgiyi geliştirerek daha ileri seviye filtreleme tekniklerinde ustalaşmayı kolaylaştırır.

---

## Binary Operations

Devam etmeden önce **binary operations** konusuna değinmek gerekir. Bir binary operation bitler üzerinde çalışır; yani sıfırlar ve birler üzerinde. Bir işlem bir veya iki bit alır ve bir bit döndürür. Aşağıda üç binary operation açıklanmaktadır: **&**, **|** ve **!**.

### & (And)

İki bit alır ve her iki girdi de 1 olmadıkça 0 döndürür.

|Input 1|Input 2|Input 1 & Input 2|
|---|---|---|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

### | (Or)

İki bit alır ve her iki girdi de 0 olmadıkça 1 döndürür.

|Input 1|Input 2|Input 1 \| Input 2|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

### ! (Not)

Tek bir bit alır ve tersine çevirir; girdi 1 ise 0, girdi 0 ise 1 döndürür.

|Input 1|! Input 1|
|---|---|
|0|1|
|1|0|

---

## Header Bytes

Bu bölümün amacı, paketleri bir header byte içeriğine göre filtreleyebilmektir. Aşağıdaki protokolleri ele alalım: **ARP**, **Ethernet**, **ICMP**, **IP**, **TCP** ve **UDP**. Bunlar şimdiye kadar incelenmiş bazı network protokolleridir. Tcpdump’a, protokol header byte’larının içeriğine göre paketleri nasıl filtreleyeceğimizi nasıl söyleriz? (Her protokolün header detaylarına girilmeyecektir; bunun yerine TCP flags’a odaklanılacaktır.)

**pcap-filter** kullanarak Tcpdump, header içindeki herhangi bir byte’ın içeriğine aşağıdaki söz dizimiyle erişilmesine izin verir:

```
proto[expr:size]
```

Burada:

- **proto**, protokolü ifade eder. Örneğin; **arp**, **ether**, **icmp**, **ip**, **ip6**, **tcp** ve **udp** sırasıyla ARP, Ethernet, ICMP, IPv4, IPv6, TCP ve UDP protokollerini ifade eder.
    
- **expr**, byte offset’i belirtir; **0**, ilk byte’ı temsil eder.
    
- **size**, ilgilenilen byte sayısını belirtir; bir, iki veya dört olabilir. Opsiyoneldir ve varsayılan olarak **1**’dir.
    

Bunu daha iyi anlamak için **pcap-filter** kılavuz sayfasından iki örnek aşağıda verilmiştir:

- **ether[0] & 1 != 0**  
    Ethernet header’ının ilk byte’ını ve ondalık **1** sayısını (binary olarak `0000 0001`) alır ve **&** (And) işlemini uygular. Sonuç **0**’a eşit değilse true döner. Bu filtrenin amacı, multicast address’e gönderilen paketleri göstermektir. Multicast Ethernet address, aynı veriyi alması amaçlanan bir cihaz grubunu tanımlar.
    
- **ip[0] & 0xf != 5**  
    IP header’ının ilk byte’ını ve hexadecimal **F** sayısını (`0000 1111`) karşılaştırır. Sonuç ondalık **5** (`0000 0101`) sayısına eşit değilse true döner. Bu filtrenin amacı, options içeren tüm IP paketlerini yakalamaktır.
    

Yukarıdaki örnekler karmaşık görünebilir; bunlar yalnızca nelerin mümkün olduğunu göstermek amacıyla verilmiştir. Bu görevi tamamlamak için bu örneklerin tam olarak anlaşılması gerekli değildir. Bunun yerine, TCP paketlerini **TCP flags**’lara göre filtrelemeye odaklanılacaktır.

---

## TCP Flags Filtering

TCP flags alanına erişmek için **tcp[tcpflags]** kullanılabilir. Karşılaştırma için kullanılabilen TCP flags şunlardır:

- **tcp-syn** – TCP SYN (Synchronize)
    
- **tcp-ack** – TCP ACK (Acknowledge)
    
- **tcp-fin** – TCP FIN (Finish)
    
- **tcp-rst** – TCP RST (Reset)
    
- **tcp-push** – TCP Push
    

Buna göre aşağıdaki filtreler yazılabilir:

- **tcpdump "tcp[tcpflags] == tcp-syn"**  
    Yalnızca SYN (Synchronize) flag’i set edilmiş, diğer tüm flag’leri unset olan TCP paketlerini yakalar.
    
- **tcpdump "tcp[tcpflags] & tcp-syn != 0"**  
    En az SYN (Synchronize) flag’i set edilmiş TCP paketlerini yakalar.
    
- **tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"**  
    En az SYN (Synchronize) veya ACK (Acknowledge) flag’i set edilmiş TCP paketlerini yakalar.
    

İhtiyaca göre, aranılan duruma bağlı olarak farklı filtreler yazılabilir.

---