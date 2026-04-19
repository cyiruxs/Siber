## Rlwrap

**Rlwrap**, düzenleme klavyesi ve geçmiş (history) özelliklerini sağlamak için **GNU readline** kütüphanesini kullanan küçük bir yardımcı programdır.

### Kullanım Örneği (Bir Netcat Shell'ini Rlwrap ile Geliştirme)

#### Terminal

Bash

```
attacker@kali:~$ rlwrap nc -lvnp 443
listening on [any] 443 ...
```

Bu komut `nc` aracını `rlwrap` ile sarmalar; böyle daha iyi bir etkileşim için ok tuşları ve geçmiş (history) gibi özelliklerin kullanılmasına olanak tanır.

---

## Ncat

**Ncat**, NMAP projesi tarafından dağıtılan Netcat'in geliştirilmiş bir versiyonudur. Şifreleme (**SSL**) gibi ekstra özellikler sağlar.

### Kullanım Örneği (Reverse Shell'leri Dinleme)

#### Terminal

Bash

```
attacker@kali:~$ ncat -lvnp 4444
Ncat: Version 7.94SVN ( https://nmap.org/ncat )
Ncat: Listening on [::]:443
Ncat: Listening on 0.0.0.0:443
```

### Kullanım Örneği (SSL ile Reverse Shell'leri Dinleme)

#### Terminal

Bash

```
attacker@kali:~$ ncat --ssl -lvnp 4444
Ncat: Version 7.94SVN ( https://nmap.org/ncat )
Ncat: Generating a temporary 2048-bit RSA key. Use --ssl-key and --ssl-cert to use a permanent one.
Ncat: SHA-1 fingerprint: B7AC F999 7FB0 9FF9 14F5 5F12 6A17 B0DC B094 AB7F
Ncat: Listening on [::]:443
Ncat: Listening on 0.0.0.0:443
```

`--ssl` seçeneği, listener için SSL şifrelemesini etkinleştirir.

---

## Socat

Bu araç, iki veri kaynağı arasında (bu durumda iki farklı host) bir **socket connection** oluşturmanıza olanak tanıyan bir yardımcı programdır.

### Varsayılan Kullanım Örneği (Reverse Shell Dinleme):

#### Terminal

Bash

```
attacker@kali:~$ socat -d -d TCP-LISTEN:443 STDOUT
2024/09/23 15:44:38 socat[41135] N listening on AF=2 0.0.0.0:443
```

Yukarıdaki komutta; `-d` seçeneği **verbose** çıktıyı etkinleştirmek için kullanılmıştır; tekrar kullanılması (`-d -d`) komutun ayrıntı düzeyini (verbosity) artıracaktır. `TCP-LISTEN:443` seçeneği, gelen bağlantılar için bir **server socket** oluşturarak 443 portunda bir **TCP** listener yaratır. Son olarak, `STDOUT` seçeneği gelen tüm verileri terminale yönlendirir.