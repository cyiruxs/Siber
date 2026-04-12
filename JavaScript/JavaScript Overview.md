# İlk JavaScript Programımız: Tarayıcı Üzerinde Kod Çalıştırma

Bu bölümde, ilk programımızı oluşturmak için JS kullanacağız. JS, **interpreted** (yorumlanan) bir dildir; yani kod, önceden derleme (compilation) işlemine gerek kalmadan doğrudan tarayıcı tarafından yürütülür. Aşağıda değişken tanımlama, veri tiplerini anlama, kontrol akış yapıları ve basit fonksiyon yazımı gibi temel kavramları gösteren örnek bir JS kodu bulunmaktadır.

JavaScript

```
// Hello, World! programı
console.log("Hello, World!");

// Değişken ve Veri Tipi
let age = 25; // Number (Sayı) tipi

// Kontrol Akış Yapısı (Control Flow)
if (age >= 18) {
    console.log("Bir yetişkinsiniz.");
} else {
    console.log("Reşit değilsiniz.");
}

// Fonksiyon Tanımlama
function greet(name) {
    console.log("Merhaba, " + name + "!");
}

// Fonksiyonu Çağırma
greet("Bob");
```

JS öncelikle **client-side** (istemci tarafı) üzerinde yürütülür, bu da HTML ile doğrudan tarayıcı içinden etkileşime girmeyi ve denetlemeyi kolaylaştırır. İlk programımızı çalıştırmak için ek bir araca ihtiyaç duymadan **Google Chrome Console** özelliğini kullanacağız.

### Başlangıç Adımları:

1. Masaüstündeki simgeye tıklayarak **Google Chrome**'u açın.
    
2. Chrome açıldığında, **Ctrl + Shift + I** tuşlarına basarak veya sayfanın herhangi bir yerine sağ tıklayıp **İncele (Inspect)** seçeneğini seçerek konsolu açın.
    
3. Ardından **Console** sekmesine tıklayın. Bu panel, herhangi bir yazılım yüklemeden doğrudan tarayıcıda JS kodu çalıştırmanıza olanak tanır.
    

---

## Basit Bir Toplama Programı

İki sayıyı toplayan ve sonucu görüntüleyen basit bir program oluşturalım:

JavaScript

```
let x = 5;
let y = 10;
let result = x + y;
console.log("Sonuç: " + result);
```

Yukarıdaki kodda `x` ve `y` sayıları tutan değişkenlerdir. `x + y` iki sayıyı toplayan bir ifadedir (**expression**), `console.log` ise sonucu konsola yazdırmak için kullanılan bir fonksiyondur.

> [!SUCCESS]
> 
> Tebrikler! İlk JS programınızı başarıyla oluşturdunuz. Bu sadece başlangıç; bu odada JS'nin derinliklerine indikçe keşfedecek çok daha fazla şey var.

---

## 🛡️ Siber Güvenlik ve CTF Notları

### 1. Client-Side Manipülasyonu

JS istemci tarafında (sizin tarayıcınızda) çalıştığı için, bir web sitesinin mantığını konsol üzerinden değiştirebilirsiniz.

- **CTF İpucu:** Eğer bir web sayfasında bir buton pasifse (`disabled`), konsola gidip ilgili elementin özelliğini JS ile değiştirerek butonu aktif hale getirebilirsiniz.
    
- **Örnek:** `document.querySelector('button').disabled = false;`
    

### 2. Hassas Veri Analizi

Geliştiriciler bazen hata ayıklama (debugging) için konsola hassas bilgiler yazdırabilir ve bunları kaldırmayı unutabilirler.

- **Güvenlik İpucu:** Bir sızma testi sırasında her zaman `Console` ve `Network` sekmelerini kontrol edin. API anahtarları, kullanıcı rolleri veya gizli parametreler `console.log` ile buraya sızmış olabilir.
    

### 3. DOM Tabanlı XSS (Cross-Site Scripting)

Konsola yazdığınız her kod sadece sizin tarayıcınızda çalışır. Ancak, bir saldırgan kullanıcıyı kandırarak konsola zararlı bir kod yapıştırmasını sağlarsa (**Self-XSS**), kullanıcının oturum bilgilerini (cookies) çalabilir.

| **Kavram**      | **Açıklama**                                                                |
| --------------- | --------------------------------------------------------------------------- |
| **Interpreted** | Kodun satır satır okunup anında çalıştırılması.                             |
| **Client-Side** | Kodun sunucuda değil, kullanıcının bilgisayarında/tarayıcısında çalışması.  |
| **Console**     | Geliştiricilerin kod test etmek ve çıktıları görmek için kullandığı arayüz. |