### Temel Kavramlar

Metasploit kullanımında sıklıkla duyacağınız üç ana terim şunlardır:

- **Vulnerability (Zafiyet):** Hedef sistemdeki bir tasarım, kodlama veya mantık hatasıdır. Bu hatalar gizli bilgilerin ifşasına veya saldırganın sistemde kod çalıştırmasına yol açabilir.
    
- **Exploit (Sömürü Kodu):** Hedef sistemdeki bir zafiyeti kullanan kod parçasıdır.
    
- **Payload (Yük):** Hedef sistemde çalıştırılacak olan asıl koddur. Exploit zafiyeti sömürürken, payload erişim sağlamak veya bilgi okumak gibi asıl hedefimizi gerçekleştirir.
    

---

### Metasploit Modül Kategorileri

Metasploit içerisindeki her görev, belirli bir modül tipi tarafından yürütülür:

#### 1. Auxiliary (Yardımcı Modüller)

Tarayıcılar (scanners), örümcekler (crawlers) ve fuzzer'lar gibi destekleyici tüm modüller bu kategoridedir. Bilgi toplama ve zafiyet tespiti aşamalarında kritik rol oynarlar.

#### 2. Exploits

Hedef sisteme göre (Windows, Linux, Android vb.) düzenlenmiş sömürü kodlarını içerir.

#### 3. Payloads

Hedefte çalışacak kodlardır. Metasploit bunları dört alt kategoriye ayırır:

- **Singles (Inline):** Ek bir bileşene ihtiyaç duymayan, tek parça halinde çalışan kodlardır (Örn: Kullanıcı ekleme).
    
- **Stagers:** Hedef ile Metasploit arasında bağlantı kanalını kurar.
    
- **Stages:** Stager tarafından indirilen ve daha büyük boyutlu işlemleri yapmaya olanak tanıyan ana yüklerdir.
    
- **Adapters:** Tekil payload'ları farklı formatlara (Örn: PowerShell komutu) dönüştürerek sarar.
    

> [!TIP] **Payload İpucu:** `shell_reverse_tcp` (alt tireli) bir **single** payload iken, `shell/reverse_tcp` (slahlı) bir **staged** payload'dur.

#### 4. Encoders & Evasion

- **Encoders:** Antivirüs imzalarından kaçmak için payload'u kodlar, ancak başarı oranı antivirüslerin gelişmiş kontrolleri nedeniyle sınırlı olabilir.
    
- **Evasion:** Antivirüs yazılımlarını doğrudan atlatmaya odaklanan özel modüllerdir.
    

#### 5. Post & NOPs

- **Post:** Sızma sonrası (post-exploitation) işlemler için kullanılır.
    
- **NOPs:** Hiçbir işlem yapmayan (No OPeration) kodlardır; genellikle payload boyutlarını standart hale getirmek için tampon olarak kullanılırlar.
    

---

### 🛡️ Siber Güvenlik İpucu

	Metasploit konsoluna (`msfconsole`) girdikten sonra bir modülün detaylarını görmek için `info [modül_adı]` komutunu kullanabilirsin. Eğer hedef sistemde sadece komut çalıştırmak değil, etkileşimli bir komut satırı istiyorsan, payload olarak bir **"shell"** seçmen gerekir.