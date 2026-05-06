Kanıt elde etme süreci kritik bir görevdir. Adli bilişim ekibi, orijinal verilere müdahale etmeden tüm kanıtları güvenli bir şekilde toplamalıdır. Dijital cihazlar için kanıt elde etme yöntemleri, cihazın türüne bağlıdır. Bununla birlikte, kanıt elde edilirken izlenmesi gereken bazı genel uygulamalar mevcuttur. Gelin bunlardan en önemlilerini tartışalım.

### Proper Authorization (Uygun Yetkilendirme)

Adli bilişim ekibi, herhangi bir veri toplamadan önce ilgili makamlardan yetki almalıdır. Önceden onay alınmadan toplanan kanıtlar mahkemede geçersiz sayılabilir. Adli kanıtlar, bir kurumun veya bireyin özel ve hassas verilerini içerir. Bu verileri toplamadan önce uygun yetkilendirmenin yapılması, soruşturmanın yasaların sınırları dahilinde yürütülmesi için esastır.

---

### Chain of Custody (Gözetim Zinciri)

Bir soruşturma ekibinin suç mahallindeki tüm kanıtları topladığını ve birkaç gün sonra bazı kanıtların kaybolduğunu veya kanıtlarda herhangi bir değişiklik olduğunu hayal edin. Bu senaryoda, kanıt sahiplerini belgelemek için uygun bir süreç olmadığından hiç kimse sorumlu tutulamaz. Bu sorun, bir **chain of custody** (gözetim zinciri) belgesi tutularak çözülebilir. Gözetim zinciri, kanıtla ilgili tüm ayrıntıları içeren resmi bir belgedir. Temel ayrıntılardan bazıları aşağıda listelenmiştir:

- Kanıtın açıklaması (ad, tür).
    
- Kanıtı toplayan kişilerin isimleri.
    
- Kanıt toplama tarihi ve saati.
    
- Her bir kanıt parçasının saklama yeri.
    
- Erişim zamanları ve kanıta erişen kişinin kaydı.
    

Bu, kanıtlar için uygun bir izleme yolu oluşturur ve kanıtların korunmasına yardımcı olur. **Chain of custody** belgesi, mahkemeye sunulan kanıtların bütünlüğünü (**integrity**) ve güvenilirliğini kanıtlamak için kullanılabilir.

---

### Use of Write Blockers (Yazma Engelleyicilerin Kullanımı)

**Write blockers** (yazma engelleyiciler), dijital adli bilişim ekibinin araç kutusunun temel bir parçasıdır. Bir şüphelinin sabit diskinden kanıt topladığınızı ve sabit diski adli bilişim iş istasyonuna (**forensic workstation**) bağladığınızı varsayalım. Toplama işlemi gerçekleşirken, adli bilişim iş istasyonundaki bazı arka plan görevleri sabit diskteki dosyaların zaman damgalarını (**timestamps**) değiştirebilir. Bu durum analiz sırasında engellere yol açabilir ve sonuçta hatalı sonuçlar doğurabilir. Aynı senaryoda, verilerin sabit diskten bir yazma engelleyici kullanılarak toplandığını varsayalım. Bu sefer, yazma engelleyici her türlü kanıt değiştirme işlemini engelleyebileceği için şüphelinin sabit diski orijinal durumunda kalacaktır.

---

> [!IMPORTANT] Kanıt toplama aşamasındaki bu prosedürler, adli bilişim sürecinin hukuki geçerliliğini ve teknik doğruluğunu garanti altına alan en önemli unsurlardır.