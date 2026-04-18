Hydra, çevrimiçi parola kırma işlemlerinde kullanılan, sistem giriş şifrelerini "hacklemek" için tasarlanmış hızlı ve "brute force" (kaba kuvvet) temelli bir programdır.

Hydra, bir liste üzerinden ilerleyerek belirli kimlik doğrulama servislerine karşı "brute force" saldırıları gerçekleştirebilir. Belirli bir servis (SSH, Web Application Form, FTP veya SNMP) üzerinde birinin parolasını manuel olarak tahmin etmeye çalıştığınızı hayal edin; Hydra, bir parola listesi üzerinden geçerek bu süreci bizim için hızlandırabilir ve doğru parolayı tespit edebilir.

Resmi deposuna göre Hydra, aşağıdaki protokolleri destekler, yani bu protokollere brute force uygulama yeteneğine sahiptir: “Asterisk, AFP, Cisco AAA, Cisco auth, Cisco enable, CVS, Firebird, FTP, HTTP-FORM-GET, HTTP-FORM-POST, HTTP-GET, HTTP-HEAD, HTTP-POST, HTTP-PROXY, HTTPS-FORM-GET, HTTPS-FORM-POST, HTTPS-GET, HTTPS-HEAD, HTTPS-POST, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MEMCACHED, MONGODB, MS-SQL, MYSQL, NCP, NNTP, Oracle Listener, Oracle SID, Oracle, PC-Anywhere, PCNFS, POP3, POSTGRES, Radmin, RDP, Rexec, Rlogin, Rsh, RTSP, SAP/R3, SIP, SMB, SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, TeamSpeak (TS2), Telnet, VMware-Auth, VNC ve XMPP.”

Hydra'daki her bir protokolün seçenekleri hakkında daha fazla bilgi için Kali Hydra araç sayfasını kontrol edebilirsiniz.

Bu durum, güçlü bir parola kullanmanın önemini göstermektedir; eğer parolanız yaygınsa, özel karakterler içermiyorsa ve sekiz karakterin üzerinde değilse, tahmin edilmeye açık olacaktır. Yüz milyonluk bir parola listesi yaygın parolaları içerir, bu nedenle hazır bir uygulama (out-of-the-box) giriş için kolay bir parola kullanıyorsa, bunu varsayılan halinden değiştirin! CCTV kameraları ve web framework'leri genellikle varsayılan giriş bilgileri olarak `admin:password` ikilisini kullanır ki bu açıkça yeterince güçlü değildir.

---

# 🛠️ Hydra Tool Notes

## 📌 Tanım ve İşlev

- **Hydra:** Çevrimiçi parola kırma (online password cracking) ve hızlı sistem girişi "hacking" aracıdır.
    
- **Mekanizma:** Belirli kimlik doğrulama servislerine (SSH, FTP, vb.) karşı bir liste kullanarak **Brute Force** saldırıları yürütür.
    

## 🌐 Desteklenen Protokoller

Hydra oldukça geniş bir yelpazede brute force desteği sunar:

|**Kategori**|**Protokoller**|
|---|---|
|**Dosya/Veri Transferi**|FTP, SMB, AFP, CVS, Subversion|
|**Web Servisleri**|HTTP(S)-FORM-GET, HTTP(S)-FORM-POST, HTTP(S)-GET, HTTP(S)-PROXY|
|**Veritabanları**|MYSQL, MONGODB, MS-SQL, ORACLE, POSTGRES, FIREBIRD|
|**Uzaktan Erişim**|SSH, RDP, TELNET, VNC, Rlogin, Rsh|
|**E-Posta**|IMAP, POP3, SMTP|
|**Diğer**|SNMP, ICQ, IRC, LDAP, SIP, Cisco AAA|

## 🛡️ Güvenlik Çıkarımları

- **Zayıf Parolalar:** 8 karakterden kısa, özel karakter içermeyen ve yaygın listelerde bulunan parolalar yüksek risk taşır.
    
- **Varsayılan Ayarlar:** CCTV kameraları ve web framework'leri sıklıkla `admin:password` gibi zayıf default bilgilerle gelir.
    
- **Önlem:** Uygulama kurulumu sonrası varsayılan parolalar (default credentials) mutlaka değiştirilmelidir.