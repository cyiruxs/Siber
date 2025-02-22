Anladım, işte **Linux komutları** ve bunlara ait **parametreler**yle birlikte daha ayrıntılı açıklamalar:

### **📂 Dosya ve Dizin İşlemleri**

1. **`ls`** - Dizin içeriğini listele
    
    - `ls -l` → Detaylı listeleme (izinler, sahiplik vs.)
    - `ls -a` → Gizli dosyaları da listele
    - `ls -lh` → İnsan tarafından okunabilir formatta (boyutları KB, MB vs.) listele
    - `ls -R` → Alt dizinlerle birlikte listele
    - `ls -1` → Her dosyayı yeni bir satırda listele
    
2. **`pwd`** - Mevcut dizini göster
    
    - `pwd` → Şu anki çalışma dizininin tam yolunu göster
3. **`cd`** - Dizin değiştirme
    - `cd /path/to/directory` → Belirtilen dizine geç
    - `cd ..` → Bir üst dizine geç
    - `cd -` → Önceki dizine geri dön
    - `cd ~` → Ana dizine (home) geç
4. **`mkdir`** - Yeni dizin oluştur
    - `mkdir yeni_dizin` → "yeni_dizin" isminde dizin oluştur
    - `mkdir -p /path/to/dizin` → Parantez içindeki tüm ara dizinleri oluşturur (varsa)
    - `mkdir -v yeni_dizin` → Hangi dizinin oluşturulduğunu belirtir
5. **`rm`** - Dosya silme
    - `rm dosya.txt` → Dosyayı sil
    - `rm -r klasör` → Klasörü ve içeriğini sil
    - `rm -f dosya.txt` → Dosyayı zorla sil (onay istemez)
    - `rm -i dosya.txt` → Dosyayı silmeden önce onay ister
    - `rm -v dosya.txt` → Silme işlemine dair bilgi verir
6. **`cp`** - Dosya kopyalama
    - `cp dosya.txt /hedef/` → Dosyayı başka bir dizine kopyala
    - `cp -r klasör/ /hedef/` → Klasörü ve içeriğini kopyala
    - `cp -i dosya.txt /hedef/` → Kopyalama işleminden önce onay ister
    - `cp -u dosya.txt /hedef/` → Yalnızca kaynak dosya hedeften eskiyse kopyalar
7. **`mv`** - Dosya taşıma veya yeniden adlandırma
    - `mv eski.txt yeni.txt` → Dosyayı yeniden adlandır
    - `mv dosya.txt /hedef/` → Dosyayı başka bir dizine taşı
    - `mv -i eski.txt yeni.txt` → Yeniden adlandırma işleminden önce onay ister
    - `mv -u eski.txt yeni.txt` → Dosya hedeften daha eskiyse taşı
8. **`find`** - Dosya arama
    - `find / -name "dosya.txt"` → "dosya.txt" adındaki dosyayı ara
    - `find / -type d` → Yalnızca dizinleri ara
    - `find . -type f -name "*.txt"` → Geçerli dizinde tüm `.txt` dosyalarını ara
    - `find . -size +10M` → 10MB'dan büyük dosyaları bul
    - `find . -user kullanıcı` → Belirtilen kullanıcıya ait dosyaları ara
9. **`file`** - Dosya türünü belirleme
    - `file dosya.txt` → Dosyanın türünü belirle (örneğin, metin, resim, vb.)
    - `file -i dosya.txt` → Dosyanın MIME türünü belirle
    - `file -b dosya.txt` → Dosya adını atlayarak yalnızca tür bilgisini göster
10. **`touch`** - Boş dosya oluşturma veya dosya zaman damgasını güncelleme
    - `touch dosya.txt` → Boş bir dosya oluştur veya mevcut dosyanın zaman damgasını güncelle
    - `touch -c dosya.txt` → Dosya mevcut değilse oluşturma, yalnızca zaman damgasını güncelle
    - `touch -t 202502201200.00 dosya.txt` → Dosyanın zaman damgasını belirtilen tarih ve saate ayarla (örneğin, 20 Şubat 2025, 12:00:00)
    

---

### **📄 Dosya İçeriğini Görüntüleme ve Düzenleme**

1. **`cat`** - Dosyanın içeriğini görüntüleme
    - `cat dosya.txt` → Dosyanın tamamını göster
    - `cat -n dosya.txt` → Satır numarası ile birlikte göster
    - `cat -b dosya.txt` → Boş satırlar hariç satır numarası gösterir
    - `cat -E dosya.txt` → Satır sonlarını `'$'` işaretiyle göster
2. **`tac`** - Dosyanın içeriğini ters sırayla görüntüle
    - `tac dosya.txt` → Dosyanın içeriğini tersten göster
3. **`less`** - Sayfa sayfa görüntüleme
    - `less dosya.txt` → Dosyayı sayfa sayfa göster
    - `less +F dosya.txt` → Gerçek zamanlı dosya görüntüleme (log dosyası izler gibi)
    - `less -N dosya.txt` → Satır numaralarını göstererek görüntüler
    - `less -S dosya.txt` → Uzun satırları kaydırmadan gösterir
4. **`head`** - Dosyanın başını görüntüle
    - `head -n 10 dosya.txt` → İlk 10 satırı göster
    - `head -c 100 dosya.txt` → İlk 100 baytı göster
5. **`tail`** - Dosyanın sonunu görüntüle
    - `tail -n 10 dosya.txt` → Son 10 satırı göster
    - `tail -f dosya.txt` → Dosyayı izleyerek sürekli göster (log izleme)
    - `tail -n +10 dosya.txt` → 10. satırdan itibaren göster
    - `tail -c 100 dosya.txt` → Son 100 baytı göster
6. **`nano`** - Basit bir metin düzenleyici ile dosya açma
    - `nano dosya.txt` → Dosyayı nano editörüyle aç
    - `nano +10 dosya.txt` → 10. satırdan itibaren aç
7. **`vim`** - Gelişmiş metin düzenleyici ile dosya açma
    - `vim dosya.txt` → Dosyayı vim editörüyle aç
    - `vim +10 dosya.txt` → 10. satırdan itibaren aç

---

### **📌 Yetkiler ve Sahiplik İşlemleri**

8. **`chmod`** - Dosya izinlerini değiştirme
    - `chmod 644 dosya.txt` → Dosya için okuma-yazma-okuma izinlerini değiştir
    - `chmod +x dosya.sh` → Dosyaya çalıştırma izni ekle
    - `chmod -R 755 dizin/` → Dizin ve içeriği için izinleri recursive (tekrarlı) değiştir
9. **`chown`** - Dosya sahibini değiştirme
    - `chown kullanıcı:grup dosya.txt` → Dosyanın sahibini değiştir
    - `chown -R kullanıcı:grup dizin/` → Dizin ve altındaki dosyaların sahibini değiştir
10. **`sudo`** - Yetkili kullanıcı olarak komut çalıştırma
    - `sudo komut` → `komut`'u root yetkileriyle çalıştır
    - `sudo -u kullanıcı komut` → Belirtilen kullanıcıyla komut çalıştır
11. **`su`** - Kullanıcı değiştirme
    - `su - kullanıcı` → Belirtilen kullanıcıya geçiş yap
    - `su` → Root kullanıcısına geçiş yap

---

### **🔍 Sistem Bilgileri ve Süreç Yönetimi**

12. **`man`** - Komut hakkında yardım alma
    - `man ls` → `ls` komutunun kullanımını ve parametrelerini göster
    - `man -k "dosya"` → "dosya" ile ilgili tüm komutları ara
13. **`ps`** - Çalışan süreçleri görüntüleme
    - `ps aux` → Sistemdeki tüm süreçleri göster
    - `ps -ef` → Tüm süreçleri göster (daha detaylı)
    - `ps -u kullanıcı` → Belirtilen kullanıcıya ait süreçleri göster
14. **`top`** - Sistem kaynak kullanımını izleme
    - `top` → Gerçek zamanlı sistem izleme (CPU, RAM kullanımı)
    - `top -u kullanıcı` → Belirli kullanıcıya ait süreçleri göster
15. **`htop`** - Daha gelişmiş sistem izleme
    - `htop` → Gerçek zamanlı süreç izleme (daha fazla interaktif özellik)
16. **`kill`** - Süreç sonlandırma
    - `kill PID` → Belirtilen PID numarasına sahip süreci sonlandır
    - `kill -9 PID` → Zorla süreci sonlandır (SYN signal)
    - `killall isim` → Belirtilen isme sahip tüm süreçleri sonlandır
17. **`uptime`** - Sistemin ne kadar süredir çalıştığını göster
    - `uptime` → Sistem açılış süresi ve yük bilgilerini göster
    - `uptime -p` → Sistem açılış süresini daha kısa formatta göster
18. **`free`** - RAM kullanımını göster
    - `free -h` → İnsan tarafından okunabilir formatta RAM bilgisi göster
19. **`df`** - Disk kullanımını göster
    - `df -h` → İnsan tarafından okunabilir formatta disk kullanım bilgisi
    - `df -T` → Dosya sisteminin türünü de göster

20. **`du`** - Dosya veya dizin boyutunu göster
    - `du -sh *` → Geçerli dizindeki tüm dosya ve alt dizinlerin boyutlarını göster
    - `du -h` → İnsan tarafından okunabilir formatta boyutları göster

---

### **🌐 Ağ Komutları**

21. **`ip`** - Ağ yapılandırmasını göster
    - `ip a` → Ağ arayüzlerinin durumunu göster
    - `ip link` → Ağ bağlantılarının durumunu göster
    - `ip addr show` → IP adreslerini göster
22. **`ping`** - Ağ bağlantısını test et
    - `ping google.com` → Google'a ping atarak bağlantıyı test et
    - `ping -c 5 google.com` → Yalnızca 5 ping gönder
23. **`netstat`** - Ağ bağlantılarını listele
    - `netstat -tulnp` → Açık portlar ve çalışan servisler
    - `netstat -r` → Routing tablosunu göster
    - `netstat -i` → Ağ arayüzlerinin istatistiklerini göster
24. **`ss`** - Netstat alternatif komutu
    - `ss -tulnp` → Açık portlar ve çalışan servisler (daha hızlı)
    - `ss -s` → Ağ durumu özetini göster
25. **`wget`** - Web üzerinden dosya indirme
    - `wget URL` → Belirtilen URL'den dosya indir
    - `wget -r URL` → URL'deki tüm bağlantıları recursive olarak indir
26. **`curl`** - Web istekleri gönderme
    - `curl URL` → URL'ye HTTP isteği gönder
    - `curl -O URL` → Dosyayı belirtilen URL'den indir

---
