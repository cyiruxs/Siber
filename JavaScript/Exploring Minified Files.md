# 🧩 JavaScript Minification, Obfuscation ve Deobfuscation

Şu ana kadar JS'nin nasıl çalıştığını ve nasıl okunacağını anladık; ancak ya dosya insan tarafından okunamaz durumdaysa ve **minified** edilmişse?

### Minification (Minimizasyon)

JS'de **Minification**, JS dosyalarını boşluklar, satır sonları, yorumlar gibi tüm gereksiz karakterleri kaldırarak ve hatta değişken isimlerini kısaltarak sıkıştırma işlemidir. Bu, dosya boyutunu küçültmeye yardımcı olur ve özellikle canlı (production) ortamlarda web sayfalarının yükleme süresini iyileştirir. Minified dosyalar kodu daha kompakt ve insanlar için okunması daha zor hale getirir, ancak yine de tamamen aynı şekilde işlev görürler.

### Obfuscation (Karmaşıklaştırma)

Benzer şekilde **Obfuscation**, istenmeyen kodlar ekleyerek, değişken ve fonksiyon isimlerini anlamsız adlarla değiştirerek ve hatta sahte (dummy) kodlar yerleştirerek JS'yi anlaşılması daha zor hale getirmek için sıklıkla kullanılır.

---

## 🛠️ Pratik Örnek

Ekteki VM'nin (Sanal Makine) Masaüstünde `hello.html` adında bir dosya oluşturun ve aşağıdaki HTML kodunu yapıştırın:

HTML

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Obfuscated JS Code</title>
</head>
<body>
    <h1>Obfuscated JS Code</h1>
    <script src="hello.js"></script>
</body>
</html>
```

Ardından, `hello.js` adıyla başka bir dosya oluşturun ve şu kodu ekleyin:

JavaScript

```
function hi() {
  alert("Welcome to THM");
}
hi();
```

Şimdi, `hello.html` dosyasını Google Chrome'da açmak için çift tıklayın. Dosya açıldığında, sizi "Welcome to THM" mesajıyla karşılayan bir alert göreceksiniz.

Alert diyalog kutusunu kapatmak için **OK**'e tıklayın. Sayfanın herhangi bir yerine sağ tıklayın ve geliştirici araçlarını açmak için **Inspect** (İncele) öğesine tıklayın. Geliştirici araçlarında **Sources** sekmesine gidin ve kaynak kodu görüntülemek için `hello.js` dosyasına tıklayın. JS kodunun aşağıda gösterildiği gibi kolayca erişilebilir ve görüntülenebilir olduğunu göreceksiniz.

---

## 🎭 Obfuscation İş Başında

Şimdi, çevrimiçi bir araç kullanarak JS kodunu minify ve obfuscate etmeyi deneyeceğiz. İlgili web sitesini ziyaret edin, `hello.js` içeriğini kopyalayın ve web sitesindeki diyalog kutusuna yapıştırın. Araç, kodu minify ve obfuscate ederek aşağıda gösterilen anlamsız karakter dizisine dönüştürecektir:

Peki ya size bu anlamsız karakterlerin hala tam fonksiyonel kodlar olduğunu söylesek? Tek fark, insan tarafından okunabilir olmamalarıdır; ancak tarayıcı bunları hala doğru bir şekilde çalıştırabilir. Web sitesi JS kodumuzu şuna dönüştürdü:

JavaScript

```
(function(_0x114713,_0x2246f2){var _0x51a830=_0x33bf,_0x4ce60b=_0x114713();while(!![]){try{var _0x51ecd3=-parseInt(_0x51a830(0x88))/(-0x1bd3+-0x9a+0x2*0xe37)*(parseInt(_0x51a830(0x94))/(-0x15c1+-0x2*-0x3b3+0xe5d))+parseInt(_0x51a830(0x8d))/(0x961*0x1+0x2*0x4cb+0x4bd*-0x4)*(-parseInt(_0x51a830(0x97))/(-0x22b3+0x16e9+0x1*0xbce))+parseInt(_0x51a830(0x89))/(-0x631+0x20cd+0x8dd*-0x3)*(-parseInt(_0x51a830(0x95))/(-0x8fc+0x161+0x7a1))+-parseInt(_0x51a830(0x93))/(-0x1c38+0x193+0x1aac)*(parseInt(_0x51a830(0x8e))/(-0x1*-0x17a6+-0x167e+-0x3*0x60))+-parseInt(_0x51a830(0x91))/(-0x2*-0x1362+-0x4a8*0x5+-0xf73)*(parseInt(_0x51a830(0x8b))/(-0xb31*0x2+0x493*0x5+0x1*-0x73))+parseInt(_0x51a830(0x8f))/(-0x257a+-0x1752+0x3cd7)+parseInt(_0x51a830(0x90))/(-0x2244+-0x15f9+0x3849);if(_0x51ecd3===_0x2246f2)break;else _0x4ce60b['push'](_0x4ce60b['shift']());}catch(_0x38d15c){_0x4ce60b['push'](_0x4ce60b['shift']());}}}(_0x11ed,-0x17d11*-0x1+0x2*0x2e27+0x100f*0x17));function hi(){var _0x48257e=_0x33bf,_0xab1127={'xMVHQ':function(_0x4eefa0,_0x4e5f74){return _0x4eefa0(_0x4e5f74);},'FvtWc':_0x48257e(0x96)+_0x48257e(0x92)};_0xab1127[_0x48257e(0x8c)](alert,_0xab1127[_0x48257e(0x8a)]);}function _0x33bf(_0xb07259,_0x5949fe){var _0x3a386b=_0x11ed();return _0x33bf=function(_0x4348ee,_0x1bbf73){_0x4348ee=_0x4348ee-(0x11f7+-0x1*0x680+-0x3a5*0x3);var _0x423ccd=_0x3a386b[_0x4348ee];return _0x423ccd;},_0x33bf(_0xb07259,_0x5949fe);}function _0x11ed(){var _0x4c8fa8=['7407EbJESQ','\x20THM','2700698TTmqXC','10ILFtfZ','190500QONgph','Welcome\x20to','4492QOmepo','21623eEAyaP','65XMlsxw','FvtWc','2410qfnGAy','xMVHQ','321PfYXZg','8XBaIAe','1946483GviJfa','15167592PYYhTN'];_0x11ed=function(){return _0x4c8fa8;};return _0x11ed();}hi();
```

Web sitesinde gösterildiği gibi **Copy to Clipboard** butonuna tıklayın. Ardından, ekli VM'deki `hello.js` dosyasının mevcut içeriğini kaldırın ve obfuscated içeriği dosyaya yapıştırın.

`hello.html` dosyasını Google Chrome'da yeniden yükleyin ve **Sources** sekmesi altında kaynak kodu tekrar inceleyin. Kodun artık obfuscate edildiğini ancak hala daha öncekiyle tam olarak aynı şekilde çalıştığını fark edeceksiniz.

---

## 🔓 Deobfuscating a Code (Kodun Çözülmesi)

Ayrıca, çevrimiçi bir araç kullanarak obfuscated bir kodu geri çözebiliriz (**Deobfuscate**). Web sitesini ziyaret edin ve ardından obfuscated kodu sağlanan diyalog kutusuna yapıştırın. Web sitesi sizin için eşdeğer, insan tarafından okunabilir JS kodunu oluşturacak; böylece orijinal betiği anlamayı ve analiz etmeyi kolaylaştıracaktır.

Orijinal kodumuzu ne kadar kolay bir şekilde deobfuscate ettiğimizi ve geri aldığımızı gördünüz.

---

## 🚀 Siber Güvenlik ve CTF İpuçları: Obfuscation Analizi

### Neden Obfuscation Kullanılır?

Geliştiriciler fikri mülkiyeti korumak için kullansa da, saldırganlar **Malware** (kötü amaçlı yazılım) analizini zorlaştırmak için JS obfuscation yöntemlerine başvururlar.

|**Yöntem**|**Amaç**|**Güvenlik Perspektifi**|
|---|---|---|
|**Hex Encoding**|Karakterleri `\x48\x65` gibi formatlara sokar.|IDS/IPS imzalarını atlatmak için kullanılır.|
|**String Splitting**|Zararlı komutları parçalara böler (`"al" + "ert"`).|Statik kod analizini yanıltır.|
|**Dead Code Injection**|Çalışmayan binlerce satır kod ekler.|Analistin vaktini çalmak (Anti-analysis) için kullanılır.|

### 💡 CTF ve Analiz Taktikleri

1. **Beautifiers:** Kod sadece minified (sıkıştırılmış) ise, Chrome Developer Tools'daki `{ }` (Pretty Print) butonuna basarak kodu okunabilir hizaya getirebilirsiniz.
    
2. **Debugging:** Obfuscated kodun ne yaptığını anlamak için `alert` veya `console.log` fonksiyonlarının üzerine **breakpoint** koyarak değişkenlerin çalışma anındaki (runtime) gerçek değerlerini görebilirsiniz.
    
3. **Manual Deobfuscation:** `_0x11ed` gibi isimler gördüğünüzde, bunları "Refactor -> Rename" yaparak `ana_fonksiyon` gibi isimlerle değiştirmeniz analiz sürecinizi hızlandırır.
    

> **Unutmayın:** Hiçbir obfuscation yöntemi kodu tamamen gizleyemez. Tarayıcı kodu çalıştırabiliyorsa, siz de o kodu deobfuscate edebilirsiniz.

---