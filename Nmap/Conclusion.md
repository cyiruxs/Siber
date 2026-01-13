Bu odada, herhangi bir ağdaki canlı hostları keşfetmek için **Nmap** kullanmayı öğrendik. Yaygın port tarama türlerini inceledik, servis versiyon numaralarını nasıl bulacağımızı, tarama zamanlamasını nasıl kontrol edeceğimizi ve sonuçları farklı formatlarda nasıl kaydedeceğimizi kapsadık.

Önemli bir hatırlatma olarak; Nmap'i tüm özellikleriyle kullanabilmek için **sudo** yetkileriyle çalıştırmak en iyisidir. Yerel kullanıcı yetkileriyle çalıştırmak mümkün olsa da birçok gelişmiş özellik kullanılamaz hale gelir. Örneğin, sudo yetkiniz varsa Nmap otomatik olarak **SYN scan (`-sS`)** yaparken, yerel kullanıcıda varsayılan olarak **connect scan (`-sT`)** yapar. Bunun nedeni, TCP SYN gibi özel paketlerin oluşturulmasının root yetkisi gerektirmesidir.

Nmap çok zengin bir araçtır ve biz burada en temel özelliklere değindik. İşte öğrendiğimiz tüm seçeneklerin toplu bir özeti:

---

### Nmap Seçenekleri Özeti

| **Kategori**          | **Seçenek**         | **Açıklama**                                                |
| --------------------- | ------------------- | ----------------------------------------------------------- |
| **Host Discovery**    | `-sL`               | **List scan** – Hedefleri taramadan sadece listeler.        |
|                       | `-sn`               | **Ping scan** – Sadece host keşfi yapar, port taramaz.      |
| **Port Scanning**     | `-sT`               | **TCP connect scan** – Üçlü el sıkışmayı tamamlar.          |
|                       | `-sS`               | **TCP SYN** – Üçlü el sıkışmanın sadece ilk adımını atar.   |
|                       | `-sU`               | **UDP Scan** – UDP servislerini tarar.                      |
|                       | `-F`                | **Fast mode** – En yaygın 100 portu tarar.                  |
|                       | `-p[range]`         | Port aralığını belirtir (`-p-` tüm portları tarar).         |
|                       | `-Pn`               | Tüm hostları çevrimiçi kabul eder (keşif aşamasını atlar).  |
| **Service Detection** | `-O`                | **OS detection** – İşletim sistemi tespiti.                 |
|                       | `-sV`               | **Service version detection** – Servis versiyon tespiti.    |
|                       | `-A`                | OS tespiti, versiyon tespiti ve ek özellikleri birleştirir. |
| **Timing**            | `-T<0-5>`           | Zamanlama şablonu (0: Paranoid - 5: Insane).                |
|                       | `--min-parallelism` | Minimum paralel prob sayısı.                                |
|                       | `--min-rate`        | Saniyede gönderilen minimum paket sayısı.                   |
|                       | `--host-timeout`    | Bir hedef host için beklenecek maksimum süre.               |
| **Real-time Output**  | `-v`                | **Verbosity** – Çıktı ayrıntı seviyesi (örn: `-vv`).        |
|                       | `-d`                | **Debugging** – Hata ayıklama seviyesi (örn: `-d9`).        |
| **Reporting**         | `-oN`               | Normal formatta çıktı kaydeder.                             |
|                       | `-oX`               | XML formatında çıktı kaydeder.                              |
|                       | `-oG`               | Grep komutuna uygun formatta çıktı kaydeder.                |
|                       | `-oA`               | Tüm ana formatlarda çıktı kaydeder.                         |