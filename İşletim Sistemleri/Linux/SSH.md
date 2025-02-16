### **SSH Nedir ve Nasıl Çalışır?**

SSH (**Secure Shell**), uzak bir makineye güvenli bir şekilde bağlanmanı sağlar. Özellikle **uzaktan yönetim**, **dosya transferi**, **port yönlendirme** ve **tünelleme** için kullanılır.

🔹 **Nasıl Çalışır?**

- **İstemci-Sunucu Modeli** ile çalışır. SSH istemcisi, sunucuya bağlanarak şifreli bir oturum açar.
- **TCP 22 Portunu Kullanır** (değiştirilebilir).
- **Kimlik Doğrulama** parola veya **SSH anahtarları** ile yapılır.
- **Şifreleme Algoritmaları** (AES, ChaCha20) sayesinde güvenli veri aktarımı sağlar.

🔹 **SSH Bağlantısı Kurma**

```bash
ssh kullanıcı_adı@sunucu_ip
```

Örnek:

```bash
ssh murat@192.168.1.100
```

Farklı bir port kullanıyorsa:

```bash
ssh -p 2222 murat@192.168.1.100
```

🔹 **Kimlik Doğrulama Yöntemleri**  
1️⃣ **Parola ile giriş** – Basit ama brute force saldırılarına açık.  
2️⃣ **SSH Anahtarları ile giriş** – Daha güvenli, özel ve açık anahtar kullanılır.

```bash
ssh-keygen -t rsa -b 4096
ssh-copy-id murat@192.168.1.100
```

🔹 **SSH Konfigürasyon Dosyası**  
SSH ayarları **`/etc/ssh/sshd_config`** dosyasında bulunur. Önemli parametreler:

```bash
Port 2222               # SSH portunu değiştir  
PermitRootLogin no      # Root kullanıcı girişi kapat  
PasswordAuthentication no  # Yalnızca anahtar doğrulama kullan  
PubkeyAuthentication yes  
```

**Değişikliklerden sonra servisi yeniden başlat:**

```bash
sudo systemctl restart ssh
```

---

### **Siber Güvenlik Açısından SSH**

SSH, hem saldırı (offensive) hem de savunma (defensive) tarafında kritik bir bileşendir.

#### **🔹 SSH'ye Saldırı Teknikleri**

🔸 **Brute Force (Parola Kırma)**  
Zayıf parolalar varsa **Hydra** veya **Medusa** ile brute force yapılabilir:

```bash
hydra -l kullanıcı_adı -P parola_listesi.txt ssh://hedef_ip
```

**Savunma:**

- Fail2Ban kullan
- Parola yerine SSH anahtarı doğrulaması yap
- Port değiştir

🔸 **SSH Key Hijacking (Anahtar Çalma)**  
Root yetkin varsa başka bir kullanıcının SSH anahtarlarını alabilirsin:

```bash
cat /home/kullanici/.ssh/id_rsa
ssh -i id_rsa kullanici@hedef_ip
```

**Savunma:**

- Özel anahtarları şifrele (passphrase)
- SSH anahtarlarını sık değiştir

🔸 **Port Forwarding (Tünelleme ile İç Ağa Sızma)**  
SSH üzerinden ağ içindeki servisleri dışarı açabilirsin:

```bash
ssh -L 8080:127.0.0.1:80 murat@hedef_ip
```

**Savunma:**

- `AllowTcpForwarding no` ayarıyla tünellemeyi kapat

🔸 **SSH Agent Hijacking (Yetkili Oturumları Kullanma)**  
Sistemdeki SSH Agent’ın oturumunu ele geçirerek yetkili kullanıcı gibi işlem yapabilirsin:

```bash
env | grep SSH_AUTH_SOCK
ssh-add -l
```

**Savunma:**

- `ForwardAgent no` ayarını yap
- Oturum kapatılınca agent’ı temizle

---

### **SSH Güvenliği İçin Alınması Gereken Önlemler**

✅ **Port değiştir:** `/etc/ssh/sshd_config` dosyasında `Port 2222` gibi farklı bir değer kullan.  
✅ **Parola girişlerini devre dışı bırak:** `PasswordAuthentication no` ve `PubkeyAuthentication yes` ayarla.  
✅ **Brute Force engelle:** Fail2Ban ile saldırıları kısıtla:

```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban --now
```

✅ **SSH bağlantılarını izle:**

```bash
sudo cat /var/log/auth.log | grep "Accepted"
```

✅ **İki faktörlü kimlik doğrulama ekle:**

```bash
sudo apt install libpam-google-authenticator
google-authenticator
```

✅ **Sadece belirli IP'leri bağlanmaya izin ver:** `/etc/hosts.allow` içine şu satırı ekle:

```bash
sshd: 192.168.1.0/24
```

SSH’ye saldırmayı ve korumayı bilmek kritik. Offensive tarafında brute force, key hijacking ve port forwarding ile iç ağa erişmeyi dene. Defensive olarak ise yetkilendirme açıklarını kapat, tünelleme ve brute force saldırılarını engelle.asdasdas