### Windows Etki Alanları: Aktif Dizin Hizmetleri

Herhangi bir Windows Etki Alanı'nın (Windows Domain) çekirdeğini **Aktif Dizin Etki Alanı Hizmeti (AD DS)** oluşturur. Bu hizmet, ağınızdaki tüm "nesnelerin" (kullanıcılar, gruplar, makineler, yazıcılar ve daha pek çok şey) bilgilerini içeren bir katalog görevi görür. Şimdi bunlardan bazılarına göz atalım:

#### Kullanıcılar

Kullanıcılar, Aktif Dizin'deki en yaygın nesne türlerinden biridir. Kullanıcılar, **güvenlik sorumluları** olarak bilinen nesnelerden biridir. Bu, etki alanı tarafından kimliklerinin doğrulanabileceği ve dosya veya yazıcı gibi kaynaklar üzerinde ayrıcalıklar atanabileceği anlamına gelir. Bir güvenlik sorumlusunun, ağdaki kaynaklar üzerinde işlem yapabilen bir nesne olduğunu söyleyebiliriz.

Kullanıcılar, iki tür varlığı temsil etmek için kullanılabilir:

- **İnsanlar:** Kullanıcılar genellikle çalışanlar gibi, ağa erişmesi gereken kuruluşunuzdaki kişileri temsil eder.
    
- **Hizmetler:** IIS veya MSSQL gibi hizmetler tarafından kullanılacak kullanıcıları da tanımlayabilirsiniz. Her hizmetin çalışması için bir kullanıcıya ihtiyacı vardır, ancak hizmet kullanıcıları normal kullanıcılardan farklıdır, çünkü yalnızca kendi özel hizmetlerini çalıştırmak için gerekli ayrıcalıklara sahip olurlar.
    

#### Makineler

Makineler, Aktif Dizin'deki başka bir nesne türüdür; Aktif Dizin etki alanına katılan her bilgisayar için bir makine nesnesi oluşturulur. Makineler de "güvenlik sorumlusu" olarak kabul edilir ve tıpkı normal bir kullanıcı gibi bir hesap atanır. Bu hesabın etki alanının kendisi içinde biraz sınırlı hakları vardır.

Makine hesapları, atandıkları bilgisayarda yerel yöneticilerdir. Genellikle bilgisayarın kendisi dışında hiç kimse tarafından erişilmemeleri gerekir, ancak diğer tüm hesaplarda olduğu gibi, parolaya sahipseniz, oturum açmak için kullanabilirsiniz.

- **Not:** Makine Hesabı parolaları otomatik olarak döndürülür ve genellikle 120 rastgele karakterden oluşur.
    

Makine hesaplarını tanımlamak nispeten kolaydır. Belirli bir adlandırma şemasını takip ederler. Makine hesabının adı, bilgisayarın adının arkasından gelen bir dolar işaretidir. Örneğin, **DC01** adlı bir makinenin **DC01$** adlı bir makine hesabı olacaktır.

#### Güvenlik Grupları

Windows'a aşinaysanız, dosyalara veya diğer kaynaklara erişim haklarını tek tek kullanıcılar yerine tüm gruplara atamak için kullanıcı gruplarını tanımlayabileceğinizi muhtemelen biliyorsunuzdur. Bu, kullanıcıları mevcut bir gruba ekleyebileceğiniz ve grubun tüm ayrıcalıklarını otomatik olarak miras alacakları için daha iyi bir yönetilebilirlik sağlar. Güvenlik grupları da güvenlik sorumlusu olarak kabul edilir ve bu nedenle ağdaki kaynaklar üzerinde ayrıcalıklara sahip olabilirler.

Gruplar, hem kullanıcıları hem de makineleri üye olarak alabilir. Gerekirse, gruplar başka grupları da içerebilir.

Bir etki alanında, kullanıcılara belirli ayrıcalıkları vermek için kullanılabilecek varsayılan olarak oluşturulmuş birkaç grup vardır. Örnek olarak, bir etki alanındaki en önemli gruplardan bazıları şunlardır:

|Güvenlik Grubu|Açıklama|
|---|---|
|**Etki Alanı Yöneticileri (Domain Admins)**|Bu grubun kullanıcıları, tüm etki alanı üzerinde yönetici ayrıcalıklarına sahiptir. Varsayılan olarak, DC'ler de dahil olmak üzere etki alanındaki herhangi bir bilgisayarı yönetebilirler.|
|**Sunucu İşletmenleri (Server Operators)**|Bu gruptaki kullanıcılar, Etki Alanı Denetleyicilerini yönetebilirler. Yönetici grup üyeliklerini değiştiremezler.|
|**Yedekleme İşletmenleri (Backup Operators)**|Bu gruptaki kullanıcıların, izinlerini dikkate almadan herhangi bir dosyaya erişmesine izin verilir. Bilgisayarlardaki verilerin yedeklerini gerçekleştirmek için kullanılırlar.|
|**Hesap İşletmenleri (Account Operators)**|Bu gruptaki kullanıcılar, etki alanında diğer hesapları oluşturabilir veya değiştirebilir.|
|**Etki Alanı Kullanıcıları (Domain Users)**|Etki alanındaki tüm mevcut kullanıcı hesaplarını içerir.|
|**Etki Alanı Bilgisayarları (Domain Computers)**|Etki alanındaki tüm mevcut bilgisayarları içerir.|
|**Etki Alanı Denetleyicileri (Domain Controllers)**|Etki alanındaki tüm mevcut DC'leri içerir.|

Varsayılan güvenlik gruplarının tam listesini Microsoft belgelerinden alabilirsiniz.

#### Aktif Dizin Kullanıcıları ve Bilgisayarları (Active Directory Users and Computers)

Aktif Dizin'deki kullanıcıları, grupları veya makineleri yapılandırmak için, Etki Alanı Denetleyicisi'ne oturum açıp "Başlat" menüsünden "Active Directory Users and Computers" uygulamasını çalıştırmamız gerekir.

Bu, etki alanında var olan kullanıcıların, bilgisayarların ve grupların hiyerarşisini görebileceğiniz bir pencere açar. Bu nesneler, kullanıcıları ve makineleri sınıflandırmanıza olanak tanıyan **Organizasyonel Birimler (OU'lar)** adı verilen **kapsayıcı** nesneler içinde düzenlenir. OU'lar, esas olarak benzer politika gereksinimleri olan kullanıcı kümelerini tanımlamak için kullanılır. Kuruluşunuzdaki Satış departmanındaki kişilere, örneğin, BT'deki kişilere uygulananlardan farklı bir dizi politika uygulanması muhtemeldir. Bir kullanıcının aynı anda yalnızca tek bir OU'nun parçası olabileceğini unutmayın.

Makinenizi kontrol ederken, BT, Yönetim, Pazarlama, Ar-Ge ve Satış departmanları için beş alt OU içeren **THM** adlı bir OU zaten olduğunu görebiliriz. OU'ların iş yapısını taklit ettiğini görmek çok tipiktir, çünkü bu, tüm departmanlara uygulanan temel politikaların verimli bir şekilde dağıtılmasına olanak tanır. Çoğu zaman beklenen model bu olsa da, OU'ları isteğe bağlı olarak tanımlayabileceğinizi unutmayın. Eğlence için THM OU'ya sağ tıklayıp altına **Students** adlı yeni bir OU oluşturmaktan çekinmeyin.

Herhangi bir OU'yu açarsanız, içerdikleri kullanıcıları görebilir ve gerektiğinde onları oluşturma, silme veya değiştirme gibi basit görevleri gerçekleştirebilirsiniz. Gerekirse parolaları da sıfırlayabilirsiniz (yardım masası için oldukça kullanışlıdır).

Muhtemelen zaten **THM** OU'su dışında başka varsayılan kapsayıcıların da olduğunu fark etmişsinizdir. Bu kapsayıcılar Windows tarafından otomatik olarak oluşturulur ve aşağıdakileri içerir:

- **Builtin:** Herhangi bir Windows ana bilgisayarında bulunan varsayılan grupları içerir.
    
- **Computers:** Ağınıza katılan herhangi bir makine varsayılan olarak buraya konur. Gerekirse onları taşıyabilirsiniz.
    
- **Domain Controllers:** Ağınızdaki DC'leri içeren varsayılan OU'dur.
    
- **Users:** Etki alanı genelinde geçerli olan varsayılan kullanıcılar ve gruplar.
    
- **Managed Service Accounts:** Windows etki alanınızdaki hizmetler tarafından kullanılan hesapları tutar.
    

#### Güvenlik Grupları vs. OU'lar

Muhtemelen hem grupların hem de OU'ların neden olduğunu merak ediyorsunuzdur. Her ikisi de kullanıcıları ve bilgisayarları sınıflandırmak için kullanılsa da, amaçları tamamen farklıdır:

- **OU'lar**, kullanıcılara ve bilgisayarlara **politikalar uygulamak** için kullanışlıdır. Bu, kurumsal organizasyondaki belirli rollerine bağlı olarak kullanıcı kümelerine ait özel yapılandırmaları içerir. Bir kullanıcıya iki farklı politika seti uygulamaya çalışmak mantıklı olmayacağından, bir kullanıcının aynı anda yalnızca tek bir **OU**'nun üyesi olabileceğini unutmayın.
    
- **Güvenlik Grupları** ise **kaynaklar üzerinde izinler vermek** için kullanılır. Örneğin, bazı kullanıcıların paylaşılan bir klasöre veya ağ yazıcısına erişmesine izin vermek istiyorsanız, grupları kullanırsınız. Bir kullanıcının birden fazla gruba üye olması gerekebilir, bu da birden fazla kaynağa erişim izni vermek için gereklidir.