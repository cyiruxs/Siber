# Temel Linux Komutları

## 1. Dosya ve Dizin İşlemleri

### `ls` - Dosya ve klasörleri listeler

Kullanım: `ls [seçenekler] [dizin]`

- `ls -l` → Ayrıntılı listeleme yapar.
- `ls -a` → Gizli dosyaları da gösterir.

### `cd` - Dizine geçiş yapar

Kullanım: `cd [dizin]`

- `cd ..` → Bir üst dizine çıkar.
- `cd /home/user` → Belirtilen dizine gider.

### `pwd` - Mevcut dizini gösterir

Kullanım: `pwd`

### `mkdir` - Yeni bir klasör oluşturur

Kullanım: `mkdir [klasör_adı]`

### `rm` - Dosya veya klasör siler

Kullanım: `rm [dosya_adı]`

- `rm -r [klasör_adı]` → Klasörü ve içindekileri siler.

### `cp` - Dosya veya klasörü kopyalar

Kullanım: `cp [kaynak] [hedef]`

- `cp -r [klasör] [hedef]` → Klasör ve içindekileri kopyalar.

### `mv` - Dosya veya klasörü taşır

Kullanım: `mv [kaynak] [hedef]`

## 2. Dosya İçeriği Görüntüleme

### `cat` - Dosya içeriğini ekrana yazdırır

Kullanım: `cat [dosya_adı]`

### `less` - Büyük dosyaları sayfa sayfa gösterir

Kullanım: `less [dosya_adı]`

### `head` - Dosyanın ilk satırlarını gösterir

Kullanım: `head -n [satır_sayısı] [dosya_adı]`

### `tail` - Dosyanın son satırlarını gösterir

Kullanım: `tail -n [satır_sayısı] [dosya_adı]`

## 3. Kullanıcı ve Yetki İşlemleri

### `whoami` - Geçerli kullanıcıyı gösterir

Kullanım: `whoami`

### `chmod` - Dosya yetkilerini değiştirir

Kullanım: `chmod [yetki] [dosya]`

- `chmod 755 dosya` → Sahip tam yetkili, diğerleri yalnızca okuyabilir.

### `chown` - Dosya sahibini değiştirir

Kullanım: `chown [kullanıcı] [dosya]`

## 4. Sistem ve Süreç Yönetimi

### `ps` - Çalışan işlemleri listeler

Kullanım: `ps aux`

### `kill` - Bir işlemi sonlandırır

Kullanım: `kill [PID]`

- `kill -9 [PID]` → Zorla sonlandırır.

### `top` - Canlı sistem bilgisi gösterir

Kullanım: `top`

## 5. Ağ İşlemleri

### `ping` - Ağ bağlantısını test eder

Kullanım: `ping [hedef]`

### `curl` - URL içeriğini görüntüler

Kullanım: `curl [URL]`

### `wget` - Dosya indirir

Kullanım: `wget [URL]`

## 6. Arşiv ve Sıkıştırma İşlemleri

### `tar` - Dosya ve dizinleri arşivler

Kullanım: `tar -cvf arşiv.tar [klasör/dosya]`

- `tar -xvf arşiv.tar` → Arşivi açar.
- `tar -czvf arşiv.tar.gz [klasör/dosya]` → GZip ile sıkıştırır.

## 7. Disk ve Bellek Yönetimi

### `df` - Disk kullanımını gösterir

Kullanım: `df -h`

### `du` - Dosya veya klasör boyutunu gösterir

Kullanım: `du -sh [klasör/dosya]`

### `free` - RAM kullanımını gösterir

Kullanım: `free -h`

## 8. Güncellemeler ve Paket Yönetimi

### Debian/Ubuntu İçin

- `sudo apt update` → Depo bilgilerini günceller.
- `sudo apt upgrade` → Güncellemeleri yükler.
- `sudo apt install paket_adı` → Paket yükler.

### Arch Linux İçin

- `sudo pacman -Syu` → Sistemi günceller.
- `sudo pacman -S paket_adı` → Paket yükler.

## 9. Operatörler

### `>` - Yönlendirme operatörü (Çıktıyı bir dosyaya kaydeder)

Kullanım: `komut > dosya`

- `ls > liste.txt` → `ls` çıktısını `liste.txt` dosyasına yazar.

### `>>` - Append operatörü (Mevcut dosyanın sonuna ekler)

Kullanım: `komut >> dosya`

- `echo "Yeni satır" >> liste.txt` → `liste.txt` dosyasına ekleme yapar.

### `<` - Girdi yönlendirme operatörü (Bir dosyadan veri alır)

Kullanım: `komut < dosya`

- `wc -l < liste.txt` → `liste.txt` dosyasındaki satır sayısını gösterir.

### `|` - Pipe operatörü (Bir komutun çıktısını başka bir komuta gönderir)

Kullanım: `komut1 | komut2`

- `ls -l | grep "txt"` → `.txt` dosyalarını listeler.

### `&&` - Ve operatörü (Bir komut başarılı olursa diğerini çalıştırır)

Kullanım: `komut1 && komut2`

- `mkdir yeni_klasor && cd yeni_klasor` → `mkdir` başarılı olursa `cd` çalışır.

### `||` - Veya operatörü (Bir komut başarısız olursa diğerini çalıştırır)

Kullanım: `komut1 || komut2`

- `ping -c 1 google.com || echo "Bağlantı yok"` → `ping` başarısız olursa mesaj gösterir.

### `&` - Arka planda çalıştırma operatörü

Kullanım: `komut &`

- `firefox &` → Firefox'u arka planda çalıştırır.

### `;` - Ardışık çalıştırma operatörü

Kullanım: `komut1 ; komut2`

- `echo "Merhaba" ; echo "Dünya"` → Komutları sırayla çalıştırır.

Daha fazla detay için `man [komut]` komutunu kullanabilirsin.