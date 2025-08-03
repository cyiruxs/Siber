### Red Team Görevlerinde Adversary Emulation ve Kill Chainler

**Red team**'in temel işlevlerinden biri **adversary emulation** (düşman taklidi) yapmaktır. Zorunlu olmamakla birlikte, gerçek bir düşmanın belirli bir ortamda kendi araç ve metodolojilerini kullanarak neler yapabileceğini değerlendirmek için yaygın olarak kullanılır. **Red team**, bir görevin adımlarını ve prosedürlerini özetlemek ve değerlendirmek için çeşitli **cyber kill chain**'leri (siber öldürme zincirleri) kullanabilir.

**Blue team** genellikle davranışları haritalamak ve bir düşmanın hareketlerini parçalara ayırmak için **cyber kill chain**'leri kullanır. **Red team** bu fikri, düşman **TTP**'lerini (**Tactics, Techniques, and Procedures** - Taktikler, Teknikler ve Prosedürler) bir görevin bileşenlerine haritalamak için uyarlayabilir.

Birçok düzenleme ve standardizasyon kuruluşu kendi **cyber kill chain**'ini yayınlamıştır. Her **kill chain**, kabaca aynı yapıyı takip eder; bazıları daha derinlemesine gider veya hedefleri farklı tanımlar. Aşağıda standart **cyber kill chain**'lerin küçük bir listesi bulunmaktadır:

- **Lockheed Martin Cyber Kill Chain**
    
- **Unified Kill Chain**
    
- **Varonis Cyber Kill Chain**
    
- **Active Directory Attack Cycle**
    
- **MITRE ATT&CK Framework**
    

Bu odada, genellikle "Lockheed Martin Cyber Kill Chain"e atıfta bulunacağız. Bu, diğerlerinden daha standart bir **kill chain**'dir ve **red team** ile **blue team** arasında çok yaygın olarak kullanılır.

**Lockheed Martin kill chain**, bir çevre veya harici ihlal (**perimeter or external breach**) üzerine odaklanır. Diğer **kill chain**'lerin aksine, dahili harekete ilişkin derinlemesine bir döküm sunmaz. Bu **kill chain**'i, mevcut tüm davranış ve operasyonların bir özeti olarak düşünebilirsiniz.
![[Pasted image 20250803040629.png]]
**Kill chain**'in bileşenleri aşağıdaki tabloda açıklanmıştır:

| Teknik (Technique)                                  | Amaç (Purpose)                                                                                                           | Örnekler (Examples)                                     |     |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------- | --- |
| **Reconnaissance** (Keşif)                          | Hedef hakkında bilgi edinmek.                                                                                            | E-posta toplama, **OSINT** (Açık Kaynak İstihbaratı)    |     |
| **Weaponization** (Silahlandırma)                   | Hedefi, bir **exploit** ile birleştirmek. Genellikle bir **deliverable payload** (teslim edilebilir yük) ile sonuçlanır. | **Backdoor** içeren **exploit**, zararlı Office belgesi |     |
| **Delivery** (Teslimat)                             | Silahlandırılmış işlevin hedefe nasıl ulaştırılacağı.                                                                    | E-posta, web, USB                                       |     |
| **Exploitation** (İstismar)                         | Kod çalıştırmak için hedefin sistemini istismar etmek.                                                                   | **MS17-010**, **Zero-Logon**, vb.                       |     |
| **Installation** (Kurulum)                          | Zararlı yazılım veya başka bir aracı kurmak.                                                                             | **Mimikatz**, **Rubeus**, vb.                           |     |
| **Command & Control** (C2)                          | Ele geçirilmiş varlığı uzak bir merkezi kontrolörden kontrol etmek.                                                      | **Empire**, **Cobalt Strike**, vb.                      |     |
| **Actions on Objectives** (Hedefe Yönelik Eylemler) | Ransomware, veri sızdırma (**data exfiltration**) gibi nihai hedefler.                                                   | **Conti**, **LockBit2.0**, vb.                          |     |
