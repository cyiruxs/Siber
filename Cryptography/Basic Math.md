### XOR İşlemi (Exclusive OR)

**XOR** ("özel VEYA"), ikili aritmetikte (binary) kullanılan mantıksal bir işlemdir. Temel kuralı basittir: İki bit birbirinden **farklıysa 1**, **aynıysa 0** sonucunu verir. Sembolü genellikle $\oplus$ veya `^` işaretidir.

**Doğruluk Tablosu:**

|**A**|**B**|**A ⊕ B**|
|---|---|---|
|0|0|**0**|
|0|1|**1**|
|1|0|**1**|
|1|1|**0**|

Kriptografideki Önemi:

XOR işleminin büyüleyici özellikleri vardır:

1. **Kendisiyle XOR:** $A \oplus A = 0$ (Bir değeri kendisiyle XOR'lamak sıfır verir).
    
2. **Sıfırla XOR:** $A \oplus 0 = A$ (Herhangi bir değeri 0 ile XOR'lamak değeri değiştirmez).
    
3. **Tersine Dönüştürülebilirlik:** Eğer bir $P$ (plaintext) mesajını $K$ (key) ile XOR'layıp $C$ (ciphertext) elde ederseniz ($P \oplus K = C$), aynı $K$ anahtarını tekrar kullanarak orijinal mesajı geri alabilirsiniz: $C \oplus K = P$.
    

Bu özellik, XOR'u temel simetrik şifreleme algoritmalarının kalbi yapar.

---

### Modulo İşlemi (Kalanlı Bölme)

Kriptografide sıkça karşılaştığımız bir diğer işlem ise **Modulo** operatörüdür (`%` veya `mod`). $X \pmod Y$ işlemi, $X$ sayısının $Y$ sayısına bölünmesinden elde edilen **kalanı** verir.

Günlük hayatta bölme işleminin sonucuna odaklansak da, kriptografi dünyasında "kalan" çok daha kritiktir.

**Örnekler:**

- $25 \pmod 5 = 0$ (Çünkü 25, 5'e tam bölünür).
    
- $23 \pmod 6 = 5$ (Çünkü $23 = (3 \times 6) + 5$).
    
- $23 \pmod 7 = 2$ (Çünkü $23 = (3 \times 7) + 2$).
    

**Önemli Özellikler:**

- **Aralık:** $a \pmod n$ işleminin sonucu her zaman $0$ ile $n-1$ arasındadır.
    
- **Geri Döndürülemezlik (Tek Yönlülük):** Modulo işlemi tek başına geri döndürülemez. Örneğin $x \pmod 5 = 4$ denklemini sağlayan sonsuz sayıda $x$ değeri vardır ($9, 14, 19...$). Bu "tek yönlü" özellik, bazı asimetrik şifreleme algoritmalarının (RSA gibi) temelini oluşturur.
    

> [!TIP] Büyük Sayılarla Hesaplama
> 
> Kriptografi egzersizlerinde çok büyük sayılarla çalışmanız gerekebilir. Standart hesap makineleri yetersiz kalırsa Python programlama dilini (büyük sayıları otomatik yönetir) veya WolframAlpha gibi çevrimiçi araçları kullanabilirsiniz.