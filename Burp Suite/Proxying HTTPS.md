**Not:** AttackBox, bu görevde ortaya konan sorunu çözmek için halihazırda yapılandırılmıştır. Eğer AttackBox kullanıyorsanız ve buradaki bilgileri okumak istemiyorsanız bir sonraki göreve geçebilirsiniz.

**HTTP** trafiğini intercept ederken, **TLS** etkinleştirilmiş sitelerde gezinirken bir sorunla karşılaşabiliriz. Örneğin, `https://google.com/` gibi bir siteye erişirken, PortSwigger Certificate Authority (**CA**) biriminin bağlantıyı güvenli hale getirmek için yetkilendirilmediğini belirten bir hata alabiliriz. Bu durum, tarayıcının **Burp Suite** tarafından sunulan sertifikaya güvenmemesi nedeniyle gerçekleşir.

Bu sorunun üstesinden gelmek için, PortSwigger **CA** sertifikasını tarayıcımızın güvenilen sertifika yetkilileri listesine manuel olarak ekleyebiliriz. İşte nasıl yapılacağı:

1. **CA Sertifikasını İndirin:** Burp **Proxy** etkinken `http://burp/cert` adresine gidin. Bu, `cacert.der` adlı bir dosyayı indirecektir. Bu dosyayı makinenizde bir yere kaydedin.
    
2. **Firefox Sertifika Ayarlarına Erişin:** Firefox URL çubuğuna `about:preferences` yazın ve **Enter**'a basın. Bu sizi Firefox ayarlar sayfasına götürecektir. Sayfada "certificates" (sertifikalar) araması yapın ve **View Certificates** butonuna tıklayın.
    
3. **CA Sertifikasını İçe Aktarın:** Sertifika Yöneticisi (**Certificate Manager**) penceresinde **Import** butonuna tıklayın. Önceki adımda indirdiğiniz `cacert.der` dosyasını seçin.
    
4. **CA Sertifikası için Güven Ayarını Yapın:** Gelen pencerede "Trust this CA to identify websites" (Web sitelerini tanımlamak için bu CA'ya güven) kutucuğunu işaretleyin ve OK butonuna tıklayın.
    

Bu adımları tamamlayarak, PortSwigger **CA** sertifikasını güvenilen sertifika yetkilileri listemize eklemiş olduk. Artık sertifika hatasıyla karşılaşmadan **TLS** özellikli herhangi bir siteyi ziyaret edebilmemiz gerekir.

Tüm sertifika içe aktarma sürecinin görsel bir gösterimi için aşağıdaki videoyu izleyebilirsiniz:

Bu talimatları izleyerek, tarayıcınızın PortSwigger **CA** sertifikasına güvenmesini ve **Burp Suite Proxy** aracılığıyla **TLS** özellikli web siteleriyle güvenli bir şekilde iletişim kurmasını sağlayabilirsiniz.