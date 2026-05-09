## Windows Defender Firewall

Windows Defender, Microsoft tarafından Windows **OS** içerisinde sunulan yerleşik bir **firewall**'dur. Bu **firewall**, belirli programları oluşturma, izin verme veya reddetme ya da özelleştirilmiş kurallar oluşturma gibi tüm temel işlevleri içerir. Bu görev, sisteminizin gelen ve giden ağ trafiğini kısıtlamak için kullanabileceğiniz Windows Defender **Firewall**'un bazı temel bileşenlerini kapsayacak şekilde tasarlanmıştır. Bu **firewall**'u açmak için Windows aramasını açmalı ve "Windows Defender Firewall" yazmalısınız.

Windows Defender **Firewall**'un ana sayfası "Network Profiles" (Ağ Profilleri) ve mevcut seçenekleri gösterir. Bu, **firewall** ile ilgili tüm seçeneklerin bulunduğu ana panodur (**dashboard**).

### Network Profiles (Ağ Profilleri)

Mevcut iki ağ profili vardır. Windows **firewall**, Network Location Awareness (NLA) özelliğine dayanarak mevcut ağınızı belirler ve ilgili profil **firewall** ayarlarını sizin için uygular. Her biri için farklı **firewall** ayarlarına sahip olabiliriz.

- **Private networks (Özel ağlar):** Ev ağımıza bağlandığımızda uygulanacak **firewall** yapılandırmalarını içerir.
    
- **Guest or public networks (Konuk veya genel ağlar):** Kahve dükkanları, restoranlar veya benzeri gibi halka açık veya güvenilmeyen bir ağa bağlandığımızda uygulanacak **firewall** yapılandırmalarını içerir. Örneğin, halka açık ağlara bağlanırken, tüm gelen ağ bağlantılarını engelleyecek ve yalnızca sizin için gerekli olan bazı giden bağlantılara izin verecek şekilde **firewall** ayarlarını yapılandırabilirsiniz. Bu ayarlar genel ağ profiline uygulanacak ve evdeki özel ağınızda olduğunuzda uygulanmayacaktır.
    

Ağ profillerinizden herhangi birinde herhangi bir uygulamaya izin vermek veya izin vermemek için ilgili seçeneğe tıklayın. Bu, sisteminizde yüklü olan tüm uygulamaların ve özelliklerin listelendiği sayfaya sizi götürecektir. Ağ profillerinizden herhangi birinde izin vermek istediklerinizi işaretleyebilir veya gerekmiyorsa işaretini kaldırabilirsiniz. Windows Defender **Firewall** varsayılan olarak açıktır. Ancak, açmak veya kapatmak isterseniz, ilgili ayarlar sayfasına gidebilirsiniz. Microsoft'un önermediği tamamen kapatma işlemi yerine, tüm gelen bağlantıları (**incoming connections**) engelleyebilirsiniz. Ayrıca, tüm **firewall** varsayılan ayarlarını geri yüklemek için ana panodan istediğiniz zaman "Restore Defaults" (Varsayılanları Geri Yükle) seçeneğine tıklayabilirsiniz.

---

### Custom Rules (Özel Kurallar)

Windows Defender **Firewall**, ağınız için gerektiğinde belirli trafiğe izin vermek veya izin vermemek amacıyla özel kurallar oluşturmanıza da olanak tanır. Giden tüm **HTTP** (port 80) veya **HTTPS** (port 443) trafiğini engellemek için özel bir kural oluşturalım. Bu kuralı oluşturduktan sonra, web siteleri bizim engelleyeceğimiz port 80 veya 443 üzerinde çalıştığından, internetteki hiçbir web sitesine göz atamayacağız.

Bu kuralı oluşturmadan önce, bir web sitesini ziyaret edip edemeyeceğimizi test edelim. Test için `[http://10.10.10.10/](http://10.10.10.10/)` adresini ziyaret edelim. Başlangıçta bu web sitesini ziyaret edebildiğimizi göreceğiz.

Özel bir kural oluşturmak için ana panodaki seçeneklerden "Advanced Settings" (Gelişmiş Ayarlar) öğesini seçin. Bu, kendi kurallarınızı oluşturabileceğiniz yeni bir sekme açacaktır.

Gelen (**inbound**) ve giden (**outbound**) kuralları oluşturmak için mevcut seçenekleri görebilirsiniz. Giden tüm **HTTP** ve **HTTPS** trafiğimizi engellemek için bir **outbound rule** oluşturalım:

1. Sol taraftaki **Outbound Rules** seçeneğine tıklayın, ardından sağ taraftaki **New Rule** seçeneğine tıklayın. Bu, kural sihirbazını açacaktır.
    
2. İlk adımda **Custom** (Özel) seçeneğini seçin ve **Next**'e basın.
    
3. İkinci adımda **All programs** (Tüm programlar) seçeneğini seçin ve **Next**'e basın.
    
4. Üçüncü adımda protokol tipini seçmeniz istenecektir. **Protocol type** olarak "TCP" seçin, **Local port** kısmını olduğu gibi bırakın ve **Remote port** kısmını açılır menüden "Specific ports" (Belirli portlar) olarak değiştirin. Aşağıdaki alana port numaralarını yazın (bizim durumumuzda: 80,443). Şimdi **Next**'e tıklayın.
    
    - _Not:_ Port numaralarını virgülle ayırın ve lütfen aralarında boşluk bırakmayın.
        
5. **Scope** (Kapsam) sekmesinde, yerel ve uzak IP adreslerini olduğu gibi bırakın ve **Next** düğmesine basın.
    
6. **Action** (Eylem) sekmesinde, **Block the connection** (Bağlantıyı engelle) seçeneğini etkinleştirin ve **Next**'e basın.
    
7. **Profile** sekmesinde, tüm ağ profillerini işaretli bırakıyoruz.
    
8. Son aşama olarak kuralınıza bir isim ve isteğe bağlı bir açıklama verip **Finish** düğmesine basın.
    

Artık kuralımızın mevcut giden kuralları arasında olduğunu görebiliriz. Şimdi `[http://10.10.10.10/](http://10.10.10.10/)` adresine giderek kuralımızı test edelim. Sayfaya ulaşılamadığına dair bir hata mesajı almalıyız; bu, kuralın çalıştığı anlamına gelir.