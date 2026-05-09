## Netfilter ve Linux Güvenlik Duvarı Araçları

**Netfilter**, paket filtreleme, **NAT** ve bağlantı takibi gibi temel **firewall** işlevlerini barındıran **Linux OS** içerisindeki bir çerçevedir (**framework**). Bu çerçeve, ağ trafiğini kontrol etmek için Linux'ta bulunan çeşitli **firewall** araçlarının temelini oluşturur. Bu çerçeveyi kullanan bazı yaygın araçlar şunlardır:

- **iptables:** Birçok Linux dağıtımında en yaygın kullanılan araçtır. Ağ trafiğini kontrol etmek için çeşitli işlevler sağlayan Netfilter çerçevesini kullanır.
    
- **nftables:** Gelişmiş paket filtreleme ve **NAT** yeteneklerine sahip, "iptables" aracının halefidir. Bu da Netfilter çerçevesine dayanır.
    
- **firewalld:** Bu araç da Netfilter çerçevesi üzerinde çalışır ve önceden tanımlanmış kural setlerine sahiptir. Diğerlerinden farklı çalışır ve önceden oluşturulmuş farklı ağ bölgesi (**network zone**) yapılandırmalarıyla birlikte gelir.
    

---

### ufw (Uncomplicated Firewall)

**ufw**, adından da anlaşılacağı gibi, size daha kolay bir arayüz sunarak "iptables" (veya halefi) içindeki karmaşık söz dizimiyle kural oluşturma zorluklarını ortadan kaldırır. Başlangıç seviyesi için daha uygundur. Temel olarak, "iptables" üzerinde ihtiyaç duyduğunuz kuralları **ufw** üzerinden kolay komutlarla tanımlayabilirsiniz; o da bu kuralları arka planda "iptables" üzerinde yapılandıracaktır. Bazı temel **ufw** komutlarına aşağıdan göz atalım.

**Güvenlik duvarının durumunu kontrol etmek için şu komutu kullanabilirsiniz:**

Bash

```
user@ubuntu:~$ sudo ufw status
Status: inactive
```

**Eğer inaktif görünüyorsa, aşağıdaki komutu kullanarak etkinleştirebilirsiniz:**

Bash

```
user@ubuntu:~$ sudo ufw enable
Firewall is active and enabled on system startup
```

_Not: Kapatmak için "enable" yerine "disable" yazmanız yeterlidir._

Aşağıda, bir Linux makinesinden gelen tüm giden bağlantılara izin vermek için oluşturulmuş bir kural bulunmaktadır. Komuttaki **default** ifadesi, belirli bir uygulama için ayrı bir kuralda kısıtlama tanımlamadığımız sürece, tüm giden trafiğe izin veren bir varsayılan politika tanımladığımız anlamına gelir. Komuttaki **outgoing** kelimesini **incoming** ile değiştirerek makinenize gelen trafiğe izin verebilir veya reddedebilirsiniz:

Bash

```
user@ubuntu:~$ sudo ufw default allow outgoing
Default outgoing policy changed to 'allow'
(be sure to update your rules accordingly)
```

Sisteminizdeki herhangi bir portta gelen trafiği reddedebilirsiniz. Diyelim ki gelen **SSH** trafiğini engellemek istiyoruz. Bunu `ufw deny 22/tcp` komutuyla başarabiliriz. Gördüğünüz gibi, önce eylemi (**deny**), ardından portu ve taşıma protokolünü (**22/tcp**) belirttik.

Bash

```
user@ubuntu:~$ sudo ufw deny 22/tcp
Rule added
Rule added (v6)
```

Aktif tüm kuralları numaralandırılmış bir sırayla listelemek için aşağıdaki komutu kullanabilirsiniz:

Bash

```
user@ubuntu:~$ sudo ufw status numbered
     To                         Action      From
     --                         ------      ----
[ 1] 22/tcp                     DENY IN     Anywhere                  
[ 2] 22/tcp (v6)                DENY IN     Anywhere (v6)   
```

Herhangi bir kuralı silmek için, silinecek kural numarasıyla birlikte şu komutu çalıştırın:

Bash

```
user@ubuntu:~$ sudo ufw delete 2
Deleting:
 deny 22/tcp
Proceed with operation (y|n)? y
Rule deleted (v6)
```

Netfilter'ı yönetmek için bu farklı araçlar kullanılabilir. **Linux OS** için doğru aracı seçmek, işletim sistemine aşinalık ve gereksinimleriniz gibi birden fazla faktöre bağlıdır. Bu görevde tanımlanan bazı kuralları oluşturarak ve beklendiği gibi çalışıp çalışmadıklarını test ederek Linux **firewall** bilginizi test edebilirsiniz.