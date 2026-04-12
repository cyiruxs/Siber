Burp Suite; web veya mobil uygulama değerlendirmeleri, pentesting, bug bounty avcılığı ve hatta web uygulaması geliştirmedeki hata ayıklama (debugging) özellikleri için olsun, elinizin altında bulunması çok yararlı olan araçlardan biridir. İşte Burp Suite'in farklı platformlara kurulmasına ilişkin bir kılavuz:

**Not:** Eğer AttackBox kullanıyorsanız, Burp Suite zaten yüklüdür, bu nedenle bu adımı atlayabilirsiniz.

### İndirmeler

Burp Suite'in diğer sistemler için en son sürümünü indirmek üzere, indirme sayfalarına gitmek için bu butona (yeni sekmede açılır) tıklayabilirsiniz.

- **Kali Linux:** Burp Suite, Kali Linux ile önceden yüklenmiş olarak gelir. Kali kurulumunuzda eksik olması durumunda, Kali **apt** depolarından kolayca yükleyebilirsiniz.
    
- **Linux, macOS ve Windows:** Diğer işletim sistemleri için PortSwigger, Burp Suite indirme sayfasında Burp Suite Community ve Burp Suite Professional için özel yükleyiciler sağlar. Açılır menüden işletim sisteminizi seçin ve **Burp Suite Community Edition**'ı seçin. Ardından, indirmeyi başlatmak için **Download** butonuna tıklayın.
    

### Kurulum

İşletim sisteminiz için uygun yöntemi kullanarak Burp Suite'i kurun. Windows'ta yürütülebilir dosyayı (executable file) çalıştırın, Linux'ta ise terminalden betiği (**sudo** ile veya sudo olmadan) çalıştırın. Linux'ta kurulum sırasında **sudo** kullanmamayı tercih ederseniz, Burp Suite ana dizininize `~/BurpSuiteCommunity/BurpSuiteCommunity` konumuna kurulacak ve **PATH**'inize eklenmeyecektir.

Kurulum sihirbazı açık talimatlar sunar ve varsayılan ayarları kabul etmek genellikle güvenlidir. Ancak, yükleyiciyi her zaman dikkatlice incelemeniz önerilir.

Burp Suite başarıyla kurulduğuna göre artık uygulamayı başlatabilirsiniz. Bir sonraki görevde, ilk kurulum ve yapılandırmayı (configuration) inceleyeceğiz.