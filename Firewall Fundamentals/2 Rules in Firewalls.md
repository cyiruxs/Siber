## Firewall Kuralları ve Bileşenleri

Bir **firewall**, ağ trafiğiniz üzerinde kontrol sahibi olmanızı sağlar. Trafiği yerleşik kurallarına göre filtrelemesine rağmen, çeşitli ağlar için bazı özelleştirilmiş kurallar tanımlanabilir. Örneğin, ağlarına gelen tüm **SSH** trafiğini reddetmek isteyen ağlar olabilir. Ancak sizin ağınızın, birkaç belirli IP adresinden gelen **SSH** trafiğine izin verme gereksinimi olabilir. Kurallar, ağınızın gelen ve giden trafiği için bu özelleştirilmiş ayarları yapılandırmanıza olanak tanır.

Bir **firewall** kuralının temel bileşenleri aşağıda açıklanmıştır:

- **Source address (Kaynak adres):** Trafiği başlatan makinenin IP adresi.
    
- **Destination address (Hedef adres):** Veriyi alacak makinenin IP adresi.
    
- **Port:** Trafik için kullanılan port numarası.
    
- **Protocol (Protokol):** İletişim sırasında kullanılacak olan protokol.
    
- **Action (Eylem):** Belirli bir nitelikteki trafik tanımlandığında gerçekleştirilecek eylemi tanımlar.
    
- **Direction (Yön):** Kuralın gelen mi yoksa giden trafiğe mi uygulanacağını tanımlar.
    

---

### Eylem Türleri (Types of Actions)

Bir kuraldaki “Action” bileşeni, bir veri paketi tanımlanan kural kategorisine girdiğinde atılacak adımları belirtir. Bir kurala uygulanabilecek üç ana eylem aşağıda açıklanmıştır:

#### Allow (İzin Ver)

Bir kuralın “Allow” eylemi, kural içinde tanımlanan belirli trafiğe izin verileceğini gösterir. Örneğin; ağımızdan internete doğru port 80 (**HTTP** trafiği için kullanılır) üzerinden çıkan tüm giden trafiğe izin veren bir kural oluşturalım:

|Action|Source|Destination|Protocol|Port|Direction|
|---|---|---|---|---|---|
|**Allow**|192.168.1.0/24|Any|TCP|80|Outbound|

#### Deny (Reddet)

Bir kuralın “Deny” eylemi, kural içinde tanımlanan trafiğin engelleneceği ve trafiğe izin verilmeyeceği anlamına gelir. Bu kurallar, güvenlik ekibi için kötü amaçlı IP adreslerinden gelen belirli trafiği reddetmek ve ağın tehdit yüzeyini azaltmak için daha fazla kural oluşturmak adına temel teşkil eder. Örneğin; kritik sunucumuzun port 22 (**SSH** üzerinden bir makineye uzaktan bağlanmak için kullanılır) üzerindeki tüm gelen trafiği reddetmek için bir kural oluşturalım:

|Action|Source|Destination|Protocol|Port|Direction|
|---|---|---|---|---|---|
|**Deny**|Any|192.168.1.0/24|TCP|22|Inbound|


#### Forward (Yönlendir)

“Forward” eylemi, **firewall** üzerinde oluşturulan yönlendirme kurallarını kullanarak trafiği farklı bir ağ segmentine yönlendirir. Bu, yönlendirme (**routing**) işlevi sağlayan ve farklı ağ segmentleri arasında ağ geçidi (**gateway**) görevi gören **firewall**'lar için geçerlidir. Örneğin; port 80 (**HTTP** trafiği) üzerinden gelen tüm trafiği **192.168.1.8** web sunucusuna yönlendiren bir kural oluşturalım:

|Action|Source|Destination|Protocol|Port|Direction|
|---|---|---|---|---|---|
|**Forward**|Any|192.168.1.8|TCP|80|Inbound|


---

### Kuralların Yönlülüğü (Directionality of Rules)

**Firewall**'lar, kuralların oluşturulduğu trafik yönüne göre kategorize edilen farklı kural kategorilerine sahiptir. Bu yönlülüklerin her birini inceleyelim.

- **Inbound Rules (Gelen Trafik Kuralları):** Kurallar yalnızca gelen trafiğe uygulanacaksa bu kategoride yer alır. Örneğin, web sunucunuzda gelen **HTTP** trafiğine (port 80) izin verebilirsiniz.
    
- **Outbound Rules (Giden Trafik Kuralları):** Bu kurallar yalnızca giden trafik için oluşturulur. Örneğin, mail sunucusu hariç tüm cihazlardan gelen giden **SMTP** trafiğini (port 25) engellemek gibi.
    
- **Forward Rules (Yönlendirme Kuralları):** Ağ içindeki belirli trafiği yönlendirmek için oluşturulur. Örneğin, gelen **HTTP** (port 80) trafiğini ağınızda bulunan web sunucusuna iletmek için bir yönlendirme kuralı oluşturulabilir.