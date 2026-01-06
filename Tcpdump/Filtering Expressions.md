
Tcpdump herhangi bir **filtering expression** belirtmeden çalıştırılabilir; ancak bu faydalı değildir. Tıpkı sosyal bir ortamda herkesin konuşmasını aynı anda dinlemeye çalışmamak gibi, belirli bir kişi ya da konuşmaya odaklanmak gerekir. Network kartımızın gördüğü paket sayısı düşünüldüğünde, her şeyi aynı anda görmek imkânsızdır; bu nedenle yalnızca incelemek istediğimiz trafiği yakalamak için spesifik olmalıyız.

---

## Filtering by Host

Yalnızca network printer’ınızla veya belirli bir game server ile değiş tokuş edilen IP paketleriyle ilgilendiğinizi varsayalım. Yakalanan paketleri **host IP** veya **host HOSTNAME** kullanarak bu host ile sınırlandırabilirsiniz. Aşağıdaki terminal çıktısında, **example.com** ile değiş tokuş edilen tüm paketler yakalanmakta ve **http.pcap** dosyasına kaydedilmektedir. Paket yakalamanın **root** olarak giriş yapmayı veya **sudo** kullanmayı gerektirdiği unutulmamalıdır.

```text
user@TryHackMe$ sudo tcpdump host example.com -w http.pcap
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
16:49:02.482295 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [S], seq 3330895816, win 32120, options [mss 1460,sackOK,TS val 621343956 ecr 0,nop,wscale 7], length 0
16:49:02.635087 IP 93.184.215.14.http > 192.168.139.132.49480: Flags [S.], seq 2231582859, ack 3330895817, win 64240, options [mss 1460], length 0
16:49:02.635125 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [.], ack 1, win 32120, length 0
16:49:02.635491 IP 192.168.139.132.49480 > 93.184.215.14.http: Flags [P.], seq 1:131, ack 1, win 32120, length 130: HTTP: GET / HTTP/1.1
16:49:02.635580 IP 93.184.215.14.http > 192.168.139.132.49480: Flags [.], ack 131, win 64240, length 0
[...]
^C
13 packets captured
25 packets received by filter
0 packets dropped by kernel
```

Belirli bir source IP address veya hostname’den gelen paketlerle sınırlandırmak için **src host IP** veya **src host HOSTNAME** kullanılmalıdır. Benzer şekilde, belirli bir destination’a gönderilen paketleri sınırlamak için **dst host IP** veya **dst host HOSTNAME** kullanılabilir.

---

## Filtering by Port

Tüm DNS trafiğini yakalamak istiyorsanız, paketleri **port 53** ile sınırlandırabilirsiniz. DNS’in varsayılan olarak UDP ve TCP **port 53** kullandığı unutulmamalıdır. Aşağıdaki örnekte, network kartı tarafından okunan tüm DNS sorguları görülmektedir. Terminal çıktısında iki DNS sorgusu yer almaktadır: ilki **example.org** için IPv4 adresini, ikincisi ise IPv6 adresini istemektedir.

```text
user@TryHackMe$ sudo tcpdump -i ens5 port 53 -n
[sudo] password for strategos: 
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
17:26:33.591670 IP 192.168.139.132.47902 > 192.168.139.2.53: 47108+ A? example.org. (29)
17:26:33.591717 IP 192.168.139.132.47902 > 192.168.139.2.53: 5+ AAAA? example.org. (29)
17:26:33.593324 IP 192.168.139.2.53 > 192.168.139.132.47902: 47108 1/0/0 A 93.184.215.14 (45)
17:26:33.593325 IP 192.168.139.2.53 > 192.168.139.132.47902: 5 1/0/0 AAAA 2606:2800:21f:cb07:6820:80da:af6b:8b2c (57)
[...]
^C
12 packets captured
12 packets received by filter
0 packets dropped by kernel
```

Yukarıdaki örnekte, belirli bir port numarasına gönderilen veya bu porttan gelen tüm paketler yakalanmıştır. Belirli bir source port veya destination port için filtreleme yapmak üzere sırasıyla **src port PORT_NUMBER** ve **dst port PORT_NUMBER** kullanılabilir.

---

## Filtering by Protocol

Ele alınacak son filtreleme türü **protocol** bazlı filtrelemedir. Paket yakalama işlemi belirli bir protokol ile sınırlandırılabilir; örnekler arasında **ip**, **ip6**, **udp**, **tcp** ve **icmp** yer alır. Aşağıdaki örnekte, paket yakalama yalnızca **ICMP** paketleriyle sınırlandırılmıştır. Bir **ICMP echo request** ve **echo reply** görülmektedir; bu, birinin **ping** komutunu çalıştırdığının göstergesi olabilir. Ayrıca bir **ICMP time exceeded** paketi de vardır; bu, **traceroute** komutunun çalıştırılmış olmasından kaynaklanabilir.

```text
user@TryHackMe$ sudo tcpdump -i ens5 icmp -n
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
18:11:00.624681 IP 192.168.139.132 > 93.184.215.14: ICMP echo request, id 47038, seq 1, length 64
18:11:00.781482 IP 93.184.215.14 > 192.168.139.132: ICMP echo reply, id 47038, seq 1, length 64
18:11:04.168792 IP 192.168.139.2 > 192.168.139.132: ICMP time exceeded in-transit, length 68
18:11:04.168815 IP 192.168.139.2 > 192.168.139.132: ICMP time exceeded in-transit, length 68
[...]
18:11:14.857188 IP 93.184.215.14 > 192.168.139.132: ICMP 93.184.215.14 udp port 33495 unreachable, length 68
^C
52 packets captured
52 packets received by filter
0 packets dropped by kernel
```

---

## Logical Operators

Kullanışlı olabilecek üç adet logical operator vardır:

- **and**: Her iki koşul da doğruysa paketleri yakalar.  
    Örnek: `tcpdump host 1.1.1.1 and tcp`
    
- **or**: Koşullardan herhangi biri doğruysa paketleri yakalar.  
    Örnek: `tcpdump udp or icmp`
    
- **not**: Koşul doğru değilse paketleri yakalar.  
    Örnek: `tcpdump not tcp`
    

---

## Summary and Examples

Aşağıdaki tablo, ele alınan komut satırı seçeneklerinin özetini sunmaktadır.

|Command|Explanation|
|---|---|
|tcpdump host IP veya tcpdump host HOSTNAME|Paketleri IP adresi veya hostname’e göre filtreler|
|tcpdump src host IP|Paketleri belirli bir source host’a göre filtreler|
|tcpdump dst host IP|Paketleri belirli bir destination host’a göre filtreler|
|tcpdump port PORT_NUMBER|Paketleri port numarasına göre filtreler|
|tcpdump src port PORT_NUMBER|Paketleri belirtilen source port’a göre filtreler|
|tcpdump dst port PORT_NUMBER|Paketleri belirtilen destination port’a göre filtreler|
|tcpdump PROTOCOL|Paketleri protokole göre filtreler (ör. ip, ip6, icmp)|

---

### Examples

- **tcpdump -i any tcp port 22**  
    Tüm interface’lerde dinleme yapar ve **port 22** üzerinden geçen TCP (SSH) trafiğini yakalar.
    
- **tcpdump -i wlo1 udp port 123**  
    WiFi interface’i üzerinde **port 123**’e giden UDP (NTP) trafiğini filtreler.
    
- **tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap**  
    eth0 interface’i üzerinde **example.com** ile TCP **port 443** kullanan trafiği yakalar ve **https.pcap** dosyasına yazar.
    

---

Bu görevdeki sorular için yakalanmış paketler **traffic.pcap** dosyasından okunacaktır. Daha önce belirtildiği gibi, dosyadan okumak için **-r FILE** kullanılır. Test etmek için `tcpdump -r traffic.pcap -c 5 -n` komutu çalıştırılabilir; bu komut IP adreslerini çözümlemeden dosyadaki ilk beş paketi gösterir.

Çıktı satırlarını saymak için çıktı **wc** komutuna pipe edilebilir. Aşağıdaki terminal çıktısında, source IP address’i **192.168.124.1** olan **910** paket bulunduğu görülmektedir. IP çözümlemesinden kaynaklı gecikmeleri önlemek için **-n** kullanılmıştır. Dosyadan okuma işlemi root yetkisi gerektirmediği için **sudo** kullanılmamıştır.

```text
user@TryHackMe$ tcpdump -r traffic.pcap src host 192.168.124.1 -n | wc
reading from file traffic.pcap, link-type EN10MB (Ethernet)
    910   17415  140616
```