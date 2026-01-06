## Packet Filtering

Wireshark, analistlerin trafiği daraltmasına ve ilgi duyulan olaya odaklanmasına yardımcı olan güçlü bir **filter engine**’e sahiptir. Wireshark’ta iki tür filtreleme yaklaşımı vardır: **capture filters** ve **display filters**. **Capture filters**, kullanılan filtreye uygun paketlerin _yakalanması_ için kullanılır. **Display filters** ise kullanılan filtreye uygun paketlerin _görüntülenmesi_ için kullanılır. Bu filtrelerin farkları ve gelişmiş kullanımı bir sonraki odada ele alınacaktır. Şimdilik analistlere ilk aşamada yardımcı olan **display filters**’ın temel kullanımına odaklanacağız.

Filtreler, Wireshark’ın resmi **protocol reference**’ında bulunan protokoller için tasarlanmış özel sorgulardır. Filtreler ilgi duyulan olayı incelemek için tek seçenek olmasa da, yakalama dosyasındaki gürültüyü azaltmak için trafiği filtrelemenin iki farklı yolu vardır. Birincisi sorguların kullanılması, ikincisi ise **right-click menu**’nün kullanılmasıdır. Wireshark güçlü bir GUI sağlar ve temel işlemler için sorgu yazmak istemeyen analistler için altın bir kural vardır:

> **If you can click on it, you can filter and copy it**

---

## Apply as Filter

Bu, trafiği filtrelemenin en temel yoludur. Bir capture file incelenirken, filtrelemek istenen alana tıklanarak **right-click menu** veya **Analyse → Apply as Filter** menüsü kullanılabilir. Filtre uygulandığında Wireshark gerekli **filter query**’yi oluşturur, filtreyi uygular, seçilen paketleri gösterir ve seçilmeyen paketleri **packet list pane**’den gizler. **Status bar** üzerinde her zaman toplam paket sayısı ve görüntülenen paket sayısı gösterilir.

---

## Conversation Filter

**Apply as Filter** seçeneği yalnızca paketteki tek bir varlığı filtreler. Ancak belirli bir **packet number** ve ona bağlı IP adresleri ile port numaralarına odaklanarak ilişkili tüm paketleri incelemek istendiğinde **Conversation Filter** seçeneği kullanılır. Bu seçenek yalnızca ilgili paketleri görüntüler ve diğer paketleri gizler. **Right-click menu** veya **Analyse → Conversation Filter** menüsü kullanılarak uygulanabilir.

---

## Colourise Conversation

Bu seçenek **Conversation Filter** ile benzerdir ancak bir farkı vardır. İlgili paketleri renklendirir ancak **display filter** uygulamaz ve görüntülenen paket sayısını azaltmaz. Bu özellik **Colouring Rules** ile çalışır ve daha önce uygulanmış renk kurallarını dikkate almadan paket renklerini değiştirir. **Right-click menu** veya **View → Colourise Conversation** menüsü kullanılarak uygulanabilir. Yapılan işlem **View → Colourise Conversation → Reset Colourisation** menüsü ile geri alınabilir.

---

## Prepare as Filter

Bu seçenek **Apply as Filter** ile benzerdir ve **right-click menu** üzerinden display filter oluşturulmasını sağlar. Ancak bu yöntemde filtre hemen uygulanmaz. Gerekli **filter query**, filtreleme çubuğuna eklenir ve çalıştırma için **Enter** tuşunun kullanılması veya **right-click menu** içindeki `.. and/or ..` seçenekleriyle başka filtrelerin eklenmesi beklenir.

---

## Apply as Column

Varsayılan olarak **packet list pane**, her paket için temel bilgileri gösterir. **Right-click menu** veya **Analyse → Apply as Column** menüsü kullanılarak seçilen değer sütun olarak eklenebilir. Bir değer sütun olarak eklendiğinde **packet list pane**’de görünür ve capture file’daki paketler boyunca ilgili alanın görünümü incelenebilir. **Packet list pane**’in üst kısmına tıklanarak gösterilen sütunlar etkinleştirilebilir veya devre dışı bırakılabilir.

---

## Follow Stream

Wireshark her şeyi paket boyutlarında gösterir. Ancak stream’leri yeniden oluşturmak ve trafiği uygulama katmanında sunulduğu haliyle görmek mümkündür. **Follow Stream** özelliği, uygulama katmanı verilerinin yeniden oluşturulmasını sağlar ve ilgi duyulan olayın anlaşılmasına yardımcı olur. Şifrelenmemiş protokollerde **username**, **password** ve aktarılan diğer veriler görüntülenebilir.

**Right-click menu** veya **Analyse → Follow TCP/UDP/HTTP Stream** menüsü kullanılarak stream’ler takip edilebilir. Stream’ler ayrı bir pencerede gösterilir; **server** kaynaklı paketler mavi, **client** kaynaklı paketler kırmızı renkle vurgulanır.

Bir stream takip edildiğinde Wireshark gerekli **display filter**’ı otomatik olarak oluşturur ve uygular. Filtre uygulandığında görüntülenen paket sayısı değişir. Capture file’daki tüm paketleri tekrar görüntülemek için display filter bar’ın sağ üst kısmındaki **X** butonu kullanılarak filtre kaldırılmalıdır.

---