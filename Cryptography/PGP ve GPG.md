**PGP** (Pretty Good Privacy), dosyaları şifrelemek, dijital imzalama yapmak ve daha fazlası için kullanılan bir yazılımdır. **GnuPG** veya **GPG**, OpenPGP standartlarının açık kaynaklı bir uygulamasıdır.

**GPG**, özellikle e-posta mesajlarının gizliliğini korumak için yaygın olarak kullanılır. Ayrıca, bir e-postayı imzalamak ve içeriğinin değiştirilmediğini (bütünlüğünü) doğrulamak için de tercih edilir.

---

## GPG Anahtar Oluşturma

Aşağıdaki terminal çıktısında, bir GPG anahtar çifti oluşturma süreci görülmektedir. Bu süreçte şifreleme algoritması, kullanım amacı (sadece imzalama veya hem imzalama hem şifreleme) ve anahtarın geçerlilik süresi gibi bilgiler seçilir:

**Terminal**

Bash

```
root@TryHackMe# gpg --full-gen-key
gpg (GnuPG) 2.4.4; Copyright (C) 2024 g10 Code GmbH

Lütfen istediğiniz anahtar türünü seçin:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sadece imzalama)
   (4) RSA (sadece imzalama)
   (9) ECC (imzalama ve şifreleme) *varsayılan*
Seçiminiz? 9

Lütfen hangi eliptik eğriyi (elliptic curve) istediğinizi seçin:
   (1) Curve 25519 *varsayılan*
Seçiminiz? 1

Anahtarın ne kadar süre geçerli olacağını belirtin.
         0 = anahtarın süresi dolmaz
Anahtar ne kadar süre geçerli olsun? (0) 0
Bu doğru mu? (y/N) y

GnuPG, anahtarınızı tanımlamak için bir kullanıcı kimliği (User ID) oluşturmalıdır.

Gerçek isim: strategos
E-posta adresi: strategos@tryhackme.thm
[...]
pub   ed25519 2024-08-29 [SC]
      AB7E6AA87B6A8E0D159CA7FFE5E63DBD5F83D5ED
uid                      Strategos <strategos@tryhackme.thm>
sub   cv25519 2024-08-29 [E]
```

---

## CTF'lerde GPG ve Şifre Kırma

CTF (Capture The Flag) yarışmalarında dosyaları deşifre etmek için GPG kullanmanız gerekebilir. PGP/GPG özel anahtarları (private keys), tıpkı SSH anahtarlarında olduğu gibi bir **passphrase** (parola) ile korunabilir.

- Eğer anahtar bir parola ile korunuyorsa, **John the Ripper** ve **gpg2john** araçlarını kullanarak bu parolayı kırmayı deneyebilirsiniz.
    
- Anahtar korumasız ise doğrudan deşifre işlemine geçebilirsiniz.
    

---

## Pratik Kullanım: İçe Aktarma ve Deşifre Etme

GPG anahtar çiftinizi oluşturduktan sonra, **public key**'inizi (açık anahtar) kişilerinizle paylaşırsınız. Birisi size güvenli bir mesaj göndermek istediğinde, bunu sizin açık anahtarınızla şifreler. Siz de bu mesajı sadece kendi **private key**'iniz (özel anahtar) ile çözebilirsiniz.

Anahtarlarınızı yeni bir bilgisayara taşımak veya yedekten geri yüklemek oldukça basittir:

1. Anahtarı İçe Aktarma: Yedeklediğiniz anahtarı sisteme tanıtmak için şu komutu kullanırsınız:
    
    gpg --import backup.key
    
2. Dosya Deşifre Etme: Şifreli bir dosyayı (örneğin confidential_message.gpg) çözmek için şu komutu kullanırsınız:
    
    gpg --decrypt confidential_message.gpg
    

---

### Özet Tablo

| **Komut**               | **Açıklama**                                         |
| ----------------------- | ---------------------------------------------------- |
| `gpg --full-gen-key`    | Detaylı parametrelerle yeni anahtar çifti oluşturur. |
| `gpg --import [dosya]`  | Mevcut bir anahtarı GPG anahtarlığına ekler.         |
| `gpg --decrypt [dosya]` | Şifreli dosyayı çözer ve içeriği görüntüler.         |
| `gpg --list-keys`       | Sistemdeki mevcut anahtarları listeler.              |