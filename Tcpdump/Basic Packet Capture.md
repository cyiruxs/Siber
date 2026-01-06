
Tcpdump herhangi bir argüman vermeden çalıştırılabilir; ancak bu yalnızca aracın kurulu olup olmadığını test etmek için faydalıdır. Gerçek senaryolarda, neyin dinleneceği, nereye yazılacağı ve paketlerin nasıl görüntüleneceği mutlaka belirtilmelidir.

---

## Specify the Network Interface

İlk olarak, hangi network interface’in dinleneceğine **-i INTERFACE** ile karar verilmelidir. Tüm mevcut arayüzleri dinlemek için **-i any** kullanılabilir; alternatif olarak **-i eth0** gibi belirli bir arayüz seçilebilir.

Mevcut network interface’leri listelemek için **ip address show** (veya kısaca **ip a s**) komutu kullanılabilir. Aşağıdaki terminal çıktısında, loopback adresine ek olarak **ens5** adlı bir network kartı görülmektedir.

```text
user@TryHackMe$ ip a s
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
[...]
2: ens5: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
[...]
```

---

## Save the Captured Packets

Birçok durumda yakalanan paketlerin daha sonra tekrar incelenmesi gerekir. Bu, **-w FILE** kullanılarak paketlerin bir dosyaya kaydedilmesiyle sağlanır. Dosya uzantısı genellikle **.pcap** olarak kullanılır. Kaydedilen paketler daha sonra **Wireshark** gibi başka bir programla incelenebilir. **-w** seçeneği kullanıldığında paketler ekranda akmaz.

---

## Read Captured Packets from a File

Tcpdump, **-r FILE** kullanılarak bir dosyadan paket okumak için kullanılabilir. Bu, protokol davranışlarını öğrenmek için oldukça faydalıdır. Belirli bir protokolü incelemek amacıyla uygun bir zaman aralığında network trafiği yakalanabilir, ardından yakalanan dosya okunarak filtreler uygulanabilir. Ayrıca, daha önce gerçekleşmiş bir network saldırısını içeren bir packet capture dosyası analiz edilebilir.

---

## Limit the Number of Captured Packets

Yakalanacak paket sayısı **-c COUNT** ile sınırlandırılabilir. Paket sayısı belirtilmezse, yakalama işlemi **CTRL-C** ile durdurulana kadar devam eder. Amaca bağlı olarak yalnızca sınırlı sayıda paket yeterli olabilir.

---

## Don’t Resolve IP Addresses and Port Numbers

Tcpdump, mümkün olduğunda IP adreslerini çözümler ve domain isimlerini yazdırır. Bu tür DNS sorgularını engellemek için **-n** argümanı kullanılabilir. Benzer şekilde, port numaralarının (örneğin 80’in http olarak) çözümlenmesini istemiyorsanız **-nn** kullanılabilir. Aşağıdaki örnekte, IP adresleri çözümlenmeden beş paket yakalanmış ve görüntülenmiştir.

```text
user@TryHackMe$ sudo tcpdump -i ens5 -c 5 -n
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on ens5, link-type EN10MB (Ethernet), capture size 262144 bytes
08:55:18.989213 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 2888580014:2888580210, ack 771262362, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989446 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 196:424, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 228
08:55:18.989576 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 424:620, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989839 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 620:816, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
08:55:18.989958 IP 10.10.117.2.22 > 10.11.81.126.53378: Flags [P.], seq 816:1012, ack 1, win 922, options [nop,nop,TS val 3216251159 ecr 33295823], length 196
5 packets captured
6 packets received by filter
0 packets dropped by kernel
```

---

## Produce (More) Verbose Output

Paketler hakkında daha fazla detay yazdırmak için **-v** kullanılabilir. **man tcpdump** sayfasına göre **-v**, IP paketlerinde “time to live, identification, total length ve options” bilgilerini yazdırır. **-vv** daha ayrıntılı çıktı üretir; **-vvv** ise daha da fazla ayrıntı sağlar.

---

## Summary and Examples

Aşağıdaki tablo, ele alınan komut satırı seçeneklerinin özetini sunmaktadır.

|Command|Explanation|
|---|---|
|tcpdump -i INTERFACE|Belirli bir network interface üzerinde paket yakalar|
|tcpdump -w FILE|Yakalanan paketleri bir dosyaya yazar|
|tcpdump -r FILE|Bir dosyadan paket okur|
|tcpdump -c COUNT|Belirli sayıda paket yakalar|
|tcpdump -n|IP adreslerini çözümlemez|
|tcpdump -nn|IP adreslerini ve protokol numaralarını çözümlemez|
|tcpdump -v|Verbose çıktı; **-vv** ve **-vvv** ile artırılabilir|

---

### Examples

- **tcpdump -i eth0 -c 50 -v**  
    eth0 interface’i üzerinden 50 paket yakalar ve verbose olarak görüntüler.
    
- **tcpdump -i wlo1 -w data.pcap**  
    wlo1 (WiFi) interface’i üzerinden paket yakalar ve data.pcap dosyasına yazar. Kullanıcı **CTRL-C** ile durdurana kadar devam eder.
    
- **tcpdump -i any -nn**  
    Tüm interface’ler üzerinde paket yakalar ve domain adı veya protokol çözümlemesi yapmadan ekranda görüntüler.
    

---