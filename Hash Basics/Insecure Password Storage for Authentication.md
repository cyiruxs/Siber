Hashing'in siber güvenlikte birçok kullanımı vardır. Bu odada iki ana kullanıma odaklanacağız: **parola saklama** (password storage) ve **veri bütünlüğü** (data integrity).1 Kimlik doğrulama (authentication) amacıyla kullanıldığında parola saklamadan bahsetmiş oluruz.

Şunu belirtmek önemlidir: Bu durum, parolanızı açık metin (cleartext) olarak geri almanız gereken **parola yöneticileri** (password managers) için geçerli değildir. Öte yandan, **kimlik doğrulama mekanizmalarının** sadece kullanıcının parolanı bildiğini teyit etmesi yeterlidir, böylece kaynağa erişim izni verilebilir; bu nedenle bu problem parola yöneticilerinden farklıdır.

### Kimlik Doğrulama İçin Güvensiz Parola Saklama Hikayeleri

Çoğu web uygulaması bir noktada kullanıcının parolasını doğrulamak zorundadır. Bu parolaları düz metin (**plaintext**) olarak saklamak çok güvensiz bir güvenlik uygulamasıdır. Muhtemelen veri tabanları sızdırılan şirketlerle ilgili haberler görmüşsünüzdür. Birçok kişinin çevrimiçi bankacılık dahil çeşitli hesaplarında aynı parolayı kullandığı bilindiğinde, bir hesaptaki parolanın sızdırılması diğer tüm hesapların güvenliğini tehlikeye atar.

Parolalar söz konusu olduğunda **üç güvensiz uygulamayı** inceleyeceğiz:

1. Parolaları düz metin (plaintext) olarak saklamak
    
2. Parolaları kullanımdan kaldırılmış (deprecated) bir şifreleme kullanarak saklamak
    
3. Parolaları güvensiz bir hashing algoritması kullanarak saklamak
    

---

#### 1. Parolaları Düz Metin (Plaintext) Olarak Saklamak

Pek çok veri ihlalinde düz metin parolalar sızdırılmıştır. Kali Linux ve diğer birçok ofansif güvenlik dağıtımındaki "**rockyou.txt**" parola listesine muhtemelen aşinasınızdır. Bu parola listesi, sosyal medya uygulamaları ve widget'ları geliştiren RockYou adlı şirketten gelmektedir. Parolalarını **plaintext** olarak saklıyorlardı ve şirket bir veri ihlali yaşadı. Bu metin dosyası 14 milyondan fazla parola içermektedir. `rockyou.txt` dosyasını `/usr/share/wordlists` dizininde bulabilirsiniz.2

**Terminal**

Bash

```
strategos@g5000 /usr/share/wordlists> wc -l rockyou.txt 
14344392 rockyou.txt      
strategos@g5000 /usr/share/wordlists> head rockyou.txt 
123456
12345
123456789
password
iloveyou
princess
1234567
rockyou
12345678
abc123
```

---

#### 2. Güvensiz Bir Şifreleme (Encryption) Algoritması Kullanmak

Adobe'nin kayda değer veri ihlali biraz daha farklıydı. Şirket, parolaların hash değerlerini saklamak için güvenli bir hashing fonksiyonu kullanmak yerine, artık kullanılmayan (deprecated) bir şifreleme formatı kullandı. Ayrıca, parola ipuçları düz metin olarak saklanmıştı ve bazen parolanın kendisini içeriyordu. Sonuç olarak, düz metin parola nispeten hızlı bir şekilde geri elde edilebildi.

---

#### 3. Güvensiz Bir Hash Fonksiyonu Kullanmak

LinkedIn de 2012 yılında bir veri ihlali yaşadı. LinkedIn, kullanıcı parolalarını saklamak için güvensiz bir hashing algoritması olan **SHA-1**'i kullandı. Ayrıca, hiçbir **password salting** (parola tuzlama) kullanılmamıştı. **Password salting**, parolanın hash'lenmeden önce ona rastgele bir değerin (salt/tuz) eklenmesi anlamına gelir.4

---

### 🛡️ Siber Güvenlik ve CTF İpucu

1. Veritabanı Sızıntılarında İlk Adım:

Bir sızma testi veya CTF sırasında ele geçirdiğiniz veri tabanında parolaların nasıl saklandığını anlamak kritiktir. Eğer parolalar hash'lenmişse, kullanılan algoritmayı tanımlamak için hash-identifier veya hashid gibi araçlar kullanabilirsiniz.5

2. RockYou.txt Gücü:

Dünya çapındaki neredeyse tüm Brute Force saldırılarında ve sözlük saldırılarında (Dictionary Attack) rockyou.txt altın standarttır. Eğer bir hedef sistemde zayıf bir parola politikası varsa, bu listenin ilk 10 satırı bile size girişi sağlayabilir.

3. Salting Neden Hayat Kurtarır?

Eğer LinkedIn "salt" kullansaydı, aynı parolaya (örneğin: 123456) sahip 1000 kullanıcının hash değerleri birbirinden farklı olacaktı. Salt kullanılmadığı için saldırganlar "Rainbow Table" kullanarak milyonlarca parolayı anında çözebildiler.

|**Uygulama**|**Güvenlik Durumu**|**Risk**|
|---|---|---|
|**Plaintext**|**Felaket**|Veri tabanını okuyan herkes tüm parolaları görür.|
|**MD5 / SHA-1**|**Zayıf**|GPU güçleri ile saniyeler içinde kırılabilir.|
|**Bcrypt / Argon2**|**Güçlü**|Modern standart; kırmak çok maliyetli ve yavaştır.|
