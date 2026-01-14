# Özel Kurallar (Custom Rules) Nedir?

John'un **Single Crack** modunda neler yapabileceğini keşfettiğimizde, bazı iyi kelime evirme (mangling) kalıpları veya parolalarınızın sıklıkla kullandığı ve belirli bir evirme kalıbıyla taklit edilebilecek kalıplar hakkında bazı fikirleriniz oluşmuş olabilir. İyi haber şu ki; John'un dinamik olarak parolalar oluşturmak için kullanacağı kendi kurallarınızı tanımlayabilirsiniz. Bu tür kuralları tanımlama yeteneği, hedefinizin parola yapısı hakkında daha fazla bilgiye sahip olduğunuzda oldukça faydalıdır.

### Yaygın Özel Kurallar (Common Custom Rules)

Birçok organizasyon, sözlük saldırılarıyla (dictionary attacks) mücadele etmek için belirli bir düzeyde parola karmaşıklığı şartı koşar. Diğer bir deyişle, yeni bir hesap oluştururken veya parolanızı değiştirirken `polopassword` gibi bir parola denerseniz, büyük olasılıkla işe yaramayacaktır. Bunun nedeni zorunlu kılınan parola karmaşıklığıdır. Sonuç olarak, parolaların şunların her birinden en az bir karakter içermesi gerektiğini söyleyen bir uyarı alabilirsiniz:

- Küçük harf
    
- Büyük harf
    
- Sayı
    
- Sembol
    

Parola karmaşıklığı iyidir! Ancak, çoğu kullanıcının bu sembollerin yerleşimi konusunda tahmin edilebilir olacağı gerçeğini istismar edebiliriz. Yukarıdaki kriterler için birçok kullanıcı şuna benzer bir şey kullanacaktır:

Polopassword1!

İlk harfi büyük, sonunda bir sayı ve ardından bir sembol gelen bu parolayı düşünün. Değiştiricilerle (büyük harfler veya semboller gibi) başına veya sonuna eklemeler yapılmış bu tanıdık parola kalıbı, insanların parola oluştururken kullandığı ve tekrar kullandığı hatırlanması kolay bir kalıptır. Bu kalıp, parola karmaşıklığı tahmin edilebilirliğini istismar etmemize olanak tanır.

Bu durum parola karmaşıklığı gereksinimlerini karşılar; ancak saldırganlar olarak, kelime listelerimizden dinamik parolalar oluşturmak için bu eklenen öğelerin muhtemel konumlarını bildiğimiz gerçeğini kullanabiliriz.

---

### Özel Kurallar Nasıl Oluşturulur? (How to create Custom Rules)

Özel kurallar `john.conf` dosyasında tanımlanır. Bu dosya TryHackMe Attackbox üzerinde `/opt/john/john.conf` dizininde bulunur. Eğer John'u bir paket yöneticisi kullanarak kurduysanız veya kaynak kodundan derlediyseniz genellikle `/etc/john/john.conf` konumundadır.

Yukarıdaki örneği hedef kalıbımız olarak kullanarak bu özel kuralların sözdizimine (syntax) bakalım. Bu kurallarda devasa düzeyde ayrıntılı kontrol tanımlayabileceğinizi unutmayın.

İlk satır:

[List.Rules:THMRules] ifadesi kuralınızın adını tanımlamak için kullanılır; John argümanı olarak özel kuralınızı çağırmak için bu ismi kullanacaksınız.

Daha sonra kelimenin nerede değiştirileceğini tanımlamak için **Regex benzeri** bir kalıp eşleştirme kullanırız:

- **`Az`**: Kelimeyi alır ve tanımladığınız karakterleri sonuna ekler.
    
- **`A0`**: Kelimeyi alır ve tanımladığınız karakterleri başına ekler.
    
- **`c`**: Karakteri konumsal olarak büyük harfe çevirir.
    

Bunlar, kelimenin neresinde ve neyi değiştirmek istediğinizi tanımlamak için kombinasyon halinde kullanılabilir.

Son olarak, hangi karakterlerin sona, başa veya başka bir yere ekleneceğini tanımlamalıyız. Bunu, kullanılması gereken yerlere köşeli parantez `[ ]` içinde karakter setleri ekleyerek yaparız. Bunlar çift tırnak `" "` içindeki değiştirici kalıpları takip eder. İşte bazı yaygın örnekler:

- **`[0-9]`**: 0-9 arası sayıları içerir.
    
- **`[0]`**: Sadece 0 sayısını içerir.
    
- **`[A-z]`**: Hem büyük hem de küçük harfleri içerir.
    
- **`[A-Z]`**: Sadece büyük harfleri içerir.
    
- **`[a-z]`**: Sadece küçük harfleri içerir.
    
- **`[!]`**: Sadece ! sembolünü içerir.
    

Hepsini bir araya getirirsek, `Polopassword1!` örnek parolasıyla (kelime listemizde `polopassword` kelimesinin olduğunu varsayarak) eşleşecek kurallardan bir kelime listesi oluşturmak için şu şekilde bir kural girişi oluştururuz:

[List.Rules:PoloPassword]

cAz"[0-9][!£$%@]"

Bu kural şunları kullanır:

- **`c`**: İlk harfi büyük yapar.
    
- **`Az`**: Kelimenin sonuna ekleme yapar.
    
- **`[0-9]`**: 0-9 aralığında bir sayı.
    
- **`[!£$%@]`**: Parolayı bu sembollerden biri takip eder.
    

---

### Özel Kuralları Kullanma (Using Custom Rules)

Daha sonra bu özel kuralı `--rule=PoloPassword` bayrağını (flag) kullanarak bir John argümanı olarak çağırabiliriz.

Tam komut olarak:

john --wordlist=[wordlist yolu] --rule=PoloPassword [dosya yolu]

**Jumbo John**, hemen hemen tüm durumlar için değiştiriciler içeren kapsamlı bir özel kural listesine zaten sahiptir. Eğer sözdiziminiz çalışmıyorsa veya takılırsanız, bu kurallara (genellikle satır 678 civarı) bakmayı deneyin.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

1. Verimlilik (Performance):

Devasa wordlist'ler yerine, elindeki küçük bir wordlist'i (hedefe özel kelimeler gibi) bu kurallarla "genişletmek" çok daha etkili bir saldırı yöntemidir. Örneğin bir şirketin adı Polo ise, Polo2024!, Polo123* gibi varyasyonları bu kurallarla saniyeler içinde üretebilirsin.

2. Kural Test Etme:

Kuralının ne üreteceğini görmek için gerçek bir hash kırmaya çalışmadan önce şu komutla test yapabilirsin:

john --wordlist=deneme.txt --rules=PoloPassword --stdout

Bu komut hash kırmaz, sadece kuralın ürettiği tüm parola varyasyonlarını ekrana basar.

| **Değiştirici** | **Pozisyon**    | **Örnek Sonuç (Kelime: polo)** |
| --------------- | --------------- | ------------------------------ |
| `Az"123"`       | Sona ekle       | `polo123`                      |
| `A0"!"`         | Başa ekle       | `!polo`                        |
| `c`             | İlk harfi büyüt | `Polo`                         |
| `cAz"1!"`       | Kombine         | `Polo1!`                       |