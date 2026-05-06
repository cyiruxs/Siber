Güvenlik görevlerinin çoğunun otomatikleştirilmesine yönelik gelişmelere rağmen, bir **SOC** içerisindeki **People** (İnsan) unsuru her zaman önemli kalacaktır. Bir güvenlik çözümü, bir **SOC** ortamında çok sayıda "kırmızı bayrak" oluşturabilir ve bu da büyük bir gürültüye (**noise**) neden olabilir.

Şehrin tüm yangın alarmlarının entegre olduğu merkezi bir yazılıma sahip bir itfaiye ekibinin parçası olduğunuzu hayal edin. Farz edin ki aynı anda farklı yerler için birçok yangın bildirimi alıyorsunuz. Ekipleriniz bu konumlara ulaştığında, çoğunun sadece yemek pişirmeden kaynaklanan aşırı duman nedeniyle tetiklendiğini fark ediyor. Sonuç olarak, tüm çabalar zaman ve kaynak israfı olacaktır.

Bir **SOC**'da, insan müdahalesi olmadan devrede olan güvenlik çözümleriyle, sonunda daha fazla ilgisiz konuya odaklanmak zorunda kalırsınız. Güvenlik çözümünün gerçekten zararlı faaliyetleri tanımlamasına ve hızlı bir yanıt verilmesine yardımcı olanlar her zaman **People** (İnsanlar) dır.

**People**, **SOC** ekibi olarak bilinir. Bu ekibin aşağıdaki rolleri ve sorumlulukları vardır:

---

### SOC Rolleri ve Sorumlulukları

- **SOC Analyst (Level 1):** Güvenlik çözümü tarafından tespit edilen her şey ilk olarak bu analistlerin elinden geçer. Bunlar, herhangi bir tespite karşı ilk müdahale ekipleridir (**first responders**). **SOC Level 1** Analistleri, belirli bir tespitin zararlı olup olmadığını belirlemek için temel **alert triage** (uyarı önceliklendirme) işlemini gerçekleştirirler. Ayrıca bu tespitleri uygun kanallar aracılığıyla raporlarlar.
    
- **SOC Analyst (Level 2):** **Level 1** birinci seviye analizi yaparken, bazı tespitler daha derinlemesine inceleme gerektirebilir. **Level 2** Analistleri, incelemelere daha derinlemesine dalmalarına ve uygun bir analiz gerçekleştirmek için birden fazla veri kaynağından gelen verileri ilişkilendirmelerine (**correlate**) yardımcı olur.
    
- **SOC Analyst (Level 3):** **Level 3** Analistleri, tehdit göstergelerini (**threat indicators**) proaktif olarak arayan ve olay yanıtı (**incident response**) faaliyetlerinde destek sağlayan deneyimli profesyonellerdir. **Level 1** ve **Level 2** Analistleri tarafından rapor edilen kritik öneme sahip tespitler, genellikle **containment** (sınırlama), **eradication** (ortadan kaldırma) ve **recovery** (iyileştirme) dahil olmak üzere ayrıntılı yanıtlar gerektiren güvenlik olaylarıdır. İşte burada **Level 3** analistlerinin deneyimi işe yarar.
    
- **Security Engineer:** Tüm analistler güvenlik çözümleri üzerinde çalışır. Bu çözümlerin dağıtımı (**deployment**) ve yapılandırılması (**configuration**) gerekir. **Security Engineer**'lar (Güvenlik Mühendisleri), sorunsuz çalışmalarını sağlamak için bu güvenlik çözümlerini kurar ve yapılandırır.
    
- **Detection Engineer:** Güvenlik kuralları (**Security rules**), zararlı faaliyetleri tespit etmek için güvenlik çözümlerinin arkasında oluşturulan mantıktır. **Level 2** ve **3** Analistleri genellikle bu kuralları oluşturur; ancak **SOC** ekibi bazen bu sorumluluk için bağımsız olarak **detection engineer** rolünden de faydalanabilir.
    
- **SOC Manager:** **SOC Manager**, **SOC** ekibinin izlediği süreçleri yönetir ve destek sağlar. **SOC Manager** ayrıca, kurumun **CISO**'su (**Chief Information Security Officer**) ile iletişimde kalarak ona **SOC** ekibinin mevcut güvenlik duruşu (**security posture**) ve çalışmaları hakkında güncellemeler sunar.