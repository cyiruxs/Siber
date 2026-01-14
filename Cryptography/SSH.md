
## Sunucuyu Kimliklendirme (Authenticating the Server)

Eğer daha önce bir **SSH** istemcisi kullandıysanız, aşağıdaki terminal çıktısında yer alan onay istemini biliyorsunuzdur.

**Terminal**

Bash

```
root@TryHackMe# ssh 10.10.244.173
The authenticity of host '10.10.244.173 (10.10.244.173)' can't be established.
ED25519 key fingerprint is SHA256:lLzhZc7YzRBDchm02qTX0qsLqeeiTCJg5ipOT0E/YM8.
This key is not known by any other name.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.244.173' (ED25519) to the list of known hosts.
```

Yukarıdaki etkileşimde, **SSH** istemcisi sunucunun **public key fingerprint** (açık anahtar parmak izi) bilgisini tanıyıp tanımadığımızı doğrular. Bu örnekte dijital imza oluşturma ve doğrulama için kullanılan public-key algoritması **ED25519**'dur.

---

## İstemciyi Kimliklendirme (Authenticating the Client)

Doğru sunucuyla konuştuğumuzu onayladıktan sonra kendimizi tanıtmamız gerekir. Genellikle şifre kullanılır ancak en iyi güvenlik pratiği **SSH anahtar kimlik doğrulamasıdır**. Varsayılan olarak SSH anahtarları **RSA** anahtarlarıdır.

`ssh-keygen`, anahtar çiftleri oluşturmak için kullanılan programdır. Aşağıdaki **manual (man)** sayfasında görüldüğü gibi çeşitli algoritmaları destekler:

**Terminal**

Bash

```
root@TryHackMe# man ssh-keygen
[...]
-t dsa | ecdsa | ecdsa-sk | ed25519 | ed25519-sk | rsa
Oluşturulacak anahtar türünü belirtir. Olası değerler: “dsa”, “ecdsa”, “ecdsa-sk”, “ed25519”, “ed25519-sk” veya “rsa”.
[...]
```

### Örnek Anahtar Çifti Oluşturma

Aşağıda varsayılan seçeneklerle bir anahtar çifti oluşturuyoruz:

**Terminal**

Bash

```
root@TryHackMe# ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/strategos/.ssh/id_ed25519): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/strategos/.ssh/id_ed25519
Your public key has been saved in /home/strategos/.ssh/id_ed25519.pub
[...]
```

Oluşturulan **public key** (`id_ed25519.pub`) ve **private key** (`id_ed25519`) içeriklerine `cat` komutu ile bakalım:

**Terminal**

Bash

```
strategos@g5000:~/.ssh$ cat id_ed25519.pub 
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAINqNMqNhpXZGt6T8Q8bOplyTeldfWq3T3RyNJTmTMJq9 strategos@g5000

strategos@g5000:~/.ssh$ cat id_ed25519
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACDajTKjYaV2Rrek/EPGzqZck3pXX1qt090cjSU5kzCavQAAAJA+E+ajPhPm
owAAAAtzc2gtZWQyNTUxOQAAACDajTKjYaV2Rrek/EPGzqZck3pXX1qt090cjSU5kzCavQ
AAAEB981T2ngdoNm8gEzRU35bGHofqRMjfo5egxl0/9fap/NqNMqNhpXZGt6T8Q8bOplyT
eldfWq3T3RyNJTmTMJq9AAAACm9xYWJAZzUwMDABAgM=
-----END OPENSSH PRIVATE KEY-----
```

---

### SSH Private Keys (Özel Anahtarlar) Hakkında Notlar

- **Gizlilik:** Private key dosyanıza şifreniz (password) gibi davranmalısınız.
    
- **İzinler:** Dosya izinleri sahibi dışında kimsenin okuyamayacağı şekilde ayarlanmalıdır (`600` izni).
    
- **Kullanım:** Bağlanırken belirli bir anahtarı belirtmek için `ssh -i privateKeyDosyaAdi kullanici@host` komutu kullanılır.
    
- **Yetkilendirme:** Sunucu tarafında erişime izin verilen public anahtarlar `~/.ssh/authorized_keys` dosyasında saklanır.