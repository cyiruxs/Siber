İnsanlar genellikle dijital dünya ile ilişkili her zararlı faaliyeti bir **hacking** girişimi olarak etiketler. Bu doğru olabilir ancak siber güvenlik açısından çok genel bir ifadedir. **Security Incident**'lar (Güvenlik Olayları) farklı türlerde olabilir. Yukarıdaki görevlerde, güvenlik ekibinin analizinden sonra bir **incident** haline gelen bir **true positive alert** örneği görmüştük. Bu **incident**, muhtemelen kötü amaçlı bir ek (**malicious attachment**) ile gelen bir **phishing** e-postasıyla ilgiliydi. Eğer sisteme indirilirse, bu ek zararlı sonuçlara yol açabilir. Bu, bir **incident** türüdür. Bunun dışında çeşitli başka **incident** türleri de mevcuttur. Bu türler bağımsız olarak veya aynı kurban üzerinde hep birlikte gerçekleşebilir.

### Malware Infections (Zararlı Yazılım Enfeksiyonları)

**Malware**, bir sisteme, ağa veya uygulamaya zarar verebilen kötü amaçlı bir programdır. **Incident**'ların çoğunluğu **malware infection**'lar ile ilişkilidir. Her biri benzersiz bir hasar verme potansiyeline sahip farklı **malware** türleri vardır. **Malware infection**'lara çoğunlukla metin, belge, yürütülebilir dosya (**executable**) vb. olabilen dosyalar neden olur.

### Security Breaches (Güvenlik İhlalleri)

**Security Breach**'ler, yetkisiz bir kişinin gizli verilere (görmesini veya sahip olmasını istemediğimiz bir şeye) erişim sağlamasıyla ortaya çıkar. Birçok işletmenin yalnızca yetkili personel tarafından erişilmesi gereken gizli verilerine güvenmesi nedeniyle, **Security Breach**'ler en üst düzeyde öneme sahiptir.

### Data Leaks (Veri Sızıntıları)

**Data leak**'ler, bir bireyin veya kuruluşun gizli bilgilerinin yetkisiz kişilere ifşa olduğu **incident**'lardır. Birçok saldırgan, kurbanlarının itibarını zedelemek için **data leak**'leri kullanır veya bu tekniği kurbanlarını tehdit ederek onlardan ihtiyaç duydukları şeyi almak için kullanır. **Security Breach**'lerin aksine, **data leak**'ler insan hataları veya yanlış yapılandırmalar (**misconfigurations**) nedeniyle kasıtsız olarak da kaynaklanabilir.

### Insider Attacks (İçeriden Gelen Saldırılar)

Bir organizasyonun içerisinden kaynaklanan **incident**'lar, **insider attack** olarak bilinir. Son iş gününde bir USB aracılığıyla tüm ağı enfekte eden memnuniyetsiz bir çalışanı düşünün. Bu, bir **insider attack** örneğidir. Kuruluşunuz içindeki birinin kasıtlı olarak bir saldırı başlatması bu kategoriye girer. İçerideki birinin kaynaklara erişimi dışarıdaki birine göre her zaman daha fazla olduğu için bu saldırılar oldukça tehlikeli olabilir.

### Denial Of Service Attacks (Hizmet Dışı Bırakma Saldırıları)

**Availability** (Erişilebilirlik), siber güvenliğin üç temel direğinden biridir. Savunma amaçlı güvenlik çözümleri ve insanlar sürekli olarak bilgiyi korumanın yollarını bulurlar; aynı zamanda verilerin insanlar için erişilebilir olmasını sağlarlar. Bunun nedeni, bizim için erişilebilir olmayan bir şeyi korumanın hiçbir anlamı olmamasıdır. **Denial of Service** saldırıları veya **DoS** saldırıları, saldırganın bir sistemi/ağı/uygulamayı sahte isteklerle (**false requests**) boğarak sonunda meşru kullanıcılar için erişilemez hale getirdiği **incident**'lardır. Bu durum, isteklere cevap vermek için mevcut olan kaynakların tükenmesi (**exhaustion of resources**) nedeniyle gerçekleşir.

Tüm bu **incident**'ların kurbanı olumsuz etkileme konusunda kendilerine özgü potansiyelleri vardır. Bu **incident**'lar yarattıkları etkinin ciddiyeti (**severity**) açısından birbirleriyle kıyaslanamazlar. Çünkü belirli bir **incident** bir kuruluş için felaket olabilirken, bir diğeri için küçük bir hasara yol açabilir. Örneğin; **XYZ Corp.**, sakladığı bilgiler başkası için kullanışsız olabileceğinden bir **data leak**'ten ağır şekilde etkilenmeyebilir. Ancak, hizmetleri bu web sitesine bağlı olduğu için ana web sitesine yapılacak bir **Denial of Service (DoS)** saldırısı durumunda büyük bir kayıp yaşayabilir.