## Güvenlik Çözümleri ve Müdahale Rehberleri

SANS'taki **Identification** ve **NIST**'teki **Detection and Analysis** olarak adlandırılan, olay müdahale yaşam döngüsünün ikinci aşamasını incelediğimizi hatırlayın. Anormal davranışları aramak ve **incident**'ları manuel olarak tanımlamak oldukça zordur. Her biri herhangi bir **incident**'ı tespit etmede kendine özgü roller üstlenen birden fazla güvenlik çözümü mevcuttur. Bunlardan bazıları, **incident**'lara müdahale etme ve yaşam döngüsünün **containment**, **eradication** vb. diğer aşamalarını yürütme yeteneğine bile sahiptir. Bu çözümlerden bazılarının kısa bir açıklaması aşağıda verilmiştir:

- **SIEM:** **Security Information and Event Management Solution** (SIEM), tüm önemli **log**'ları tek bir merkezi konumda toplar ve **incident**'ları tanımlamak için bunları birbiriyle ilişkilendirir (**correlates**).
    
- **AV:** **Antivirus** (AV), bir sistemdeki bilinen kötü amaçlı programları tespit eder ve sisteminizi bunlar için düzenli olarak tarar.
    
- **EDR:** **Endpoint Detection and Response** (EDR), her sisteme konuşlandırılır ve sistemi bazı ileri düzey tehditlere karşı korur. Bu çözüm ayrıca tehdidi kontrol altına alabilir (**contain**) ve yok edebilir (**eradicate**).
    

**Incident**'lar tanımlandıktan sonra; saldırının kapsamını araştırmak, daha fazla hasarı önlemek için gerekli önlemleri almak ve tehdidi kökten ortadan kaldırmak dahil olmak üzere belirli prosedürler izlenmelidir. Bu adımlar, farklı **incident** türleri için farklılık gösterebilir. Bu senaryoda, her bir **incident** türüyle başa çıkmak için adım adım talimatlara sahip olmak, size büyük ölçüde zaman kazandırır. Bu tür talimatlar **Playbooks** olarak bilinir.

**Playbooks**, kapsamlı bir **incident response** için hazırlanan kılavuzlardır. Aşağıda bir **incident** (Örn: **Phishing Email**) için örnek bir **Playbook** verilmiştir:

1. Tüm paydaşları **phishing email incident**'ı hakkında bilgilendir.
    
2. E-postanın **header** ve **body** analizini yaparak kötü amaçlı olup olmadığını belirle.
    
3. E-posta ile birlikte gelen ekleri (**attachments**) kontrol et ve bunları analiz et.
    
4. Herhangi birinin ekleri açıp açmadığını tespit et.
    
5. Enfekte olmuş sistemleri ağdan izole et (**isolate**).
    
6. E-posta göndericisini engelle (**block**).
    

**Runbooks** ise diğer yandan, farklı **incident**'lar sırasında belirli adımların ayrıntılı, adım adım yürütülmesidir. Bu adımlar, inceleme için mevcut kaynaklara bağlı olarak değişiklik gösterebilir.