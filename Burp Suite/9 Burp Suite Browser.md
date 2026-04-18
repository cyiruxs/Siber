Normal web tarayıcımızı **proxy** ile çalışacak şekilde modifiye etmeye ek olarak, **Burp Suite** ayrıca az önce yapmak zorunda kaldığımız modifikasyonların hiçbirine gerek duymadan **proxy**'yi kullanacak şekilde önceden yapılandırılmış yerleşik bir Chromium tarayıcısı içerir.

Burp Browser'ı başlatmak için proxy sekmesindeki **Open Browser** butonuna tıklayın. Bir Chromium penceresi açılacaktır ve bu tarayıcıda yapılan tüm istekler proxy üzerinden geçecektir.

**Not:** Proje seçenekleri (project options) ve kullanıcı seçenekleri (user options) ayarlarında Burp Browser ile ilgili pek çok ayar bulunmaktadır. Bunları keşfettiğinizden ve ihtiyaca göre özelleştirdiğinizden emin olun.

Ancak, Burp Suite'i Linux üzerinde root kullanıcısı olarak çalıştırıyorsanız (AttackBox'ta olduğu gibi), bir **sandbox** ortamı oluşturulamaması nedeniyle Burp Browser'ın başlamasını engelleyen bir hatayla karşılaşabilirsiniz.

Bunun için iki basit çözüm vardır:

- **Akıllı seçenek (Smart option):** Yeni bir kullanıcı oluşturun ve Burp Browser'ın sorunsuz çalışmasına izin vermek için Burp Suite'i düşük ayrıcalıklı bir hesap (**low-privilege account**) altında çalıştırın.
    
- **Kolay seçenek (Easy option):** **Settings -> Tools -> Burp's browser** yoluna gidin ve **Allow Burp's browser to run without a sandbox** seçeneğini işaretleyin. Bu seçeneğin etkinleştirilmesi, tarayıcının bir **sandbox** olmadan başlamasına izin verecektir. Ancak, güvenlik nedenleriyle bu seçeneğin varsayılan olarak devre dışı bırakıldığını lütfen unutmayın. Eğer etkinleştirmeyi seçerseniz dikkatli olun; zira tarayıcının ele geçirilmesi, bir saldırgana tüm makinenize erişim sağlayabilir. AttackBox'ın eğitim ortamında bu durumun önemli bir sorun teşkil etmesi pek olası değildir, ancak yine de sorumlu bir şekilde kullanın.