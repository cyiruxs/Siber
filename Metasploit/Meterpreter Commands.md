herhangi bir Meterpreter oturumunda (komut satırında `meterpreter>` şeklinde gösterilir) `help` yazmak, mevcut tüm komutları listeleyecektir.

**Meterpreter Yardım Menüsü**

Bash

```
meterpreter > help

Core Commands
=============

    Command                   Description
    -------                   -----------
    ?                         Help menu
    background                Backgrounds the current session
    bg                        Alias for background
    bgkill                    Kills a background meterpreter script
    bglist                    Lists running background scripts
    bgrun                     Executes a meterpreter script as a background thread
    channel                   Displays information or control active channels
    close                     Closes a channel[...]
```

Meterpreter'ın her versiyonu farklı komut seçeneklerine sahip olacaktır, bu nedenle `help` komutunu çalıştırmak her zaman iyi bir fikirdir. Komutlar, Meterpreter üzerinde bulunan yerleşik araçlardır. Herhangi bir ek betik veya yürütülebilir dosya yüklemeden hedef sistemde çalışırlar.

Meterpreter size üç ana araç kategorisi sunacaktır;

- Yerleşik komutlar
    
- Meterpreter araçları
    
- Meterpreter betikleri
    

`help` komutunu çalıştırırsanız, Meterpreter komutlarının farklı kategoriler altında listelendiğini göreceksiniz.

- Core commands (Çekirdek komutlar)
    
- File system commands (Dosya sistemi komutları)
    
- Networking commands (Ağ komutları)
    
- System commands (Sistem komutları)
    
- User interface commands (Kullanıcı arayüzü komutları)
    
- Webcam commands (Web kamerası komutları)
    
- Audio output commands (Ses çıkışı komutları)
    
- Elevate commands (Yükseltme komutları)
    
- Password database commands (Parola veritabanı komutları)
    
- Timestomp commands (Zaman damgası komutları)
    

Lütfen yukarıdaki listenin, Meterpreter'ın Windows versiyonundaki (windows/x64/meterpreter/reverse_tcp) `help` komutu çıktısından alındığını unutmayın. Bunlar diğer Meterpreter versiyonları için farklı olacaktır.

### Meterpreter Komutları

Çekirdek komutlar, hedef sistemde gezinmek ve etkileşim kurmak için yardımcı olacaktır. Aşağıda en yaygın kullanılanlardan bazıları verilmiştir. Bir Meterpreter oturumu başladıktan sonra `help` komutunu çalıştırarak mevcut tüm komutları kontrol etmeyi unutmayın.

**Core Commands (Çekirdek Komutlar)**

- **background**: Mevcut oturumu arka plana atar
    
- **exit**: Meterpreter oturumunu sonlandırır
    
- **guid**: Oturumun GUID (Globally Unique Identifier) değerini alır
    
- **help**: Yardım menüsünü görüntüler
    
- **info**: Bir Post modülü hakkında bilgi görüntüler
    
- **irb**: Mevcut oturumda etkileşimli bir Ruby kabuğu açar
    
- **load**: Bir veya daha fazla Meterpreter uzantısını yükler
    
- **migrate**: Meterpreter'ı başka bir sürece (process) taşımanıza (migrate) olanak tanır
    
- **run**: Bir Meterpreter betiğini veya Post modülünü yürütür
    
- **sessions**: Hızlı bir şekilde başka bir oturuma geçiş yapar
    

**File System Commands (Dosya Sistemi Komutları)**

- **cd**: Dizini değiştirir
    
- **ls**: Mevcut dizindeki dosyaları listeler (dir de çalışacaktır)
    
- **pwd**: Mevcut çalışma dizinini yazdırır
    
- **edit**: Bir dosyayı düzenlemenize olanak tanır
    
- **cat**: Bir dosyanın içeriğini ekrana gösterir
    
- **rm**: Belirtilen dosyayı siler
    
- **search**: Dosya arar
    
- **upload**: Bir dosya veya dizin yükler
    
- **download**: Bir dosya veya dizin indirir
    

**Networking Commands (Ağ Komutları)**

- **arp**: Ana makinenin ARP (Address Resolution Protocol) önbelleğini görüntüler
    
- **ifconfig**: Hedef sistemde mevcut ağ arayüzlerini görüntüler
    
- **netstat**: Ağ bağlantılarını görüntüler
    
- **portfwd**: Yerel bir portu uzak bir servise yönlendirir
    
- **route**: Yönlendirme tablosunu görüntülemenize ve değiştirmenize olanak tanır
    

**System Commands (Sistem Komutları)**

- **clearev**: Olay günlüklerini (event logs) temizler
    
- **execute**: Bir komut yürütür
    
- **getpid**: Mevcut işlem tanımlayıcısını (PID) gösterir
    
- **getuid**: Meterpreter'ın çalıştığı kullanıcıyı gösterir
    
- **kill**: Bir süreci sonlandırır
    
- **pkill**: Süreçleri isme göre sonlandırır
    
- **ps**: Çalışan süreçleri listeler
    
- **reboot**: Uzak bilgisayarı yeniden başlatır
    
- **shell**: Bir sistem komut kabuğuna (shell) düşer
    
- **shutdown**: Uzak bilgisayarı kapatır
    
- **sysinfo**: İşletim sistemi gibi uzak sistem hakkında bilgi alır
    

**Diğer Komutlar (Bunlar yardım menüsünde farklı menü kategorileri altında listelenecektir)**

- **idletime**: Uzak kullanıcının kaç saniyedir boşta (idle) olduğunu döndürür
    
- **keyscan_dump**: Tuş vuruşu tamponunu dökümler (dump)
    
- **keyscan_start**: Tuş vuruşlarını yakalamaya başlar
    
- **keyscan_stop**: Tuş vuruşlarını yakalamayı durdurur
    
- **screenshare**: Uzak kullanıcının masaüstünü gerçek zamanlı izlemenize olanak tanır
    
- **screenshot**: Etkileşimli masaüstünün ekran görüntüsünü alır
    
- **record_mic**: Varsayılan mikrofondan X saniye boyunca ses kaydeder
    
- **webcam_chat**: Bir görüntülü sohbet başlatır
    
- **webcam_list**: Web kameralarını listeler
    
- **webcam_snap**: Belirtilen web kamerasından anlık görüntü alır
    
- **webcam_stream**: Belirtilen web kamerasından bir video akışı oynatır
    
- **getsystem**: Ayrıcalıklarınızı yerel sistem (local system) düzeyine yükseltmeye çalışır
    
- **hashdump**: SAM veritabanının içeriğini dökümler (dump)
    

Tüm bu komutlar yardım menüsü altında mevcut görünse de, hepsi çalışmayabilir. Örneğin, hedef sistemde bir web kamerası olmayabilir veya uygun bir masaüstü ortamı olmayan bir sanal makine üzerinde çalışıyor olabilir.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

Özellikle `getsystem` ve `hashdump` komutları yetki yükseltme ve parola ele geçirme aşamalarında hayat kurtarır. Eğer `getsystem` hata verirse, sistemde `NT AUTHORITY\SYSTEM` yetkilerine sahip olmadığın veya mevcut exploit'in buna izin vermediği anlamına gelebilir. Bu durumda post-exploitation modülleriyle başka yollar araman gerekir.