## IDS Yayılım Modları (Deployment Modes)

**IDS** (Intrusion Detection System - Saldırı Tespit Sistemi) aşağıdaki şekillerde yaygınlaştırılabilir:

### Host Intrusion Detection System (HIDS)

**Host** tabanlı **IDS** çözümleri, **host**'lara tek tek yüklenir ve yalnızca o belirli **host** ile ilişkili potansiyel güvenlik tehditlerini tespit etmekten sorumludur. **Host** faaliyetlerine dair ayrıntılı görünürlük sağlarlar. Ancak, büyük ağlarda yönetilmeleri zor olabilir; çünkü kaynak yoğundurlar ve her bir **host** üzerinde ayrı yönetim gerektirirler.

### Network Intrusion Detection System (NIDS)

Ağ tabanlı **IDS** çözümleri, belirli **host**'lardan bağımsız olarak tüm ağ içindeki potansiyel kötü amaçlı faaliyetleri tespit etmede kritik öneme sahiptir. Şüpheli faaliyetleri tespit etmek için ilgili tüm **host**'ların ağ trafiğini izlerler. Tüm ağ içindeki tespitlerin merkezi bir görünümünü sağlarlar.

---

## Tespit Modları (Detection Modes)

### Signature-Based IDS (İmza Tabanlı IDS)

Her gün birçok saldırı gerçekleşir. Her saldırının "imza" (**signature**) olarak bilinen kendine özgü bir deseni vardır. Bu imzalar, aynı saldırı gelecekte tekrar gerçekleşirse imzasıyla tespit edilebilmesi ve müdahale için güvenlik yöneticilerine raporlanabilmesi amacıyla **IDS** tarafından veritabanlarında korunur. **IDS**'in imza veritabanı ne kadar güçlüyse, bilinen tehditleri o kadar verimli tespit eder. Ancak, imza tabanlı **IDS**, **zero-day** (sıfırıncı gün) saldırılarını tespit edemez. **Zero-day** saldırılarının önceden belirlenmiş bir imzası yoktur ve **IDS** veritabanlarında kayıtlı değildir. Bu nedenle imza tabanlı **IDS**, yalnızca daha önce gerçekleşmiş ve imzaları veritabanına kaydedilmiş saldırıları tespit edebilir. Gelecek görevlerde, **Snort** adlı imza tabanlı bir **IDS**'i keşfedeceğiz.

### Anomaly-Based IDS (Anomali Tabanlı IDS)

Bu **IDS** türü önce ağın veya sistemin normal davranışını (**baseline**) öğrenir ve normal davranıştan herhangi bir sapma olduğunda tespit gerçekleştirir. Anomali tabanlı **IDS**, tespit için mevcut imzalara dayanmadığından **zero-day** saldırılarını da tespit edebilir. Mevcut durumu normal davranışla (**baseline**) karşılaştırarak ağ veya sistem içindeki anormallikleri tespit ederler. Ancak, bu tür **IDS**'ler çok sayıda **false positive** (zararsız faaliyetleri kötü amaçlı olarak işaretleme) üretebilir; çünkü birçok meşru programın doğası kötü amaçlı olanlarla eşleşebilir. Anomali tabanlı **IDS** bunları kötü amaçlı olarak işaretleyecek ve olağandışı davranan her şeyin kötü amaçlı olduğuna inanacaktır. Anomali tabanlı **IDS** tarafından üretilen **false positive**'leri, ince ayar (**fine-tuning**) yaparak (normal davranışı **IDS** içinde manuel olarak tanımlayarak) azaltabiliriz.

### Hybrid IDS (Hibrit IDS)

Hibrit bir **IDS**, her bir yaklaşımın güçlü yönlerinden yararlanmak için imza tabanlı **IDS** ve anomali tabanlı **IDS**'in tespit yöntemlerini birleştirir. Bazı bilinen tehditlerin **IDS** veritabanında zaten imzaları olabilir; bu durumda hibrit **IDS**, imza tabanlı **IDS**'in tespit tekniğini kullanır. Yeni bir tehditle karşılaşırsa, anomali tabanlı **IDS**'in tespit yönteminden yararlanabilir.

**Özetle:** İmza tabanlı **IDS** tehditleri hızlı bir şekilde tespit edebilirken, diğer **IDS** türleri yüksek işlem yüküne (**processing overhead**) sahip olabilir. Ancak **IDS** seçimini farklı faktörlere göre değerlendirmek esastır. İmza tabanlı **IDS**, küçük bir tehdit yüzeyini kapsamak için iyi bir seçenek olabilir. Anomali tabanlı **IDS** ve hibrit **IDS**, her geçen gün artan ve kuruluşlara büyük zararlar verebilen modern **zero-day** saldırılarını tespit etmeye yardımcı olabilir.