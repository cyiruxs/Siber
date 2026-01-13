Nmap, tarama hızını ve zamanlamasını kontrol etmek için çeşitli seçenekler sunar. Taramayı normal hızında çalıştırmak, bir **IDS** (Saldırı Tespit Sistemi) veya diğer güvenlik çözümlerini tetikleyebilir. Bu nedenle, bir taramanın ne kadar hızlı ilerleyeceğini kontrol etmek mantıklıdır.

### Timing Templates (Zamanlama Şablonları)

Nmap size altı farklı zamanlama şablonu sunar ve isimleri her şeyi açıklamaktadır:

- **paranoid (0)**
    
- **sneaky (1)**
    
- **polite (2)**
    
- **normal (3)**
    
- **aggressive (4)**
    
- **insane (5)**
    

Zamanlama şablonunu adıyla veya numarasıyla seçebilirsiniz. Örneğin, en yavaş zamanlamayı seçmek için `-T0` (veya `-T 0`) ya da `-T paranoid` ekleyebilirsiniz.

Aşağıdaki tablo, 100 portu tararken farklı zamanlamaların ne kadar sürdüğüne dair bir fikir vermektedir (sonuçlar ağ kurulumuna göre değişebilir):

|**Zamanlama**|**Toplam Süre**|
|---|---|
|**T0 (paranoid)**|9.8 saat|
|**T1 (sneaky)**|27.53 dakika|
|**T2 (polite)**|40.56 saniye|
|**T3 (normal)**|0.15 saniye|
|**T4 (aggressive)**|0.13 saniye|

Nmap'in paketler arasında ne kadar beklediğini incelediğimizde:

- **T0** modunda Nmap, bir sonraki porta geçmeden önce **5 dakika** bekler.
    
- **T1** modunda bu süre her iki port arasında **15 saniyeye** düşer.
    
- **T2** modunda bekleme süresi **0.4 saniyeye** iner.
    
- Varsayılan olan **T3** modunda ise Nmap, ağın güvenilirliğine göre olabildiğince hızlı çalışır.
    

---

### Gelişmiş Hız ve Paralellik Ayarları

Zamanlama şablonlarının dışında, tarama hızını daha hassas ayarlamak için şu seçenekler kullanılabilir:

- **Paralel Problar:** `--min-parallelism <sayı>` ve `--max-parallelism <sayı>` seçenekleri, aynı anda aktif olan TCP ve UDP port taramalarının (probes) minimum ve maksimum sayısını belirler. Varsayılan olarak Nmap bunu otomatik kontrol eder; paket kaybı varsa sayı düşer, ağ kusursuzsa yüzlerceye çıkabilir.
    
- **Paket Oranı (Rate):** `--min-rate <sayı>` ve `--max-rate <sayı>` seçenekleri, Nmap'in **saniyede gönderdiği paket sayısını** kontrol eder. Belirtilen oran, tek bir hosta değil tüm taramaya uygulanır.
    
- **Host Timeout:** `--host-timeout <süre>` seçeneği, yavaş hostlar veya zayıf ağ bağlantıları için bir hedef hostu ne kadar süre bekleyeceğinizi belirler. Belirlenen süre aşılırsa Nmap o hostu taramayı bırakır.
    

---

### Özet Tablo

|**Seçenek**|**Açıklama**|
|---|---|
|**`-T<0-5>`**|Zamanlama şablonu (0: En yavaş, 5: En hızlı)|
|**`--min-parallelism`** / **`--max-parallelism`**|Paralel olarak gönderilen prob sayısı (min ve max)|
|**`--min-rate`** / **`--max-rate`**|Saniye başına gönderilen paket sayısı (min ve max)|
|**`--host-timeout`**|Bir hedef host için beklenecek maksimum süre|