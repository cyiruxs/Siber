# Packet Numbers

Wireshark, incelenen packet’ların sayısını hesaplar ve her packet için benzersiz bir numara atar. Bu, büyük capture’lar için analiz sürecini kolaylaştırır ve bir olayın belirli bir noktasına geri dönmeyi pratik hale getirir.

---

## Go to Packet

Packet number’lar yalnızca toplam packet sayısını görmek veya belirli packet’ları daha kolay bulup incelemek için kullanılmaz. Bu özellik sadece packet’lar arasında yukarı ve aşağı gezinmeyi sağlamaz; aynı zamanda frame içi packet takibini yapar ve belirli bir conversation’ın ilgili bölümündeki bir sonraki packet’ı bulur.  
Belirli packet’ları görüntülemek için **"Go (Ctrl+G)"** menüsünü ve toolbar’ı kullanabilirsiniz. 

---

## Find Packets

Packet number’a ek olarak, Wireshark packet content’e göre de packet bulabilir. **"Edit --> Find Packet(Ctrl+F)"** menüsünü kullanarak packet’lar içinde ilgilenilen belirli bir olayı arayabilirsiniz. Bu özellik, analyst ve administrator’ların belirli intrusion pattern’larını veya failure trace’lerini bulmasına yardımcı olur.

Packet bulma işlemi sırasında iki kritik nokta vardır:

### 1. Input Type’ı Bilmek  
Bu fonksiyon dört tür input kabul eder:

- Display filter  
- Hex  
- String  
- Regex  

String ve regex aramaları en sık kullanılan arama türleridir. Aramalar varsayılan olarak case insensitive’dir, ancak radio button’a tıklayarak case sensitivity ayarlanabilir.

### 2. Search Field Seçimi  
Aramalar üç pane üzerinde yapılabilir:

- packet list  
- packet details  
- packet bytes  

İlgilenilen bilginin hangi pane’de bulunduğunu bilmek önemlidir. Örneğin, packet details pane içinde bulunan bir bilgiyi packet list pane’de ararsanız, bilgi mevcut olsa bile Wireshark sonucu bulamaz.

---

## Mark Packets

Packet işaretleme, analyst’ler için oldukça faydalı bir başka özelliktir. Belirli bir packet’ı daha sonra incelemek üzere işaretleyebilirsiniz. Bu, ilgilenilen bir olaya dikkat çekmeyi veya capture’dan belirli packet’ları export etmeyi kolaylaştırır.  
Packet’ları işaretlemek veya işaretini kaldırmak için **"Edit"** menüsünü veya **right-click (Ctrl+M)** menüsünü kullanabilirsiniz.

İşaretlenen packet’lar, bağlantı türünü temsil eden orijinal renkten bağımsız olarak siyah renkte gösterilir.  
Not: İşaretli packet bilgileri yalnızca mevcut file session boyunca geçerlidir. Capture file kapatıldığında işaretli packet’lar kaybolur.

---

## Packet Comments

Packet işaretlemeye benzer şekilde, commenting de analyst’ler için faydalı bir özelliktir. Belirli packet’lara yorum ekleyerek daha sonraki incelemeler için notlar bırakabilir veya diğer layer analyst’leri için önemli/şüpheli noktaları vurgulayabilirsiniz.  
Packet marking’in aksine, comments capture file içinde saklanır ve operator kaldırana kadar kalıcıdır.

---

## Export Packets

Capture file’lar tek bir dosyada binlerce packet içerebilir. Daha önce belirtildiği gibi, Wireshark bir IDS değildir. Bu nedenle bazen belirli packet’ları dosyadan ayırıp daha derin analiz yapmak gerekir.  
Bu özellik, analyst’lerin yalnızca şüpheli packet’ları (belirlenen scope) paylaşmasına olanak tanır ve gereksiz bilgilerin analiz sürecine dahil edilmesini önler. Packet export etmek için **"File"** menüsünü kullanabilirsiniz.

---

## Export Objects (Files)

Wireshark, wire üzerinden transfer edilen dosyaları extract edebilir. Bir security analyst için paylaşılan dosyaları tespit etmek ve daha ileri inceleme için kaydetmek hayati önem taşır.  
Object export işlemi yalnızca belirli protocol stream’leri için kullanılabilir:

- DICOM  
- HTTP  
- IMF  
- SMB  
- TFTP  

---

## Time Display Format

Wireshark, packet’ları yakalandıkları sıraya göre listeler; bu nedenle varsayılan akış her zaman en iyi inceleme yöntemi olmayabilir.  
Varsayılan olarak Wireshark zamanı **"Seconds Since Beginning of Capture"** formatında gösterir. Yaygın kullanım ise daha net bir görünüm için **UTC Time Display Format** kullanmaktır.  
Zaman formatını değiştirmek için **"View --> Time Display Format"** menüsünü kullanabilirsiniz.

---

## Expert Info

Wireshark, analyst’lerin olası anormallikleri ve problemleri kolayca fark edebilmesi için protocol’lerin belirli durumlarını da tespit eder. Bunların yalnızca birer öneri olduğunu ve false positive/negative olasılığı bulunduğunu unutmayın.

Expert info, üç farklı severity seviyesinde kategoriler sunar. Detaylar aşağıdaki tabloda gösterilmiştir:

| Severity | Colour | Info |
|--------|--------|------|
| Chat | Blue | Normal workflow hakkında bilgi |
| Note | Cyan | Application error code’ları gibi dikkat çekici olaylar |
| Warn | Yellow | Olağandışı error code’lar veya problem ifadeleri |
| Error | Red | Malformed packet gibi ciddi problemler |

Sık karşılaşılan information group’ları aşağıda listelenmiştir:

| Group | Info | Group | Info |
|------|------|-------|------|
| Checksum | Checksum errors | Deprecated | Deprecated protocol kullanımı |
| Comment | Packet comment detection | Malformed | Malformed packet detection |

Tüm expert info kayıtlarını görmek için status bar’daki **"lower left bottom section"** veya **"Analyse --> Expert Information"** menüsünü kullanabilirsiniz. Açılan dialogue box; packet number, summary, group, protocol ve toplam occurrence bilgilerini gösterir.
