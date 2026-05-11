## Snort Yapılandırması ve Kural Oluşturma

Snort; yerleşik kural dosyaları, bir yapılandırma dosyası ve diğer yardımcı dosyalara sahiptir. Bunlar `/etc/snort` dizininde saklanır. Snort için en kritik dosya, hangi kural dosyalarının etkinleştirileceğini, hangi ağ aralığının izleneceğini ve diğer ayarları belirlediğiniz `snort.conf` yapılandırma dosyasıdır. Kural dosyaları ise `rules` klasöründe tutulur.

### Snort Dizini İçeriği

Bash

```
ubuntu@tryhackme:~$ ls /etc/snort
classification.config  reference.config  snort.debian.conf
community-sid-msg.map  rules             threshold.conf
gen-msg.map            snort.conf        unicode.map
```

---

### Kural Formatı (Rule Format)

Snort'ta kuralların belirli bir yazım şekli vardır. Örnek bir kural; herhangi bir IP adresi ve porttan gelen, yapılandırma dosyasında tanımlanan ev ağına (**home network**) herhangi bir port üzerinden ulaşan **ICMP** paketlerini (genellikle ping işlemi sırasında kullanılır) tespit eder. Bu trafik algılandığında "Ping Detected" uyarısı oluşturur.

**Kural Bileşenleri:**

- **Action (Eylem):** Kural tetiklendiğinde hangi işlemin yapılacağını belirtir. Bu örnekte, trafik kurala uyduğunda "alert" (uyarı ver) eylemi kullanılmıştır.
    
- **Protocol (Protokol):** Kural ile eşleşen protokolü ifade eder. Ping işlemleri için "ICMP" protokolü kullanılır.
    
- **Source IP (Kaynak IP):** Trafiğin kaynaklandığı IP adresini belirler. Herhangi bir kaynak IP'yi tespit etmek istediğimiz için "any" olarak ayarlanmıştır.
    
- **Source Port (Kaynak Port):** Trafiğin kaynaklandığı portu belirler. Herhangi bir porttan gelebileceği için "any" seçilmiştir.
    
- **Destination IP (Hedef IP):** Uyarıyı tetikleyecek olan hedef IP'yi belirtir. Burada `$HOME_NET` değişkeni kullanılmıştır; bu değişkenin değeri Snort yapılandırma dosyasında tüm ağ aralığımız olarak tanımlanır.
    
- **Destination Port (Hedef Port):** Trafiğin ulaşacağı portu belirtir. "any" olarak ayarlanmıştır.
    

**Rule Metadata (Kural Meta Verileri):** Kuralın sonunda parantez içinde tanımlanır:

1. **Message (msg):** Kural tetiklendiğinde görüntülenecek mesajdır. Tespit edilen faaliyetin türünü belirtmelidir (Örn: "Ping Detected").
    
2. **Signature ID (sid):** Her kuralı diğerlerinden ayıran benzersiz bir tanımlayıcıdır.
    
3. **Rule Revision (rev):** Kuralın revizyon numarasını belirler. Kural her değiştirildiğinde bu numara artırılır.
    

---

### Kural Oluşturma (Rule Creation)

Özel kural dosyasını bir metin düzenleyici ile açalım:

Bash

```
ubuntu@tryhackme:~$ sudo nano /etc/snort/rules/local.rules
```

Dosyaya aşağıdaki kuralı ekleyin ve kaydedin (Ctrl+X, ardından Y): `alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)`

---

### Kural Testi (Rule Testing)

Snort'u, kural dosyasında tanımlanan sızmaları tespit etmesi için başlatalım:

Bash

```
ubuntu@tryhackme:~$ sudo snort -q -l /var/log/snort -i lo -A console -c /etc/snort/snort.conf
```

_Not: Eğer loopback arayüzünüzün adı "lo" değilse, doğru isimle değiştirin._

Şimdi kuralın çalışıp çalışmadığını görmek için loopback adresimize ping atalım:

Bash

```
ubuntu@tryhackme:~$ ping 127.0.0.1
```

Eğer kural doğru çalışıyorsa konsolda şu çıktıları görmelisiniz:

Plaintext

```
07/24-10:46:52.401504 [**] [1:10003:1] Loopback Ping Detected [**] [Priority: 0] {ICMP} 127.0.0.1 -> 127.0.0.1
```

---

### PCAP Dosyaları Üzerinde Snort Çalıştırma

Snort, gerçek zamanlı trafiğin yanı sıra geçmişe dönük ağ trafiğinin kaydedildiği **PCAP** dosyaları üzerinde de tespit yapabilir. Bu, adli bilişim (**forensic**) incelemelerinde sızma belirtilerini belirlemek için oldukça kullanışlıdır.

Aşağıdaki komut, bir **PCAP** dosyası üzerinde analiz yapmak için kullanılır:

Bash

```
ubuntu@tryhackme:~$ sudo snort -q -l /var/log/snort -r Task.pcap -A console -c /etc/snort/snort.conf
```