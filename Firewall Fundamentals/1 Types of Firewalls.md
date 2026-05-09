
## Güvenlik Duvarı Türleri ve OSI Katmanları

Kuruluşlar, zararlı trafiği sistemlerinden ve ağlarından filtreleme yeteneğini keşfettikten sonra ağlarda **firewall** kullanımı yaygınlaştı. Daha sonra, her biri benzersiz bir amaca hizmet eden birkaç farklı **firewall** türü tanıtıldı. Farklı **firewall** türlerinin farklı **OSI model** katmanlarında çalıştığını not etmek de önemlidir. **Firewall**'lar birçok türe ayrılır.

En yaygın **firewall** türlerinden bazılarını ve **OSI** modelindeki rollerini inceleyelim.

### Stateless Firewall (Durumsuz Güvenlik Duvarı)

Bu tür **firewall**, **OSI model**'in 3. ve 4. katmanlarında çalışır ve önceki bağlantıların durumunu dikkate almadan, yalnızca önceden belirlenmiş kurallara göre verileri filtreleyerek çalışır. Bu, meşru bir bağlantının parçası olup olmadığına bakılmaksızın her paketi kurallarla eşleştireceği anlamına gelir. Gelecekteki paketler için karar vermek üzere önceki bağlantıların durumu hakkında hiçbir bilgi tutmaz. Bu nedenle, bu **firewall**'lar paketleri hızlı bir şekilde işleyebilir. Ancak, önceki bağlantılarla olan ilişkisine dayanarak verilere karmaşık politikalar uygulayamazlar. Diyelim ki **firewall**, kurallarına dayanarak tek bir kaynaktan gelen birkaç paketi reddetti. İdeal olarak, önceki paketler **firewall** kurallarına uyamadığı için bu kaynaktan gelen gelecekteki tüm paketleri düşürmelidir. Ancak, **firewall** bunu unutmaya devam eder ve bu kaynaktan gelen gelecekteki paketler yeniymiş gibi değerlendirilir ve kurallarıyla tekrar eşleştirilir.

### Stateful Firewall (Durumlu Güvenlik Duvarı)

**Stateless firewall**'ların aksine, bu tür **firewall** paketleri önceden belirlenmiş kurallara göre filtrelemenin ötesine geçer. Ayrıca önceki bağlantıları takip eder ve bunları bir **state table** (durum tablosu) içinde saklar. Bu, paketleri bağlantı geçmişlerine göre inceleyerek başka bir güvenlik katmanı ekler. **Stateful firewall**'lar **OSI model**'in 3. ve 4. katmanlarında çalışır. Diyelim ki **firewall**, kurallarına dayanarak bir kaynak adresten birkaç paketi kabul etti. Bu durumda, bu bağlantıyı **state table**'ına not edecek ve bu bağlantı için gelecekteki tüm paketlerin her birini incelemeden otomatik olarak izin verilmesini sağlayacaktır. Benzer şekilde, **stateful firewall**'lar birkaç paketini reddettikleri bağlantıları not eder ve bu bilgilere dayanarak aynı kaynaktan gelen sonraki tüm paketleri reddederler.

### Proxy Firewall

Önceki **firewall**'ların sorunu, bir paketin içeriğini inceleyememeleriydi. **Proxy firewall**'lar veya uygulama düzeyi ağ geçitleri (**application-level gateways**), özel ağ ile İnternet arasında aracılar olarak hareket eder ve **OSI model**'in 7. katmanında çalışır. Tüm paketlerin içeriğini de incelerler. Bir ağdaki kullanıcılar tarafından yapılan istekler, bu **proxy** tarafından incelendikten ve dahili IP adresleri için anonimlik sağlamak amacıyla kendi IP adresleriyle maskelendikten sonra iletilir. İçeriğine göre gelen ve giden trafiğe izin vermek/reddetmek için bu **firewall**'lara içerik filtreleme (**content filtering**) politikaları uygulanabilir.

### Next-Generation Firewall (NGFW)

Bu, **OSI model**'in 3. katmanından 7. katmanına kadar çalışan, derin paket incelemesi (**deep packet inspection**) ve gelen ve giden ağ trafiğinin güvenliğini artıran diğer işlevleri sunan en gelişmiş **firewall** türüdür. Kötü amaçlı faaliyetleri gerçek zamanlı olarak engelleyen bir saldırı önleme sistemine (**intrusion prevention system - IPS**) sahiptir. Saldırı modellerini analiz ederek ve ağa ulaşmadan önce anında engelleyerek sezgisel analiz (**heuristic analysis**) sunar. **NGFW**'ler, paketleri şifresini çözdükten sonra inceleyen ve verimli kararlar vermek için verileri tehdit istihbaratı akışlarıyla (**threat intelligence feeds**) ilişkilendiren **SSL/TLS decryption** yeteneklerine sahiptir.

---

### Firewall Karşılaştırma Tablosu

Aşağıdaki tablo, her bir **firewall**'un özelliklerini listeler ve farklı kullanım durumları için en uygun **firewall**'u seçmenize yardımcı olur.

| **Firewall Türü**             | **Özellikler**                                                                                                                                                                                                                                  |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Stateless firewalls**       | - Temel filtreleme<br><br>  <br><br>- Önceki bağlantıların takibi yapılmaz<br><br>  <br><br>- Yüksek hızlı ağlar için verimli                                                                                                                   |
| **Stateful firewalls**        | - Trafiği paternlerle tanır<br><br>  <br><br>- Karmaşık kurallar uygulanabilir<br><br>  <br><br>- Ağ bağlantılarını izler                                                                                                                       |
| **Proxy firewalls**           | - Paketlerin içindeki verileri de inceler<br><br>  <br><br>- İçerik filtreleme seçenekleri sunar<br><br>  <br><br>- Uygulama kontrolü sağlar<br><br>  <br><br>- **SSL/TLS** veri paketlerini çözer ve inceler                                   |
| **Next-generation firewalls** | - Gelişmiş tehdit koruması sağlar<br><br>  <br><br>- Yerleşik bir **intrusion prevention system** ile gelir<br><br>  <br><br>- Sezgisel analize dayalı anormallikleri tanımlar<br><br>  <br><br>- **SSL/TLS** veri paketlerini çözer ve inceler |