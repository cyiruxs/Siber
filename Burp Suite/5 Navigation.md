**Burp Suite**'te varsayılan navigasyon öncelikle, modüller arasında geçiş yapmanıza ve her modül içindeki çeşitli alt sekmelere (sub-tabs) erişmenize olanak tanıyan üst menü çubukları aracılığıyla yapılır. Alt sekmeler, ana menü çubuğunun hemen altında ikinci bir menü çubuğunda görünür.

Navigasyon şu şekilde çalışır:

- **Modül Seçimi (Module Selection):** Menü çubuğunun üst satırı, Burp Suite'teki kullanılabilir modülleri görüntüler. Aralarında geçiş yapmak için her modülün üzerine tıklayabilirsiniz. Örneğin, aşağıdaki görselde Burp **Proxy** modülü seçilidir.
    
- **Alt Sekmeler (Sub-Tabs):** Seçilen bir modülün birden fazla alt sekmesi varsa, bunlara ana menü çubuğunun hemen altında görünen ikinci menü çubuğundan erişilebilir. Bu alt sekmeler genellikle modüle özgü ayarları ve seçenekleri içerir. Örneğin, yukarıdaki görselde, Burp **Proxy** modülü içinde **Proxy Intercept** alt sekmesi seçilidir.
    
- **Sekmeleri Ayırmak (Detaching Tabs):** Birden fazla sekmeyi ayrı ayrı görüntülemeyi tercih ederseniz, bunları ayrı pencerelere ayırabilirsiniz. Bunu yapmak için, **Module Selection** çubuğunun üzerindeki uygulama menüsünde bulunan **Window** seçeneğine gidin. Oradan "Detach" seçeneğini seçtiğinizde, seçili sekme ayrı bir pencerede açılacaktır. Ayrılan sekmeler aynı yöntem kullanılarak tekrar eklenebilir (reattached).
    

**Burp Suite** ayrıca temel sekmelere hızlı navigasyon için klavye kısayolları sağlar. Varsayılan olarak aşağıdaki kısayollar mevcuttur:

| **Kısayol**          | **Sekme**        |
| -------------------- | ---------------- |
| **Ctrl + Shift + D** | Dashboard        |
| **Ctrl + Shift + T** | Target sekmesi   |
| **Ctrl + Shift + P** | Proxy sekmesi    |
| **Ctrl + Shift + I** | Intruder sekmesi |
| **Ctrl + Shift + R** | Repeater sekmesi |