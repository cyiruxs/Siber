### **JavaScript (JS) Nedir ve Ne İşe Yarar?**

**JavaScript (JS)**, dünyanın en popüler programlama dillerinden biridir ve **web sayfalarına etkileşim kazandırır**.

- **HTML**, web sitesinin **yapısını ve içeriğini** oluşturur.
- **JavaScript**, sayfanın **işlevselliğini** kontrol eder.

Eğer bir web sitesinde **JavaScript olmasaydı, sayfa yalnızca statik olurdu** ve etkileşimli öğeler (butonlar, animasyonlar, dinamik içerikler vb.) bulunmazdı. **JavaScript, sayfanın içeriğini gerçek zamanlı olarak değiştirebilir.**

### **JavaScript Nasıl Eklenir?**

JavaScript kodu **sayfa kaynağına** eklenebilir. İki farklı yöntem vardır:

1. **HTML içine `<script>` etiketiyle ekleme**
    
    ```html
    <script>
        alert("Merhaba Dünya!");
    </script>
    ```
    
2. **Harici bir dosyadan yükleme (`src` ile)**
    
    ```html
    <script src="/location/of/javascript_file.js"></script>
    ```
    

### **JavaScript ile HTML Elemanlarını Değiştirme**

Aşağıdaki kod, sayfada **id'si "demo" olan bir HTML elemanını bulur** ve içeriğini **"Hack the Planet"** olarak değiştirir:

```javascript
document.getElementById("demo").innerHTML = "Hack the Planet";
```

### **JavaScript ile Etkileşim (Event Kullanımı)**

HTML elemanları, belirli olaylar gerçekleştiğinde **JavaScript kodları çalıştırabilir**.

#### **Butona Tıklayınca (`onclick`) İçeriği Değiştirme**

Aşağıdaki kod, butona tıklanınca **id'si "demo" olan elemanın içeriğini "Button Clicked" olarak değiştirir**:

```html
<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>
```

**Not:** `onclick` gibi olaylar doğrudan HTML elemanlarına eklenebildiği gibi, **JavaScript dosyasında ayrı olarak da tanımlanabilir**.