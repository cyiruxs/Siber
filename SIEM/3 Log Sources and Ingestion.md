## Log Kaynakları (Log Sources)

Ağdaki her cihaz; bir kullanıcının web sitesini ziyaret etmesi, **SSH** bağlantısı kurması veya iş istasyonuna giriş yapması gibi bir işlem gerçekleştirildiğinde bir tür **log** oluşturur. Bir ağ ortamında bulunan bazı yaygın cihazların **log**'larının neye benzediğini görelim.

### Windows Makinesi

Windows, **Event Viewer** (Olay Görüntüleyicisi) aracılığıyla görüntülenebilen her olayı kaydeder. Her **log** faaliyeti türüne benzersiz bir kimlik (**Event ID**) atayarak analistin incelemesini ve takibini kolaylaştırır. Tüm Windows uç noktalarından (**endpoints**) gelen bu **log**'lar, izleme ve daha iyi görünürlük için **SIEM** çözümüne iletilir.

### Linux Makinesi

**Linux OS**, olaylar, hatalar ve uyarılar gibi ilgili tüm **log**'ları saklar. Bunlar sürekli izleme için **SIEM**'e aktarılır. Linux'un **log**'ları sakladığı yaygın konumlardan bazıları şunlardır:

- **/var/log/httpd:** HTTP İstek / Yanıt ve hata günlüklerini içerir.
    
- **/var/log/cron:** **Cron job**'lar (zamanlanmış görevler) ile ilgili olaylar burada saklanır.
    
- **/var/log/auth.log** ve **/var/log/secure:** Kimlik doğrulama (**authentication**) ile ilgili günlükleri saklar.
    
- **/var/log/kern:** Kernel (çekirdek) ile ilgili olayları saklar.
    

**Örnek Cron Logu:**

Plaintext

```
May 28 13:04:20 ebr crond[2843]: /usr/sbin/crond 4.4 dillon's cron daemon, started with loglevel notice
May 28 13:04:20 ebr crond[2843]: no timestamp found (user root job sys-hourly)
Jun 13 07:46:22 ebr crond[3592]: unable to exec /usr/sbin/sendmail: cron output for user root job sys-daily to /dev/null
```

### Web Sunucusu

Potansiyel bir web saldırısı girişimine karşı web sunucusuna gelen ve giden tüm isteklerin/yanıtların izlenmesi önemlidir. Linux'ta Apache ile ilgili tüm günlüklerin yazıldığı yaygın konumlar `/var/log/apache` veya `/var/log/httpd` şeklindedir.

**Örnek Apache Logu:**

```
192.168.21.200 - - [21/March/2022:10:17:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.102 Safari/537.36"
127.0.0.1 - - [21/March/2022:10:22:04 -0300] "GET / HTTP/1.0" 200 2216 "-" "curl/7.68.0"
```

---

## Log Ingestion (Log Aktarımı)

Tüm bu **log**'lar zengin bir bilgi birikimi sağlar ve güvenlik sorunlarının tanımlanmasına yardımcı olabilir. Her **SIEM** çözümünün **log**'ları içeri aktarmak için kendine özgü bir yolu vardır. Yaygın kullanılan yöntemlerden bazıları şunlardır:

- **Agent / Forwarder (Aracı / İletici):** Bu **SIEM** çözümleri, uç noktaya yüklenen **Agent** (Splunk tarafında **Forwarder** denir) adında hafif bir araç sağlar. Önemli tüm **log**'ları yakalayıp **SIEM** sunucusuna gönderecek şekilde yapılandırılır.
    
- **Syslog:** Web sunucuları, veritabanları vb. gibi çeşitli sistemlerden veri toplamak ve merkezi hedefe gerçek zamanlı veri göndermek için yaygın olarak kullanılan bir protokoldür.
    
- **Manual Upload (Manuel Yükleme):** **Splunk**, **ELK** gibi bazı **SIEM** çözümleri, kullanıcıların hızlı analiz için çevrimdışı verileri içeri aktarmasına olanak tanır. Veri aktarıldıktan sonra normalize edilir ve analiz için hazır hale getirilir.
    
- **Port-Forwarding (Port Yönlendirme):** **SIEM** çözümleri belirli bir portu dinleyecek şekilde yapılandırılabilir ve ardından uç noktalar verileri o dinleme portu üzerinden **SIEM** örneğine (**instance**) iletir.