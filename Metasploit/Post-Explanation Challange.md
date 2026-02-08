Daha önce bahsedilen `getsystem` ve `hashdump` gibi komutlar, yetki yükseltme (privilege escalation) ve yanal hareket (lateral movement) için önemli avantajlar ve bilgiler sağlayacaktır. **Meterpreter**, Metasploit framework'ünde bulunan sızma sonrası modülleri çalıştırmak için kullanabileceğiniz iyi bir temeldir. Son olarak, **Kiwi** ve hatta tüm **Python** dilini kullanmak gibi ek araçlardan faydalanmak için `load` komutunu kullanabilirsiniz.

### Python Yükleme

Bash

```
meterpreter > load python
Loading extension python...Success.
meterpreter > python_execute "print 'TryHackMe Rocks!'"
[+] Content written to stdout:
TryHackMe Rocks!
```

Sızma sonrası (post-exploitation) aşamasının birkaç hedefi vardır; Meterpreter, bunların hepsine yardımcı olabilecek fonksiyonlara sahiptir:

- Hedef sistem hakkında daha fazla bilgi toplamak.
    
- Hedef sistemde ilginç dosyalar, kullanıcı kimlik bilgileri, ek ağ arayüzleri ve genel olarak ilgi çekici bilgiler aramak.
    
- Yetki yükseltme (Privilege escalation).
    
- Yanal hareket (Lateral movement).
    

`load` komutu kullanılarak herhangi bir ek araç yüklendiğinde, `help` menüsünde yeni seçenekler göreceksiniz. Aşağıdaki örnek, Kiwi modülü yüklendikten sonra eklenen komutları göstermektedir (`load kiwi` komutu kullanılarak).

### Kiwi Yükleme

Bash

```
meterpreter > load kiwi
Loading extension kiwi...
  .#####.   mimikatz 2.2.0 20191125 (x64/windows)
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
...
Success.
```

Bu komutlar yüklenen menüye göre değişecektir, bu nedenle bir modülü yükledikten sonra `help` komutunu çalıştırmak her zaman iyi bir fikirdir.

---

## Siber Güvenlik Analizi ve İpuçları

Metinde geçen araçlar ve teknikler, modern bir sızma testinin en kritik aşamalarını temsil eder.

### 1. Kiwi (Mimikatz) Nedir?

`load kiwi`, aslında ünlü **Mimikatz** aracını Meterpreter içine entegre eder. Mimikatz, Windows sistemlerdeki bellekten (LSASS süreci) açık metin şifreleri, hash'leri (NTLM) ve Kerberos biletlerini çekmek için kullanılır.

- **CTF İpucu:** Eğer bir Windows makinesinde `SYSTEM` yetkisine ulaştıysanız, ilk yapmanız gereken `load kiwi` ardından `creds_all` komutunu çalıştırmaktır. Bu, makinedeki tüm kayıtlı kullanıcı şifrelerini veya hash'lerini dökmenizi sağlar.
    

### 2. Sızma Sonrası Temel Hedefler Tablosu

|**Hedef**|**Meterpreter Komutu / Modülü**|**Açıklama**|
|---|---|---|
|**Bilgi Toplama**|`sysinfo`, `getuid`, `ipconfig`|İşletim sistemi, kullanıcı adı ve ağ yapılandırmasını öğrenme.|
|**Yetki Yükseltme**|`getsystem`, `suggest`|Normal kullanıcıdan Admin/System yetkisine geçiş yollarını arama.|
|**Parola Avcılığı**|`hashdump`, `load kiwi`|SAM veritabanını dökme veya bellekten şifre çalma.|
|**Yanal Hareket**|`portfwd`, `autoroute`|Hedef makineyi bir köprü (pivot) olarak kullanarak iç ağa sızma.|

### 3. Savunma Tarafı (Mavi Takım) Notu

Meterpreter modülleri bellekte çalıştığı için (fileless), geleneksel antivirüslerden kaçabilir. Ancak, `load kiwi` gibi komutlar LSASS sürecine müdahale ettiği için modern **EDR (Endpoint Detection and Response)** çözümleri tarafından kolayca fark edilir. Bir saldırgan olarak bu araçları kullanmadan önce `getprivs` ile mevcut yetkilerinizi kontrol etmelisiniz.

---

## Sızma Sonrası Yaşam Döngüsü

### CTF İpuçları:

- **Python Gücü:** `load python` komutu, hedef sistemde Python yüklü olmasa bile sizin Meterpreter üzerinden Python scriptleri çalıştırmanıza olanak tanır. Bu, karmaşık otomasyonlar için hayat kurtarıcıdır.
    
- **Help Komutunu Unutma:** Her yeni modül yüklediğinizde mutlaka `help` yazın. Bazı modüller (`kiwi`, `incognito`) sadece belirli yetki seviyelerinde çalışan çok özel komutlar ekler.