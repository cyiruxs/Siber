## Windows Event Viewer ve Log Analizi

Diğer işletim sistemleri gibi, Windows **OS** de gerçekleşen birçok faaliyeti günlüğe kaydeder. Bunlar, her biri belirli bir **log** kategorisine sahip ayrılmış **log file**'larda saklanır. Windows İşletim Sisteminde saklanan bazı kritik **log** türleri şunlardır:

- **Application:** İşletim sistemi üzerinde çalışan birçok uygulama vardır. Bu uygulamalarla ilgili her türlü bilgi bu dosyaya kaydedilir. Bu bilgiler hataları (**errors**), uyarıları (**warnings**), uyumluluk sorunlarını (**compatibility issues**) vb. içerir.
    
- **System:** İşletim sisteminin kendisinin farklı çalışma operasyonları vardır. Bu operasyonlarla ilgili tüm bilgiler **System log** dosyasına kaydedilir. Bu bilgiler sürücü sorunlarını (**driver issues**), donanım sorunlarını (**hardware issues**), sistem başlatma ve kapatma bilgilerini, servis bilgilerini vb. içerir.
    
- **Security:** Güvenlik açısından Windows **OS**'teki en önemli **log** dosyasıdır. Kullanıcı kimlik doğrulaması (**user authentication**), kullanıcı hesaplarındaki değişiklikler, güvenlik politikası değişiklikleri vb. dahil olmak üzere güvenlikle ilgili tüm faaliyetleri kaydeder.
    

Bunların yanı sıra, Windows işletim sisteminde belirli eylemler ve uygulamalarla ilgili faaliyetleri kaydetmek için tasarlanmış birkaç **log** dosyası daha bulunmaktadır.

Önceki görevlerde incelenen ve görüntülemek için yerleşik bir uygulaması olmayan diğer **log** dosyalarının aksine, Windows **OS**, bu **log**'ları görüntülemek ve içlerinde herhangi bir şeyi aramak için güzel bir grafik kullanıcı arayüzü sunan **Event Viewer** (Olay Görüntüleyicisi) adlı bir yardımcı programa sahiptir.

**Event Viewer**'ı açmak için Windows'un Başlat düğmesine tıklayın ve 'Event Viewer' yazın. Bu, sizin için **Event Viewer**'ı açacaktır. Program açıldığında, sol taraftaki panelde mevcut farklı **log**'lar görülebilir. Bu bölümden 'Windows Logs' klasörüne tıklayarak bu görevin başında tartıştığımız farklı **log** türlerini görebilirsiniz.

Ana panelde bir **log** dosyasına tıkladığımızda farklı **log** kayıtlarını görürüz. Sağ taraftaki panelde ise **log**'ları analiz etmek için farklı seçenekler mevcuttur. İçeriğini görmek için bu **log**'lardan birine çift tıklayalım. Bir Windows **event log**'u şu alanlara sahiptir:

- **Description:** Bu alan, faaliyet hakkında ayrıntılı bilgi içerir.
    
- **Log Name:** **Log** dosyasının adını belirtir.
    
- **Logged:** Bu alan, faaliyetin gerçekleştiği zamanı belirtir.
    
- **Event ID:** Belirli bir faaliyet için benzersiz tanımlayıcılardır.
    

### Kritik Windows Event ID'leri

Windows olay günlüklerinde çok sayıda **Event ID** mevcuttur. Belirli bir faaliyeti aramak için bu **Event ID**'leri kullanabiliriz. Örneğin, **Event ID 4624** başarılı bir giriş faaliyetini benzersiz şekilde tanımlar; dolayısıyla başarılı girişleri araştırırken yalnızca bu **Event ID**'yi aramanız yeterlidir.

|**Event ID**|**Açıklama**|
|---|---|
|**4624**|Bir kullanıcı hesabı başarıyla oturum açtı (**logged in**)|
|**4625**|Bir kullanıcı hesabı oturum açamadı (**failed to login**)|
|**4634**|Bir kullanıcı hesabı başarıyla oturum kapattı (**logged off**)|
|**4720**|Bir kullanıcı hesabı oluşturuldu|
|**4724**|Bir hesabın şifresini sıfırlama girişimi yapıldı|
|**4722**|Bir kullanıcı hesabı etkinleştirildi (**enabled**)|
|**4725**|Bir kullanıcı hesabı devre dışı bırakıldı (**disabled**)|
|**4726**|Bir kullanıcı hesabı silindi|

Çok daha fazla **Event ID** vardır. Hepsini hatırlamak gerekli değildir ancak kritik olanları hatırlamak faydalıdır.

**Event Viewer**, 'Filter Current Log' özelliği ile belirli bir **Event ID** ile ilgili **log**'ları aramıza olanak tanır. Herhangi bir filtre uygulamak için bu özelliğe tıklayabiliriz. 'Filter Current Log' seçeneğine tıkladığımızda, filtrelemek istediğimiz **Event ID**'leri girmemiz istenen bir pencere açılır. Buraya örneğin **4624** yazıp 'OK' butonuna bastığınızda, yalnızca bu kimliğe sahip tüm **log**'ları görebilirsiniz. Herhangi bir **log**'un üzerine çift tıklayarak detaylarını görüntüleyebilirsiniz