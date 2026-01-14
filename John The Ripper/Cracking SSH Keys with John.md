# SSH Anahtar Parolalarını Kırma (Cracking SSH Key Passwords)

Tamam, tamam, duyuyorum sizi. Artık dosya arşivi kalmadı! Güzel! Hadi, CTF (Capture The Flag) mücadelelerinde oldukça sık karşımıza çıkan başka bir John kullanımını inceleyelim: `id_rsa` dosyalarının **SSH private key** (özel anahtar) parolasını kırmak için John'u kullanmak.

Aksi belirtilmedikçe, SSH girişinizi bir parola kullanarak doğrularsınız. Ancak, SSH üzerinden uzak bir makinede oturum açmak için kimlik doğrulama anahtarı olarak özel anahtarınızı (`id_rsa`) kullanmanıza olanak tanıyan **anahtar tabanlı kimlik doğrulamayı** (key-based authentication) yapılandırabilirsiniz. Bunu yapmak genellikle özel anahtara erişmek için bir parola gerektirecektir; burada, anahtarı kullanarak SSH üzerinden kimlik doğrulamasına izin vermek için bu parolayı kırmak amacıyla John'u kullanacağız.

### SSH2John

Kim tahmin edebilirdi, başka bir dönüştürme aracı mı? Pekala, John ile çalışmak tam olarak budur. Adından da anlaşılacağı gibi, **`ssh2john`**, SSH oturumunda oturum açmak için kullanılan `id_rsa` özel anahtarını, John'un üzerinde çalışabileceği bir hash formatına dönüştürür. Şaka bir yana, bu John'un çok yönlülüğünün bir başka güzel örneğidir. Sözdizimi (syntax) beklediğiniz gibidir.

**Not:** Eğer sisteminizde `ssh2john` yüklü değilse, `/opt/john/ssh2john.py` adresinde bulunan `ssh2john.py` dosyasını kullanabilirsiniz. Eğer bunu AttackBox üzerinde yapıyorsanız, `ssh2john` komutunu `python3 /opt/john/ssh2john.py` ile; Kali üzerinde yapıyorsanız `python /usr/share/john/ssh2john.py` ile değiştirin.

**Temel Sözdizimi:** `ssh2john [id_rsa özel anahtar dosyası] > [çıktı dosyası]`

- **ssh2john:** `ssh2john` aracını çağırır.
    
- **[id_rsa private key file]:** Hash'ini almak istediğiniz `id_rsa` dosyasının yoludur.
    
- **`>`**: Çıktı yönlendiricidir; komutun çıktısını başka bir dosyaya yönlendirmek için kullanılır.
    
- **[output file]:** Çıktıyı saklayacak olan dosyadır.
    

**Örnek Kullanım:** `/opt/john/ssh2john.py id_rsa > id_rsa_hash.txt`

---

### Kırma İşlemi (Cracking)

Son kez, `ssh2john` aracından çıkardığımız (örneğimizde `id_rsa_hash.txt` olarak adlandırılan) dosyayı alıyoruz ve tıpkı `rar2john` aracında yaptığımız gibi bunu John ile sorunsuz bir şekilde kullanabiliyoruz:

**Terminal Komutu:** `john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt`

---

### 🛡️ Siber Güvenlik ve CTF İpucu

**1. Dosya İzinleri (Chmod 600):** SSH anahtarının parolasını kırdıktan sonra anahtarı kullanmak istediğinde Linux hata verebilir. SSH anahtarları "fazla açık" izinleri sevmez. Anahtarı kullanmadan önce şu komutu çalıştırmayı unutma: `chmod 600 id_rsa`

**2. Anahtarın Formatı:** `ssh2john`, hem eski (PEM) hem de yeni (OpenSSH) formatlı anahtarları destekler. Ancak bazen anahtarın başında `-----BEGIN OPENSSH PRIVATE KEY-----` yazıyorsa, kırma hızı SHA-512 tabanlı yeni koruma nedeniyle biraz daha yavaş olabilir.

**3. Bağlanma Aşaması:** Parolayı kırdıktan sonra şu komutla bağlanabilirsin: `ssh -i id_rsa kullanici_adi@hedef_ip` _John'un sana bulduğu parolayı, anahtarı kullanırken soracaktır._