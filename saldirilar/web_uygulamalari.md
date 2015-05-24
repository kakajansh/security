### WEB UYGULAMALARI

Otomatik tarayıcıların bilinen güvenlik açıklarını bulmada iyi olabilir, ama genel olarak kendi özel web uygulamasını geliştirenler de var. Onlar için bazı ücretli programlar ile tarama yapılabilse bile, iyi bir penetrasyon tester için proxy denemelerinin yerini alamaz.

Her programda olduğu gibi, web programlarında da doğru sterilize edilmemiş girişler olabilir. Mesela bir sorgu, veritabanla iletişime geçerken kullanıcıdan adını veya şifresini istemektedir. Şimdi kullanıcı oraya isim değilde, veritabanında çalışan bir zararlı komut yazdığında, veriyi çalabilir veya kimlik doğrulamasını aşabilir.

Bu bölümde de bunun gibi dikkat etmemiz gerek genel güvenlik açıklarını Windows 7 sistemimize kurduğumuz, basit bir kitapçı uygulamamız üstünde denemeler yapacağız.

#### Burp Proxy kullanımı

Proxy kullanarak bizim tarayıcımız ile web uygulaması arasında geçen sorguları görebilir, kesin olarak hangi verilerin iletildiğine bakabiliriz. Kali Linux proxy özelliği olan web uygulamalarını denemeye yarayan Burp Suite programının bedava versiyonunu bulundurmaktadır.

Burp Suite başlatmak için __Applications > Kali Linux > Web Applications > Web Application Fuzzers > burpsuite__ 

Aşağıdaki gibi __Proxy__ üstüne basalım. Varsayılan olarak, __Intercept is on__ özelliği açık olacaktır; bu web tarayıcısndan giden istekleri yakalayarak bize onları sunucuya göndermeden önce görmemizi, hatda üstünde değişikler yapmamızı sağlayacaktır.

Şimdi Kali Linux'umuzda çalışan tarayıcıya web trafiğin Burp Suite üzerinden geçmesini söylememiz gerekiyor.

1. _Iceweasel_ tarayıcısını açalım, __Edit > Preferences > Advanced__ gelerek __Network__ seçelim.
2. Connection sağında olan __Settings__ tıklayalım.
3. Resimdeki gibi, __Manul proxy configuration__ seçerek IP adrese __127.0.0.1__ ve porta __8080__ girelim. Böylelikle Burp Proxy'nin varsayılan portuna yönlendirmiş olcağız.

Iceweasel'in trafiği Burp Suite üzerinden aktardığına emin olmak için, Windows 7 makinemizde çalışan _ http://192.168.2.12/bookservice _ adresini açalım.

Bağlantının tarayıcıda askıya alındığı görülecektir, ve resimde olduğu gibi hem tarayıcıda hem de Burp Suit'ta bookservice sitesinin ana sayfası için `HTTP GET` isteği gönderildiği görüntülenecektir.

Aldığımız `HTTP GET` sorgusu için daha detaylı bir bilgi edinebiliriz. Biraz sonra göreceğiz ki, bunları sunucuya göndermeden bazı değişiklikler de yapabiliceğiz. Ama şimdilik sadece __Forward__ basarak devam ettirelim. Tarayıcıya geri dönersek, server'in bizi bookservice sitesinin ana sayfayasına yönlendirdiğini göreceğiz.

Şimdi, bu siteye bir üye olalım. Yukarıda sağda __Login__ tıklayalım, sonra sorguyu proxy'dan server'a forward yapalım. Aynı şeyi Sign up sayfasına gidebilmek için __New User__ üstüne tıklayarak ta tekrarlayalım.

Kullanıcı adı, şifre, ve mail adresimizi girdikten sonra __Go__ basalım. Sorgumuz resimde gösterildiği gibi Bupr Proxy tarafından yakalanmış olması lazım.

Ek olarak, okumak için pek iyi olmayan _raw request (ham sorgu)_ yerine __Params__ basarak Burp Suit'in sorgumuzu daha okunabilir halini göstermesini sağlayabiliriz.

Mesela, yeni açtığımız ekranda kullanıcı alanı _cansu_, şifre alanı _password_, ve mail alanı cansu@hotmail.com gösterir.

Şimdi istersek burda şifreyi _password_ yerine _password123_ yaparak sorgumuzu sunucuya göndermeden değiştirebiliriz, ve sunucu _cansu_ için _password123_ şifresini atayacaktır, çünkü sunucun sorgunun orjinal halinden haberi olmamaktadır.

Proxy sunucuya gönderilen sorguları daha detaylı bir şekilde görmemizi sağlamaktadır. Bazen proxy trafiğini istemiğimiz de olacaktır, onun için __Intercept on__ basarak __Intercept off__ değiştirebiliriz. Sonradan gene bir sorgu yakalamak için lazım olursa geri açarız.

### SQL Injection

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























