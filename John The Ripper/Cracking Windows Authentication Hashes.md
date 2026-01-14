
# NTHash / NTLM: Windows Kimlik Doğrulama Hash'leri

John the Ripper'ın temel sözdizimini ve kullanımını anladığımıza göre, biraz daha karmaşık bir şeye geçelim; gerçek bir sızma testi veya Red Team çalışmasında karşılaşabileceğiniz bir konu. **Kimlik doğrulama hash'leri (Authentication hashes)**, işletim sistemleri tarafından saklanan parolaların hash'lenmiş versiyonlarıdır. Brute-force (kaba kuvvet) yöntemlerimizi kullanarak bunları kırmak bazen mümkündür. Bu hash'leri ele geçirmek için genellikle zaten ayrıcalıklı (privileged) bir kullanıcı olmanız gerekir; bu nedenle kırmaya çalışacağımız bazı hash'leri deneme yaparken açıklayacağız.

### NTHash / NTLM Nedir?

**NThash**, modern Windows işletim sistemi makinelerinin kullanıcı ve servis parolalarını saklamak için kullandığı hash formatıdır. Bu format yaygın olarak **NTLM** olarak da adlandırılır; bu isim, Windows'un LM (LAN Manager) olarak bilinen önceki parola hash'leme formatına atıfta bulunur, dolayısıyla **NT/LM** olarak bilinir.

**Kısa bir tarihçe:** Windows ürünleri için "NT" ibaresi orijinal olarak "New Technology" (Yeni Teknoloji) anlamına geliyordu. MS-DOS işletim sistemi üzerine inşa edilmemiş ürünleri belirtmek için Windows NT ile kullanılmaya başlandı. Zamanla "NT" serisi, Microsoft tarafından piyasaya sürülen standart işletim sistemi türü haline geldi ve isim bırakıldı, ancak bazı Microsoft teknolojilerinin isimlerinde hala yaşamaya devam ediyor.

---

### Windows'ta Hash'lerin Saklandığı Yer: SAM

Windows'ta **SAM (Security Account Manager - Güvenlik Hesap Yöneticisi)**, kullanıcı adları ve hash'lenmiş parolalar da dahil olmak üzere kullanıcı hesabı bilgilerini saklamak için kullanılır. NTHash/NTLM hash'lerini bir Windows makinesindeki SAM veritabanını **Mimikatz** gibi bir araç kullanarak dökerek (dump) veya Active Directory veritabanı olan **NTDS.dit** dosyasını kullanarak elde edebilirsiniz.

Hak yükseltme (privilege escalation) sürecine devam etmek için hash'i kırmak zorunda kalmayabilirsiniz; çünkü genellikle bunun yerine bir **"pass the hash"** saldırısı gerçekleştirebilirsiniz. Ancak bazen, zayıf bir parola politikası varsa, hash kırma uygulanabilir bir seçenektir.

---

### 🛡️ Siber Güvenlik ve CTF İpucu

1. Pass-the-Hash (PtH) Mantığı:

NThash'in en büyük zayıflığı, orijinal parolayı bilmeden de kullanılabilmesidir. Eğer admin kullanıcısının NTLM hash'ini ele geçirdiysen, bu hash'i doğrudan ağ üzerinden sisteme giriş yapmak için kullanabilirsin. John ile kırmakla vakit kaybetmene gerek kalmaz.

2. NTLM Hash'ini Tanımak:

Bir NTLM hash'i her zaman 32 karakterden oluşan bir Hex (onaltılık) dizisidir. MD5 ile görsel olarak aynıdır.

- **Örnek:** `aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0`
    
- İlk kısım (ilk 32 karakter) genellikle boş bir LM hash'ini temsil eder, ikinci kısım ise gerçek NT hash'idir.
    

3. John ile NTLM Kırma:

John the Ripper'da Windows hash'lerini kırmak için şu format kullanılır:

john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

---

### Özet Karşılaştırma Tablosu

|**Özellik**|**NTLM (NThash)**|**LM (Legacy)**|
|---|---|---|
|**İşletim Sistemi**|Modern Windows (10, 11, Server)|Eski Windows (95, 98, XP)|
|**Güvenlik**|Orta (MD4 tabanlıdır)|Çok Zayıf (Kırılması saniyeler sürer)|
|**Büyük/Küçük Harf**|Duyarlı|Duyarlı Değil (Hepsi büyük harfe çevrilir)|
|**John Formatı**|`--format=nt`|`--format=lm`|