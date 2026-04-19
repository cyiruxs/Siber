## Shell Nedir?

Bir **shell**, kullanıcının bir **OS** (İşletim Sistemi) ile etkileşime girmesini sağlayan yazılımdır. Grafiksel bir arayüz olabilir, ancak genellikle bir **command-line interface** (komut satırı arayüzü) şeklindedir ve bu, hedef sistemde çalışan işletim sistemine bağlıdır.

Siber güvenlikte bu terim, genellikle bir saldırganın ele geçirilmiş bir sisteme erişirken kullandığı, komutlar çalıştırmasına ve yazılımlar yürütmesine olanak tanıyan belirli bir **shell session**'ı (shell oturumu) ifade eder. Bu, saldırganların aşağıda açıklananlar gibi çeşitli faaliyetleri yürütmesine olanak tanır:

- **Remote System Control (Uzak Sistem Kontrolü):** Saldırganın hedef sistemde uzaktan komut veya yazılım yürütmesine olanak tanır.
    
- **Privilege Escalation (Yetki Yükseltme):** Eğer bir shell üzerinden sağlanan ilk erişim sınırlı veya kısıtlıysa, saldırganlar daha yüksek veya idari erişim seviyelerine yetki yükseltmek için yollar arayabilirler.
    
- **Data Exfiltration (Veri Sızdırma):** Saldırganlar elde edilen bir shell aracılığıyla komut yürütme erişimine sahip olduklarında, hassas verileri okumak ve kopyalamak için sistemi keşfedebilirler.
    
- **Persistence (Kalıcılık) ve Maintenance Access (Erişim Bakımı):** Shell erişimi elde edildikten sonra saldırganlar, hedef sisteme daha sonraki kullanımlar için erişimi sürdürmek amacıyla kullanıcılar ve kimlik bilgileri oluşturabilir veya **backdoor** yazılımları kopyalayabilirler.
    
- **Post-Exploitation Activities (Sömürü Sonrası Faaliyetler):** Bir shell erişimi sağlandıktan sonra saldırganlar; kötü amaçlı yazılım (malware) yayma, gizli hesaplar oluşturma ve bilgileri silme gibi geniş bir yelpazede sömürü sonrası faaliyetler yürütebilirler.
    
- **Access Other Systems on the Network (Ağdaki Diğer Sistemlere Erişim):** Saldırganın niyetine bağlı olarak, elde edilen shell sadece bir ilk erişim noktası olabilir. Amaç, elde edilen shell'i ele geçirilen sistem ağındaki farklı noktalara bir **pivot** olarak kullanarak ağ üzerinden farklı bir hedefe atlamak olabilir. Bu durum **pivoting** olarak da bilinir.