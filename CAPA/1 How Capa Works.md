## CAPA Nedir?

**CAPA** (Common Analysis Platform for Artifacts), FireEye Mandiant ekibi tarafından geliştirilmiş bir araçtır. **Portable Executables (PE)**, **ELF binaries**, **.NET modules**, **shellcode** ve hatta **sandbox** raporları gibi yürütülebilir dosyalarda bulunan **capabilities** (yetenekleri) tanımlamak için tasarlanmıştır.

Bunu, dosyayı analiz ederek ve yaygın davranışları tanımlayan bir dizi kural uygulayarak yapar. Bu sayede programın şunlar gibi neler yapabileceğini belirler:

- **Network communication** (Ağ iletişimi)
    
- **File manipulation** (Dosya manipülasyonu)
    
- **Process injection** (Süreç enjeksiyonu) ve çok daha fazlası.
    

CAPA'nın en büyük avantajı, yılların tersine mühendislik (**reverse engineering**) bilgisini otomatik bir araçta toplamasıdır. Bu durum, tersine mühendislik uzmanı olmayan analistler ve güvenlik profesyonelleri için bile aracı erişilebilir kılar; kodu manuel olarak incelemek zorunda kalmadan kötü amaçlı yazılımın işlevselliğini hızla anlamalarına yardımcı olur.

![malware analysis process, yapay zekayla üretilmiş](https://encrypted-tbn0.gstatic.com/licensed-image?q=tbn:ANd9GcQqsBLMN19iMUabHN_J1PY0Wy6HSJUj0i4v5zYa5_OhRmsFYGbgrsoi-LpGgBz3dzq_IpFC3CNLALkvhqrYPoRJ65_FVjmwC7xQ5XSgnfxrAT0cSU8)


---

## Öğrenme Hedefleri

- CAPA'nın ne olduğunu keşfetmek.
    
- CAPA'yı etkili bir şekilde nasıl kullanacağınızı öğrenmek.
    
- Araç tarafından sunulan ortak alanları ve sonuçları anlamak.
    
- Programın potansiyel faaliyetlerini belirlemek için aracı kullanmak.
    

---

## Oda Ön Koşulları ve Sanal Makine

**MITRE ATT&CK Framework**'üne aşina olmanız önerilir ancak zorunlu değildir.

Bu görevde ekli olan makinedeki aracı kullanacağız. Makine split-screen (bölünmüş ekran) görünümünde başlayacaktır. Eğer Uzak Masaüstü (RDP) ile erişmek isterseniz aşağıdaki bilgileri kullanabilirsiniz:

- **Kullanıcı Adı:** Administrator
    
- **Şifre:** letmein123!
    
- **IP Adresi:** MACHINE_IP
    

> [!IMPORTANT] **Not** Sanal makine (VM) içinde CAPA yüklüdür ve farklı komut parametrelerini deneyebilirsiniz. Ancak ekli VM üzerinde analizlerin tamamlanması uzun sürebildiği için, aşağıdaki gibi önceden işlenmiş raporlar hazırladık:
> 
> - `cryptbot.txt`
>     
> - `cryptbot_vv.txt`
>     
> - `cryptbot_vv.json`
>     
> 
> Bu dosyalar `C:\Users\Administrator\Desktop\capa` dizini altındadır. Bu odada kullanacağımız neredeyse tüm dosyalar bu dizinde yer almaktadır.