# Hashing Temelleri (Hashing Basics)

Hash fonksiyonları şifrelemeden (encryption) farklıdır. Bir anahtar (key) yoktur ve çıktıdan girdiye geri dönmek imkansız (veya hesaplama açısından imkansız derecede zordur) olması amaçlanmıştır.

### Hash Fonksiyonu Nedir?

Bir hash fonksiyonu, herhangi bir boyuttaki girdi verisini alır ve bu verinin bir özetini (**digest**) oluşturur. Çıktı sabit bir boyuta sahiptir. Herhangi bir girdi için çıktıyı tahmin etmek (veya tersini yapmak) zordur. İyi bir hashing algoritması, hesaplanırken nispeten hızlı olacak ancak geri döndürülürken (yani çıktıdan yola çıkarak girdiyi belirlerken) engelleyici derecede yavaş olacaktır. Girdi verisindeki herhangi bir küçük değişiklik, tek bir bit bile olsa, çıktıda önemli bir değişikliğe neden olmalıdır.

> [!INFO] Avalanche Effect (Çığ Etkisi)
> 
> Girdideki küçük bir değişikliğin çıktıda devasa farklar yaratmasına "Avalanche Effect" denir. Bu, hash algoritmalarının temel güvenlik mekanizmalarından biridir.

Bir örneği inceleyelim. Aşağıdaki terminalde iki dosya görebilirsiniz; birincisi "T" harfini, ikincisi ise "U" harfini içermektedir. Eğer T ve U harflerini bir ASCII tablosunda veya `hexdump` kullanarak kontrol ederseniz, bu iki harfin tek bir bit ile birbirinden ayrıldığını fark edeceksiniz.

- **T** harfi onaltılık (hexadecimal) sistemde `54`'tür, yani ikilik (binary) sistemde `01010100`'dür.
    
- **U** harfi onaltılık sistemde `55`'tir, yani ikilik sistemde `01010101`'dir.
    

Sonuç olarak, aşağıdaki iki dosya birbirinden tek bir bit ile ayrılmaktadır. Ancak, bunların **MD5** (Message-Digest Algorithm 5), **SHA1** (Secure Hash Algorithm 1) veya **SHA-256** (Secure Hash Algorithm 2) hash değerlerini karşılaştırırsak, tamamen farklı olduklarını fark ederiz. Aşağıdaki komutları kendiniz denemenizi öneririz. Dosyalar `~/Hashing-Basics/Task-2/` dizininde bulunmaktadır.

**Terminal Uygulaması**

Bash

```
strategos@g5000 ~> cat file1.txt 
T
strategos@g5000 ~> cat file2.txt 
U
strategos@g5000 ~> hexdump -C file1.txt 
00000000  54                                                |T|
00000001
strategos@g5000 ~> hexdump -C file2.txt 
00000000  55                                                |U|
00000001
strategos@g5000 ~> md5sum *.txt
b9ece18c950afbfa6b0fdbfa4ff731d3  file1.txt
4c614360da93c0a041b22e537de151eb  file2.txt
strategos@g5000 ~> sha1sum *.txt
c2c53d66948214258a26ca9ca845d7ac0c17f8e7  file1.txt
b2c7c0caa10a0cca5ea7d69e54018ae0c0389dd6  file2.txt
strategos@g5000 ~> sha256sum *.txt
e632b7095b0bf32c260fa4c539e9fd7b852d0de454e9be26f24d0d6f91d069d3  file1.txt
a25513c7e0f6eaa80a3337ee18081b9e2ed09e00af8531c8f7bb2542764027e7  file2.txt
```

Bir hash fonksiyonunun çıktısı tipik olarak ham baytlardır (raw bytes) ve bunlar daha sonra kodlanır. Yaygın kodlamalar **base64** veya **hexadecimal** (onaltılık) sistemdir. `md5sum`, `sha1sum`, `sha256sum` ve `sha512sum` çıktılarını onaltılık formatta üretir. Onaltılık formatın, her ham baytı iki onaltılık basamak olarak yazdırdığını unutmayın.

---

### Hashing Neden Önemlidir?

Hashing, interneti günlük kullanımımızda hayati bir rol oynar. Diğer kriptografik fonksiyonlar gibi, hashing de kullanıcıdan gizli kalır. Hashing, verilerin bütünlüğünü (**integrity**) korumaya ve parolanın gizliliğini sağlamaya yardımcı olur.

Siber güvenliğinizi korumak için kullanılan bu hashing örneğini düşünün. TryHackMe'ye giriş yaptığınızda, sunucu parolanızı doğrulamak için hashing kullanır. Aslında, iyi güvenlik uygulamaları gereği, bir sunucu parolanızı kaydetmez; parolanızın **hash değerini** kaydeder. Ne zaman giriş yapmak isterseniz, gönderdiğiniz parolanın hash değerini hesaplar ve kaydedilen hash değeriyle karşılaştırır. Benzer şekilde, bilgisayarınıza giriş yaptığınızda da hashing parolanızı doğrulamada rol oynar. Hashing ile düşündüğünüzden daha fazla dolaylı yoldan ve parola bağlamında neredeyse her gün etkileşime girersiniz.

> [!TIP] Güvenlik Notu: Salting (Tuzlama)
> 
> Sadece hash kullanmak yetmez; çünkü "Rainbow Tables" (önceden hesaplanmış hash tabloları) ile kolayca kırılabilir. Modern sistemler, hash'lemeden önce parolaya rastgele bir veri ekler. Buna Salt denir.

---

### Hash Collision (Hash Çarpışması) Nedir?

Bir **hash collision**, iki farklı girdinin aynı çıktıyı vermesidir. Hash fonksiyonları, çarpışmaları mümkün olduğunca önlemek için tasarlanmıştır. Ayrıca, bir saldırganın kasıtlı olarak bir çarpışma oluşturmasını, yani "mühendisliğini yapmasını" (engineer) engelleyecek şekilde tasarlanmışlardır. Ancak, girdi sayısı pratikte sınırsızken olası çıktı sayısı sınırlı olduğundan, bu durum bir **pigeonhole effect** (güvercin yuvası ilkesi) yaratır.

Sayısal bir örnek olarak, bir hash fonksiyonu 4 bitlik bir hash değeri üretiyorsa, sadece 16 farklı hash değerimiz olur. Olası toplam hash değeri sayısı $2^{\text{bit\_sayısı}} = 2^4 = 16$'dır. Bu durumda bir çarpışma olasılığı nispeten çok yüksektir.

Pigeonhole effect (Güvercin Yuvası İlkesi):

Öğe sayısının (güvercinler) kap sayısından (güvercin yuvaları) daha fazla olması durumunda, bazı kapların birden fazla öğe tutması gerektiğini belirtir. Diğer bir deyişle, bu bağlamda, hash fonksiyonu için sabit sayıda farklı çıktı değeri vardır ancak ona herhangi bir boyutta girdi verebilirsiniz. Girdiler çıktılardan daha fazla olduğu için, bazı girdiler kaçınılmaz olarak aynı çıktıyı vermelidir. Eğer 21 güvercininiz ve 16 güvercin yuvanız varsa, güvercinlerden bazıları yuvaları paylaşacaktır. Sonuç olarak, çarpışmalar kaçınılmazdır. Ancak iyi bir hash fonksiyonu, bir çarpışma olasılığının göz ardı edilebilir olmasını sağlar.

**MD5** ve **SHA1** saldırıya uğramıştır ve artık hash çarpışmaları mühendisliği yapılabildiği için güvensiz kabul edilmektedir. Ancak, henüz hiçbir saldırı her iki algoritmada aynı anda bir çarpışma sağlamamıştır; bu nedenle MD5 ve SHA1 hash değerlerini karşılaştırırsanız farklı olduklarını görürsünüz. MD5 çarpışma örneğini **MD5 Collision Demo** sayfasında inceleyebilir; ayrıca SHA1 çarpışma saldırısının detaylarını **Shattered** üzerinden okuyabilirsiniz. Bunlar nedeniyle, parolaları veya verileri hash'lemek için bu iki algoritmaya da güvenmemelisiniz.

---

### Özet Tablo: Yaygın Hash Algoritmaları

|**Algoritma**|**Çıktı Uzunluğu (Bit)**|**Güvenlik Durumu**|
|---|---|---|
|**MD5**|128 bit|**Güvensiz** (Çarpışmalar kolayca üretiliyor)|
|**SHA-1**|160 bit|**Güvensiz** (Pratik saldırılar mevcut)|
|**SHA-256**|256 bit|**Güvenli** (Modern standart)|
|**SHA-512**|512 bit|**Çok Güvenli**|
