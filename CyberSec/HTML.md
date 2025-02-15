### **Web Siteleri Hangi Teknolojilerle Oluşturulur?**

Web siteleri genellikle aşağıdaki teknolojiler kullanılarak oluşturulur:

- **HTML** → Web sitelerinin yapısını oluşturur.
- **CSS** → Web sitelerini görsel olarak düzenler, stiller ekler.
- **JavaScript** → Web sayfalarına etkileşim ve dinamik özellikler ekler.

### **HTML ve Temel Yapısı**

**HTML (HyperText Markup Language)**, web sitelerinin yazıldığı dildir. **Etiketler (tags)**, HTML sayfalarının yapı taşlarıdır ve tarayıcıya içeriği nasıl görüntülemesi gerektiğini söyler. Aşağıda, her web sitesinde bulunan temel bir HTML yapısı yer almaktadır:
![[example_html.png]]
#### **HTML Yapısının Bileşenleri**

1. **`<!DOCTYPE html>`** → Sayfanın **HTML5** belgesi olduğunu belirtir. Bu, tarayıcıların sayfayı nasıl yorumlayacağını standart hale getirir.
2. **`<html>`** → HTML sayfasının kök (root) elemanıdır, tüm diğer elemanlar bunun içinde bulunur.
3. **`<head>`** → Sayfa hakkında bilgileri içerir (**başlık, meta veriler, CSS dosyaları** vb.).
4. **`<body>`** → Sayfanın içeriğini barındırır. **Tarayıcıda görüntülenen her şey burada yer alır.**
5. **`<h1>`** → Büyük başlıkları tanımlar.
6. **`<p>`** → Paragrafları tanımlar.

Bunlara ek olarak, **butonlar (`<button>`), resimler (`<img>`), listeler (`<ul>`, `<ol>`, `<li>`)** ve daha birçok HTML etiketi bulunmaktadır.

### **HTML Etiketlerinde Kullanılan Özellikler (Attributes)**

- **`class`** → Elemanı CSS ile biçimlendirmek için kullanılır.
    
    ```html
    <p class="bold-text">Bu bir paragraf.</p>
    ```
    
- **`src`** → Resimlerin kaynağını belirtir.
    
    ```html
    <img src="img/cat.jpg">
    ```
    
- **`id`** → Bir elemanı benzersiz şekilde tanımlar (JavaScript veya CSS için kullanılır).
    
    ```html
    <p id="example">Bu bir örnek metindir.</p>
    ```
    
    **Not:** Birden fazla eleman **aynı `class` değerini** alabilir, ancak **`id` değerleri benzersiz olmalıdır.**

### **Bir Web Sitesinin HTML Kodunu Görüntüleme**

Bir web sitesinin HTML kodunu incelemek için:

- **Chrome:** Sağ tıklayıp **"View Page Source"** seçeneğine tıklayın.
- **Safari:** Sağ tıklayıp **"Show Page Source"** seçeneğine tıklayın.