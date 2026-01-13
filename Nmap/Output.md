Bu görev iki ana özelliğe odaklanmaktadır: tarama devam ederken ek bilgilerin görüntülenmesi ve tarama raporunun kaydedileceği dosya formatının seçilmesi.

---

## Verbosity (Ayrıntı) ve Debugging (Hata Ayıklama)

Bazı durumlarda taramanın tamamlanması veya ekranda bir çıktı üretmesi çok uzun sürebilir. Tarama ilerlemesi hakkında gerçek zamanlı bilgi almak için en iyi yol, `-v` seçeneğini ekleyerek **verbose** (ayrıntılı) çıktıyı etkinleştirmektir.

Aşağıdaki terminal çıktılarında farkı görebilirsiniz:

- **Varsayılan Çıktı:** Sadece tarama bittiğinde özet bilgi verir.
    
- **`-v` Çıktısı:** Nmap'in hangi aşamada olduğunu (ARP ping scan, DNS resolution, SYN stealth scan) ve açık portları bulduğu anı anlık olarak gösterir.
    

Daha fazla ayrıntıya ihtiyaç duyarsanız:

- **`-vv`** veya **`-v2`**: Ayrıntı seviyesini daha da artırır.
    
- **`-d`**: **Debugging** (hata ayıklama) seviyesinde çıktı verir. En yüksek seviye `-d9`'dur ve binlerce satır teknik bilgi üretir.
    
- **İpucu:** Tarama başladıktan sonra klavyeden `v` tuşuna basarak ayrıntı seviyesini dinamik olarak artırabilirsiniz.
    

---

## Saving Scan Report (Tarama Raporunu Kaydetme)

Tarama sonuçlarını daha sonra incelemek veya başka araçlarla kullanmak için kaydetmek isteyebilirsiniz. Nmap üç ana format sunar:

1. **`-oN <dosya_adı>` (Normal):** İnsanlar tarafından okunması kolay, terminal çıktısına benzer format.
    
2. **`-oX <dosya_adı>` (XML):** Yazılımlar tarafından işlenmeye uygun format.
    
3. **`-oG <dosya_adı>` (Grepable):** `grep`, `awk` veya `cut` gibi komut satırı araçlarıyla kolayca taranabilen format.
    
4. **`-oA <temel_ad>` (All):** Yukarıdaki üç formatın hepsinde birden çıktı alır (`.nmap`, `.xml` ve `.gnmap` uzantılarıyla).
    

**Örnek kullanım:**

Bash

```
root@tryhackme:~# nmap -sS 192.168.139.1 -oA gateway
```

Bu komut sonucunda `gateway.nmap`, `gateway.xml` ve `gateway.gnmap` dosyaları oluşturulur.

---

## Özet

| **Seçenek**      | **Açıklama**                                   |
| ---------------- | ---------------------------------------------- |
| **`-v` / `-vv`** | Çıktı ayrıntı seviyesini artırır               |
| **`-d`**         | Hata ayıklama (debugging) bilgilerini gösterir |
| **`-oN`**        | Sonucu normal (okunabilir) formatta kaydeder   |
| **`-oX`**        | Sonucu XML formatında kaydeder                 |
| **`-oG`**        | Sonucu `grep` komutuna uygun formatta kaydeder |
| **`-oA`**        | Sonucu tüm ana formatlarda kaydeder            |