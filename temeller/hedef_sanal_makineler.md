### Hedef Sanal Makineler

* Ubuntu
* Windows XP SP3
* Winwows 7 SP1

Yapacağımız saldırı denemelerinde kullanmak amaçlı kendimize __Ubuntu__, __Windows XP__ ve __Windows 7__ olmak üzere 3 sanal makine daha kurmamız lazım. İnternette bu sistemlerin sanallaştırılmış versiyonları mevcuttur.

İlk önce VMware dosyalarımızı indirelim:

* __Ubuntu:__ http://www.mininova.org/tor/13274076 (torrent)

* __Windows:__ http://dev.modern.ie/tools/vms/#downloads

    * Windows XP
        Virtual Machine: __IE on XP__
        Select Platform: __VMware__

    * Windows 7
        Virtual Machine: __IE10 on Win7__
        Select Platform: __VMware__

![k1]

Dosya indirme işlemi tamamlandıktan sonra, artık bir tıklama ile hem Windows hem Ubuntu sistemlerini çalıştırabiliriz. İsterseniz internetten iso dosyalarını indirerek, sıfır kurulum da yapılabilir, seçenek sizin.. Biz kolaya kaçıyoruz.. VMware çalıştırdığınızda son olarak karşınıza çıkacak ekran çıktısı aşağıde verilmiştir. Şimdi ise tek tük ayarlar kaldı onlarla devam edelim.

![k2]

#### Ubuntu

![ubuntu]

Ubuntu sanal makinemizi çalıştırmak için, verdiğim linkten indirmeniz yeterlidir. Herhangi bir ayar yapmaya gerek yoktur. İndireceğiniz dosya 7zip dosyasıdır, aşağıda vereceğim linkleri kullanarak açabilirsiniz. Şifresi: _1stPentestBook?!_ İlk çalıştırdığınızda VMware sizden birşeyler isteyecektir, orda __I copied it__ diyerek geçebilirsiniz. Sisteme giriş yapmak için kullanıcı adı: _georgia_, şifre: password. Hiçbir güncelleme yapmayın.

* Win: http://www.7-zip.org/download.html
* Mac: http://ez7z.en.softonic.com/mac

#### Windows XP

![winxp]

##### Windows Güvenlik Duvarını Kapatma

Başlat menüsünden __Control Panel__ açalım, ordan __Security Center > Windows Firewall__ gelerek güvenlik duvarını resimde olduğu gibi kapatalım.

![k3]

##### Kullanıcı Parolası

__Control Panel__ kapatmadan, gene ordan __User Accounts__ açalım. Mevcut kullanıcıya __Create a password__ diyerek yeni parola atayalım. Ve ismi: _security_ şifresi de: _security_ olan bir kullanıcı daha ekleyelim.

![k4]

##### Statik IP Adres Ayarı

Denemelerimizin devamında IP adreslerimizin her defasında değişmemesi için statik bir IP adres verelim. Bu yapmadan, sistemimizin _Bridge Network Mode_ kullandığına VMware ayarlarından emin olmamız lazım, sonrasında ise otomatik verilen IP öğreneceğiz. __Start > Run__ dan __cmd__ yi açalım, ve karşımıza çıkan ekranda `ipconfig` yazalım. Bu bize şu anda kullanmakta olduğumuzun network ayarlarını gösterecektir.

![k5]

Bu bilgilere ulaştıktan sonra,
    1. __Control Panel > Network and Internet Connections > Network Connections__ gidelim
    2. Ordan __Local Area Connection__ sağ tıklayıp __Properties__ açalım. 3. __Internet Protocal (TCP/IP)__ seçerek __Properties__ basalım. yukarda aldığımız sonuçları aşağıdaki şekilde girelim.

![k6]

İşlem başarılı tamamlandımı, onu kontrol etmek için __Kali__'mizi açalım, terminalde `ping [windows_ip_aresi]` komutunu çalıştıralım.

```ShellSession
root@kali:~# ping 192.168.2.240
PING 192.168.20.10 (192.168.20.10) 56(84) bytes of data.
64 bytes from 192.168.20.10: icmp_req=1 ttl=128 time=3.06 ms
^C
```

`ping` sonsuza kadar çalışır, o yüzden __Ctrl+C__ yaparak işlemi kesebiliriz.

Benim girdiğim IP _192.168.2.240_, siz ona göre kendi bilgisayarınızda aldığınız sonuçlara bakarak değişiklik yaparsınız. `ping` komutu çalıştırdıktan sonra `64 bytes from 192.168.20.10: icmp_req=1 ttl=128 time=3.06 ms` bu satırı görüyorsak, demekki ayarlarımız doğru yapmışız ve Kali ile Windows sanal makinelerimiz aynı network altında çalışmakta. Zaten normal bilgisayarınızda bile aşağıdakiye benzer bir ekranla karşılaşabilirsiniz. Yani burdaki _samsung_ normal bilgisayar, _ie8winxp_ ise sanal makine.

![k7]

##### XP'mizi Windows Domain'in bir Üyesi gibi yapma

Son olarakta, kurduğumuz Windows XP sistemini normal bir windows domain'in üyesiymiş gibi yapmayı ögreneceğiz.

1. __Start > Run__ seçerek `secpol.msc` komutu ile Local Security Setting Panel'ini açalım.
2. Soldaki __Local Policies__ seçeneğini genişleterek, sağda __Security Options__ üstüne çift tıklayalım.
3. Sağdaki Policy listesinden __Network access: Sharing and security model for local accounts__ çift tıklayıp, __Classic-local users authenticate as themselves__ seçelim.

![k8]

TODO: Installing Vulnerable Software

#### Windows 7

TODO: windows7

Tebrik ederim! Hedef sanal makinelerimizin kurulumunu tamamlamış bulunmaktayız. Yorucu bir gündü.. Birazda kafa dağıtmaya ne dersiniz? Ubuntu açalım, ordan __Games > Nibbles__ oyununu açalım.. öyle devam ederiz..

![nibbles]

[k1]: ../resim/hedef/k1.png
[k2]: ../resim/hedef/k2.png
[k3]: ../resim/hedef/k3.png
[k4]: ../resim/hedef/k4.png
[k5]: ../resim/hedef/k5.png
[k6]: ../resim/hedef/k6.png
[k7]: ../resim/hedef/k7.png
[k8]: ../resim/hedef/k8.png
[ubuntu]: ../resim/hedef/ubuntu.png
[winxp]: ../resim/hedef/winxp.png
[nibbles]: ../resim/hedef/nibbles.png


















