## Incident Response Frameworks (Olay Müdahale Çerçeveleri)

Yukarıdaki görevde farklı **incident** türlerini gördük. Bazen bir ortamda çok çeşitli **incident**'larla başa çıkmak zor olabilir. Organizasyonlardaki **incident**'ların farklı doğası nedeniyle, **incident response** (olay müdahale) için yapılandırılmış bir süreç olmalıdır. **Incident Response Frameworks**, etkili müdahale için herhangi bir olayda izlenecek genel yaklaşımları sağlayarak bize bu konuda yardımcı olur. En yaygın kullanılan iki olay müdahale çerçevesini ele alacağız: **SANS** ve **NIST**.

**SANS** ve **NIST**, siber güvenliğe katkıda bulunan popüler kuruluşlardır. SANS, siber güvenlik alanında çeşitli kurslar ve sertifikalar sunarken; **NIST**, siber güvenlik standartları ve yönergeleri geliştirmede rol oynamıştır. Hem SANS hem de **NIST** oldukça benzer olay müdahale çerçevelerine sahiptir.

### SANS Incident Response Framework (PICERL)

SANS olay müdahale çerçevesi 6 aşamadan oluşur; bunları kolayca hatırlamak için baş harflerinden oluşan '**PICERL**' terimi kullanılabilir.

|Aşama|Açıklama|Örnek|
|---|---|---|
|**Preparation** (Hazırlık)|Bu ilk aşamadır. Bir **incident** ile başa çıkmak için gerekli kaynakların oluşturulmasını içerir. Bu kaynaklar; **incident response** ekiplerinin kurulmasını, uygun bir **incident response plan**'ın hazırda bulunmasını ve olaylarla mücadele etmek için gerekli güvenlik çözümlerinin konuşlandırılmasını içerir.|Çalışanlar için **phishing** e-postaları hakkında farkındalık eğitimi düzenlemek. **Phishing** e-postaları, sizi bir **incident**'a yol açabilecek eylemleri gerçekleştirmeye iten dolandırıcı e-postalardır.|
|**Identification** (Tanımlama)|**Identification** aşaması, bir **incident**'a işaret edebilecek herhangi bir anormal davranışın aranmasını ifade eder. Bu, anormal **event**'leri izlemek için çeşitli güvenlik çözümlerinin ve tekniklerinin kullanılmasını içerir.|Güvenlik ekibi, **host**'lardan birinden dışarıya büyük miktarda veri gönderildiğini fark eder. Analiz sonucunda, bir **phishing** e-postası ekinden indirilen kötü amaçlı bir dosyanın ardından sistemin ele geçirildiği (**compromised**) tespit edilir.|
|**Containment** (Kapsama/Sınırlama)|Bir **incident** tanımlandıktan sonraki adım onu kontrol altına almak olmalıdır. Bu, saldırının etkisini en aza indirmek anlamına gelir. Bu genellikle kurban makinenin izole edilmesi, ele geçirilen kullanıcı hesaplarının devre dışı bırakılması vb. ile yapılır.|Güvenlik ekibi, etkiyi en aza indirmek ve saldırganın ele geçirilen **host**'u kullanarak diğer sistemlere sıçramasına (**lateral movement**) izin vermemek için makineyi ağdan izole eder.|
|**Eradication** (Yok Etme)|Bu aşama, adından da anlaşılacağı gibi, tehdidin saldırıya uğrayan ortamdan kaldırılmasını içerir. Tehdit her türlü olabilir. **Eradication** aşaması, ilgili ortamın temiz olduğundan emin olmamızı sağlar ve ardından **recovery** aşamasına geçilebilir.|Kötü amaçlı yazılımı (**malware**) **host**'tan kaldırmak için sistem üzerinde derin bir **malware scan** yürütülür.|
|**Recovery** (Kurtarma)|**Recovery** aşaması bu zincirde çok önemlidir. Etkilenen sistemlerin yedekten (**backup**) kurtarılmasını veya yeniden kurulmasını içerir. Kurtarılan sistemler daha sonra test edilir ve kullanıma hazır hale getirilir.|Ele geçirilen **host** yeniden yapılandırılır ve dışarı sızdırılan (**exfiltrated**) veriler yedekten geri yüklenir.|
|**Lessons Learned** (Çıkarılan Dersler)|Bu da **incident response lifecycle**'ın (olay müdahale yaşam döngüsü) önemli bir parçasıdır. Olayın tespiti ve analizindeki eksiklikler belirlenir ve belgelenir; bu da gelecekteki olaylarda genel sürecin iyileştirilmesine yardımcı olur.|Olayın kök nedenini (**root cause**) analiz etmek ve gelecekteki saldırıları önlemek amacıyla güvenliği artırmak için bir **post-incident review** toplantısı düzenlemek.|

### NIST Incident Response Framework

**NIST**'in Olay Müdahale Çerçevesi, yukarıda incelediğimiz SANS çerçevesine benzer. Bu çerçevede aşama sayısı 4'e indirilmiştir:

1. **Preparation** (Hazırlık)
    
2. **Detection and Analysis** (Tespit ve Analiz)
    
3. **Containment, Eradication, and Recovery** (Kapsama, Yok Etme ve Kurtarma)
    
4. **Post-Incident Activity** (Olay Sonrası Faaliyet)
    

---

### Incident Response Plan (Olay Müdahale Planı)

Organizasyonlar, bu çerçeveleri izleyerek kendi olay müdahale süreçlerini türetebilirler. Her sürecin, ilgili tüm organizasyonel prosedürleri listeleyen resmi bir belgesi vardır. Bu resmi olay müdahale belgesine **Incident Response Plan** denir. Bu yapılandırılmış belge, herhangi bir olay sırasındaki yaklaşımın altını çizer. Üst yönetim tarafından resmi olarak onaylanır ve bir olay öncesinde, sırasında ve sonrasında izlenecek prosedürlerden oluşur.

Bu planın temel bileşenleri şunları içerir (ancak bunlarla sınırlı değildir):

- **Roles and Responsibilities** (Roller ve Sorumluluklar)
    
- **Incident Response methodology** (Olay Müdahale metodolojisi)
    
- Kolluk kuvvetleri dahil olmak üzere paydaşlarla iletişim planı (**Communication plan**)
    
- İzlenecek yükseltme yolu (**Escalation path**)