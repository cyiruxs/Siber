# Parolaları Saklamak İçin Hashing Kullanımı (Using Hashing to Store Passwords)

Hashing burada devreye girer. Ya parolanın kendisini saklamak yerine, güvenli bir hashing fonksiyonu kullanarak sadece onun hash değerini saklasaydınız? Bu süreç, kullanıcının parolasını asla saklamanıza gerek kalmadığı ve veri tabanınız sızdırılsa bile, bir saldırganın parolanın ne olduğunu bulmak için her bir parolanın hash'ini kırmak (crack) zorunda kalacağı anlamına gelir.

Bununla ilgili tek bir problem vardır. Ya iki kullanıcı aynı parolaya sahipse? Bir hash fonksiyonu her zaman aynı girdiyi aynı çıktıya dönüştüreceği için, her kullanıcı için aynı parola hash'ini saklarsınız. Bu, birisi o hash'i kırarsa, birden fazla hesaba erişim sağlayacağı anlamına gelir. Ayrıca, birinin hash'leri kırmak için bir **Rainbow Table** (Gökkuşağı Tablosu) oluşturabileceği anlamına gelir.

Bir **Rainbow Table**, hash'lerden düz metinlere (plaintext) giden bir arama tablosudur; böylece bir kullanıcının parolasının ne olduğunu sadece hash değerinden hızlıca öğrenebilirsiniz. Bir rainbow table, bir hash'i kırmak için gereken süreyi disk alanı ile takas eder, ancak oluşturulması zaman alır. Rainbow table'ın neye benzediği hakkında fikir edinmek için işte hızlı bir örnek:

|**Hash**|**Password**|
|---|---|
|02c75fb22c75b23dc963c7eb91a062cc|zxcvbnm|
|b0baee9d279d34fa1dfd71aadb908c3f|11111|
|c44a471bd78cc6c2fea32b9fe028d30a|asdfghjkl|
|d0199f51d2728db6011945145a1b607a|basketball|
|dcddb75469b4b4875094e14561e573d8|000000|
|e10adc3949ba59abbe56e057f20f883e|123456|
|e19d5cd5af0378da05f63f891c7467af|abcd1234|
|e99a18c428cb38d5f260853678922e03|abc123|
|fcea920f7412b5da7be0cf42b8c93759|1234567|
|4c5923b6a6fac7b7355f53bfe2b8f8c1|inS3CyourP4$$|

**CrackStation** ve **Hashes.com** gibi web siteleri, salt (tuz) içermeyen hash'ler için hızlı parola kırma sağlamak amacıyla dahili olarak devasa rainbow table'lar kullanır. Sıralanmış bir hash listesinde arama yapmak, hash'i kırmaya çalışmaktan daha hızlıdır.

---

### Rainbow Table'lara Karşı Korunma (Protecting Against Rainbow Tables)

Rainbow table'lara karşı korunmak için parolalara bir **salt** (tuz) ekleriz. Salt, veri tabanında saklanan, rastgele oluşturulmuş bir değerdir ve her kullanıcı için benzersiz olmalıdır. Teoride, tüm kullanıcılar için aynı salt'ı kullanabilirsiniz ancak kopya parolalar hala aynı hash'e sahip olurdu ve o salt ile parolalar için hala bir rainbow table oluşturulabilirdi.

Salt, hash'lenmeden önce parolanın başına veya sonuna eklenir; bu, her kullanıcının aynı parolaya sahip olsa bile farklı bir parola hash'ine sahip olacağı anlamına gelir. **Bcrypt** ve **Scrypt** gibi hash fonksiyonları bu işlemi otomatik olarak halleder. Salt'ların gizli tutulmasına gerek yoktur.

---

### Parolaları Güvenli Bir Şekilde Saklama Örneği (Example of Securely Storing Passwords)

Parolaları saklarken en iyi güvenlik uygulamalarını teşvik eden birçok iyi rehberi çevrimiçi olarak bulabilirsiniz. Lütfen birini benimsemeden önce parolaları saklarken uymanız gereken herhangi bir standart olup olmadığını kontrol edin. Kullanıcı parolalarını saklarken iyi güvenlik uygulamalarını takip eden bu örneği göz önünde bulundurun:

1. **Argon2, Scrypt, Bcrypt** veya **PBKDF2** gibi güvenli bir hashing fonksiyonu seçeriz.
    
2. Parolaya `Y4UV*^(=go_!` gibi benzersiz bir salt ekleriz.
    
3. Parolayı benzersiz salt ile birleştiririz (concatenate). Örneğin, parola `AL4RMc10k` ise, sonuç dizisi `AL4RMc10kY4UV*^(=go_!` olur.
    
4. Birleştirilmiş parola ve salt'ın hash değerini hesaplarız. Bu örnekte, seçilen algoritmayı kullanarak `AL4RMc10kY4UV*^(=go_!` değerinin hash'ini hesaplamanız gerekir.
    
5. Hash değerini ve kullanılan benzersiz salt'ı (`Y4UV*^(=go_!`) saklarız.
    

---

### Parolaları Saklamak İçin Şifreleme Kullanmak (Using Encryption to Store Passwords)

Kimlik doğrulama için parola kaydetme problemini göz önüne aldığımızda, neden tüm bu zahmetli adımlar yerine parolaları şifrelemiyoruz (**encrypt**)? Bunun nedeni, parolaları saklamadan önce şifrelemek için güvenli bir algoritma seçsek bile, kullanılan anahtarı (**key**) hala saklamamız gerekmesidir. Sonuç olarak, eğer birisi anahtarı ele geçirirse, tüm parolaları kolayca deşifre edebilir.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

1. Rainbow Tables vs. Brute Force:

CTF'lerde bir hash ile karşılaştığınızda, elinizdeki hash'i önce CrackStation gibi sitelere sormanız zaman kazandırır. Eğer hash orada "biliniyorsa", bu bir rainbow table eşleşmesidir. Eğer sonuç dönmezse, o zaman Hashcat veya John the Ripper ile kırma işlemine geçmelisiniz.

2. Salt Nerede Durur?

Genellikle sızdırılan veri tabanlarında hash'ler şu formatta görünür: admin:5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8:s4lt_v4lu3. Buradaki üçüncü kısım salt'tır. Kırma işlemi yaparken bu salt değerini kırma aracına (örneğin John the Ripper) tanıtmanız şarttır.

3. Argon2 Farkı:

Eğer bir sistemde Argon2 kullanıldığını görürseniz, bu sistemin modern ve çok güvenli olduğunu anlayabilirsiniz. Argon2 sadece işlemci (CPU) değil, bellek (RAM) maliyetini de artırarak ekran kartlarıyla (GPU) yapılan kırma saldırılarını çok zorlaştırır.