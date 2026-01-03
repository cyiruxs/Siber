Emerging tehditlere ayak uydurmak için, **red team engagements** odağı geleneksel **penetration tests**'lerden (sızma testleri) kaydırarak, savunma ekibimizin (defensive team) gerçek bir tehdit aktörünü **tespit etme (detecting)** ve **müdahale etme (responding)** yeteneklerini net bir şekilde görmemizi sağlayan bir sürece dönüştürmek amacıyla tasarlandı. Geleneksel sızma testlerinin yerini almazlar, ancak önlem yerine tespit ve müdahaleye odaklanarak onları tamamlarlar.

**Red teaming** terimi, ordudan ödünç alınmıştır. Askeri tatbikatlarda, bir grup, bilinen düşman stratejilerine karşı savunma ekibinin (genellikle **blue team** olarak bilinir) tepki yeteneklerini test etmek için saldırı tekniklerini simüle etmek amacıyla bir **red team** rolünü üstlenir. Siber güvenlik dünyasına uyarlandığında, **red team engagements**, savunma ekibimizin (blue team) bunlara ne kadar iyi yanıt verdiğini ölçmek ve sonuç olarak mevcut güvenlik kontrollerini geliştirmek için gerçek bir tehdit aktörünün **Taktiklerini, Tekniklerini ve Prosedürlerini (TTPs)** taklit etmekten oluşur.

Her **red team engagement**, kritik bir host'un ele geçirilmesinden hedeften hassas bilgilerin çalınmasına kadar değişen, genellikle **crown jewels** veya **flags** olarak anılan net hedefler tanımlayarak başlar. Genellikle, **blue team**, analizlerinde herhangi bir ön yargıyı önlemek için bu tatbikatlardan haberdar edilmez. **Red team**, hedeflere ulaşmak için mümkün olan her şeyi yaparken, **firewall**, **antivirus**, **EDR**, **IPS** ve diğerleri gibi mevcut güvenlik mekanizmalarını atlatarak tespit edilmeden kalmaya çalışır. Bir **red team engagement**'ta, bir ağdaki tüm host'ların zafiyetler açısından kontrol edilmeyeceğini unutmayın. Gerçek bir saldırganın sadece hedefine giden tek bir yol bulması yeterlidir ve **blue team**'in tespit edebileceği gürültülü taramalar (noisy scans) yapmakla ilgilenmez.

Daha önce olduğu gibi aynı ağı ele alırsak, intranet sunucusunu ele geçirmenin amaç olduğu bir **red team engagement**'ta, diğer host'larla mümkün olduğunca az etkileşimde bulunarak hedefimize ulaşmak için bir yol planlarız. Bu sırada, **blue team**'in saldırıyı tespit etme ve buna uygun şekilde yanıt verme kapasitesi değerlendirilebilir.

Bu tür tatbikatların nihai amacının asla **red team**'in **blue team**'i "yenmesi" olmaması, bunun yerine **blue team**'in devam eden gerçek bir tehdide yeterli şekilde tepki vermeyi öğrenmesi için yeterli TTP'leri simüle etmek olması önemlidir. Gerekirse, tespit yeteneklerini geliştirmeye yardımcı olacak güvenlik kontrollerini düzenleyebilir veya ekleyebilirler.

**Red team engagements** aynı zamanda çeşitli saldırı yüzeylerini (attack surfaces) dikkate alarak geleneksel **penetration tests**'lerden daha iyi performans gösterir:

- **Technical Infrastructure (Teknik Altyapı):** Geleneksel bir sızma testi gibi, bir **red team** de teknik zafiyetleri ortaya çıkarmaya çalışır, ancak gizlilik (stealth) ve kaçınmaya (evasion) çok daha fazla vurgu yapar.
    
- **Social Engineering (Sosyal Mühendislik):** İnsanları **phishing** kampanyaları, telefon aramaları veya sosyal medya aracılığıyla özel olması gereken bilgileri ifşa etmeleri için kandırmayı hedefler.
    
- **Physical Intrusion (Fiziksel İzinsiz Giriş):** Tesislerin kısıtlı alanlarına erişmek için kilit açma (lockpicking), **RFID** klonlama, elektronik erişim kontrol cihazlarındaki zayıflıkları istismar etme gibi teknikleri kullanır.
    

Mevcut kaynaklara bağlı olarak, **red team exercise** (kırmızı takım tatbikatı) çeşitli şekillerde yürütülebilir:

- **Full Engagement (Tam Angajman):** İlk ele geçirmeden nihai hedeflere ulaşılana kadar bir saldırganın tüm iş akışını simüle eder.
    
- **Assumed Breach (İhlal Varsayımı):** Saldırganın zaten bazı varlıklar üzerinde kontrolü ele geçirdiğini varsayarak başlar ve hedeflere oradan ulaşmaya çalışır. Örneğin, **red team**, bazı kullanıcıların **credentials**'larına veya hatta iç ağdaki bir **workstation**'a erişim alabilir.
    
- **Table-top Exercise (Masaüstü Tatbikatı):** Senaryoların, belirli tehditlere teorik olarak nasıl yanıt verileceğini değerlendirmek için **red team** ve **blue team** arasında tartışıldığı, masa başında yapılan bir simülasyondur. Canlı simülasyonların karmaşık olabileceği durumlar için idealdir.
    
