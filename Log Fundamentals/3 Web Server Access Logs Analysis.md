## Web Sunucusu Log Analizi (Apache Access Logs)

Günlük olarak birçok web sitesiyle etkileşime gireriz. Bazen sadece web sitesini görüntülemek isteriz, bazen de giriş yapmak veya mevcut herhangi bir giriş alanına bir dosya yüklemek isteriz. Bunlar, bir web sitesine yaptığımız farklı istek (**request**) türleridir. Tüm bu istekler web sitesi tarafından günlüğe kaydedilir ve o web sitesini çalıştıran web sunucusundaki bir **log file** içerisinde saklanır.

Bu **log** dosyası; web sitesine yapılan tüm istekleri, zaman dilimi, istek yapılan IP (**requested IP**), istek türü ve URL bilgileriyle birlikte içerir. Aşağıda, `/var/log/apache2/access.log` dizininde bulunan bir **Apache** web sunucusu erişim günlüğü dosyasından alınmış örnek alanlar yer almaktadır:

- **IP Address:** “172.16.0.1” - İsteği yapan kullanıcının IP adresi.
    
- **Timestamp:** “[06/Jun/2024:13:58:44]” - İsteğin web sitesine yapıldığı zaman.
    
- **Request:** İstek detayları.
    
    - **HTTP Method:** “GET” - Web sitesine istek üzerinde hangi eylemin gerçekleştirileceğini söyler.
        
    - **URL:** “/” - İstenen kaynak (**requested resource**).
        
    - **Status Code:** “200” - Sunucudan gelen yanıt. Farklı numaralar farklı yanıt sonuçlarını gösterir.
        
- **User-Agent:** “Mozilla/5.0...” - İsteği yaparken kullanıcının İşletim Sistemi (**Operating System**), tarayıcı vb. bilgileri.
    

### Linux Komut Satırı ile Manuel Log Analizi

**Linux** işletim sistemindeki bazı komut satırı araçlarını kullanarak manuel **log analysis** gerçekleştirebiliriz. İşte bu süreçte faydalı olabilecek bazı komutlar:

#### 1. cat

`cat`, bir metin dosyasının içeriğini görüntülemek için popüler bir araçtır. **Log** dosyaları genellikle metin formatında olduğu için içeriklerini görüntülemek için `cat` komutunu kullanabiliriz.

Bash

```
root@kali$ cat access.log
172.16.0.1 - - [06/Jun/2024:13:58:44] "GET /products HTTP/1.1" 404 "-" "Mozilla/5.0..."
10.0.0.1 - - [06/Jun/2024:13:57:44] "GET / HTTP/1.1" 404 "-" "Mozilla/5.0..."
```

Çoğu sistem **log**'ları düzenli olarak döndürür (**rotate**). Bu döndürme işlemi, belirli zaman dilimleri için ayrı **log** dosyaları oluşturulmasına ve her şeyin tek bir dosyada birikmemesine yardımcı olur. Ancak bazen iki **log** dosyasını birleştirmemiz gerekebilir. `cat` aracı bu durumda da yardımcı olabilir:

Bash

```
root@kali$ cat access1.log access2.log > combined_access.log
```

#### 2. grep

`grep`, bir **log** dosyası içinde dizgileri (**strings**) ve desenleri (**patterns**) aramanıza olanak tanıyan çok kullanışlı bir komut satırı aracıdır. Örneğin, belirli bir IP adresinin **log** dosyanızda mevcut olup olmadığını araştırmanız gerekebilir:

Bash

```
root@kali$ grep "192.168.1.1" access.log
192.168.1.1 - - [06/Jun/2024:13:56:44] "GET /about HTTP/1.1" 500 "-" "Mozilla/5.0..."
```

#### 3. less

`less` komutu, çok sayıda veya büyük **log** dosyalarını yönetmek için kullanışlıdır. Belirli bölümleri sayfa sayfa analiz etmeniz gerekebilir.

Bash

```
root@kali$ less access.log
```

- **Spacebar (Boşluk tuşu):** Bir sonraki sayfaya geçmek için kullanılır.
    
- **b:** Önceki sayfaya dönmek için kullanılır.
    
- **/:** Bir desen aramak için `/` yazıp ardından aradığınız terimi yazarak Enter'a basın.
    
- **n:** Aramanızın bir sonraki sonucuna gitmek için kullanılır.
    
- **N:** Aramanızın bir önceki sonucuna gitmek için kullanılır.