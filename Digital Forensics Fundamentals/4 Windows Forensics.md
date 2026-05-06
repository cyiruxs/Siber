Suç mahallerinden toplanan en yaygın kanıt türleri, çoğu suç faaliyetinin kişisel bir sistem içermesi nedeniyle masaüstü bilgisayarlar ve dizüstü bilgisayarlardır. Bu cihazlar üzerinde çalışan farklı işletim sistemlerine sahiptir. Bu görevde, birçok vakada incelenmiş olan ve çok yaygın bir işletim sistemi olan Windows işletim sisteminin kanıt elde etme ve analiz süreçlerini tartışacağız.

Veri toplama aşamasının bir parçası olarak, Windows işletim sisteminin adli imajları (**forensic images**) alınır. Bu adli imajlar, tüm işletim sisteminin bit-bit kopyalarıdır. Windows işletim sisteminden iki farklı kategoride adli imaj alınır:

- **Disk image (Disk imajı):** Disk imajı, sistemin depolama aygıtında (HDD, SSD, vb.) bulunan tüm verileri içerir. Bu veriler **non-volatile** (kalıcı) niteliktedir, yani disk verileri işletim sistemi yeniden başlatıldıktan sonra bile varlığını sürdürür. Örneğin; medya dosyaları, belgeler, internet tarama geçmişi ve daha fazlası gibi tüm dosyalar bu kapsamdadır.
    
- **Memory image (Bellek imajı):** Bellek imajı, işletim sisteminin **RAM**'i içerisindeki verileri içerir. Bu bellek **volatile** (uçucu) niteliktedir, yani sistem kapatıldığında veya yeniden başlatıldığında veriler kaybolacaktır. Örneğin; açık dosyaları, çalışan süreçleri (**running processes**), mevcut ağ bağlantılarını vb. yakalamak için bellek imajına öncelik verilmeli ve şüphelinin işletim sisteminden ilk olarak bu imaj alınmalıdır; aksi takdirde sistemin herhangi bir şekilde yeniden başlatılması veya kapatılması tüm uçucu verilerin silinmesine neden olur. Bir Windows işletim sistemi üzerinde dijital adli bilişim yürütürken, disk ve bellek imajlarının toplanması çok önemlidir.
    

Windows işletim sisteminin disk ve bellek imajı edinimi ve analizi için kullanılan bazı popüler araçları tartışalım:

---

### Disk ve Bellek Analiz Araçları

- **FTK Imager:** **FTK Imager**, Windows işletim sistemlerinin disk imajlarını almak için yaygın olarak kullanılan bir araçtır. Çeşitli formatlarda imaj oluşturmak için kullanıcı dostu bir grafik arayüz sunar. Bu araç ayrıca bir disk imajının içeriğini de analiz edebilir. Hem edinim (**acquisition**) hem de analiz amaçlı kullanılabilir.
    
- **Autopsy:** **Autopsy**, popüler bir açık kaynaklı dijital adli bilişim platformudur. Bir araştırmacı, elde edilen bir disk imajını bu araca aktarabilir ve araç imaj üzerinde kapsamlı bir analiz gerçekleştirecektir. İmaj analizi sırasında anahtar kelime arama, silinmiş dosya kurtarma (**deleted file recovery**), dosya meta verileri (**file metadata**), uzantı uyumsuzluğu tespiti (**extension mismatch detection**) ve çok daha fazlası dahil olmak üzere çeşitli özellikler sunar.
    
- **DumpIt:** **DumpIt**, bir Windows işletim sisteminden bellek imajı alma imkanı sunar. Bu araç, bir komut satırı arayüzü ve birkaç komut kullanarak bellek imajları oluşturur. Bellek imajı farklı formatlarda da alınabilir.
    
- **Volatility:** **Volatility**, bellek imajlarını analiz etmek için güçlü bir açık kaynaklı araçtır. Bazı son derece yararlı eklentiler (**plugins**) sunar. Her bir kalıntı (**artifact**), belirli bir eklenti kullanılarak analiz edilebilir. Bu araç Windows, **Linux**, macOS ve Android dahil olmak üzere çeşitli işletim sistemlerini destekler.
    

> [!NOTE] Windows işletim sisteminin disk ve bellek imajlarını elde etmek ve analiz etmek için çeşitli başka araçlar da kullanılmaktadır.