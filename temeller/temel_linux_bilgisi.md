### Temel Linux Bilgisi

* Terminal Nedir?
* Linux Komutları
* Kullanıcı Yönetimi
* Dosya Sistemi
* Metin Editörleri
* Veri İşleme Komutları
* Paket Yönetimi
* Servisler
* Network Ayarları

#### Terminal
___

* Terminal Gnome masaüstü aracının komut satırı aracıdır.
* Linux'un en güçlü olduğu taraf terminal (shell) sistemidir.
* Kali grafik arayüzüne sahip olsa da, komut satırında grafik ara biriminde yapılanlardan daha çok eylem gerçekleştirebilir
* Kali'de terminali komut satırından açmak için `ctrl + alt + T` kombinasyonu kullanılır.

#### Linux Komutları
___

* Linux'te birçok komut parametre almaktadır. Parametreler komut adı yazıldıktan sonra bir boşluk bırakılarak yazılmalıdır. Genellikle parametreler '-' işareti ile başlamaktadır.
* Linux komutlarına parametreler ile özel işler yaptırabilir.
* Temel kural: `Komut + alacağı parametreler`
* Komut hakkında bilinmek istenen her şey için `man + komut` yeterlidir.

##### Terminale ilk bakış

```ShellSession
root@kali:~#
```

##### Dosya, dizin listeleme `ls`

* `ls` listeleme komutudur. Dosya, dizin listelemek ve özelliklerini görüntülemek için kullanılır.
* `a` parametresi gizli dosyaları gösterir.
* `l` parametresi detaylı listeleme seçeneği sağlar.
* `h` parametresi anlaşılabilir dosya boyutu sağlar.
* Ayrıntılı bilgi için: `man ls`

```ShellSession
root@kali:~# ls
Desktop
```

##### Bulunduğumuz dizin `pwd`

`pwd` komutu, print working directory, bulunduğumuz dizini ekrana yazan komuttur.

```ShellSession
root@kali:~# pwd
/root
```

##### Klasörleri arası geçiş `cd`

* `cd` komutu -change directory- ile dizin veya klasörler arası geçiş yapılabilmektedir.
* `cd..` komutu ile bir üst dizine/klasöre geçiş yapılır.

```ShellSession
root@kali:~/Desktop# cd ..
root@kali:~/# cd ../etc
root@kali:/etc#
```

##### Komutlar hakkında bilgi `man`

Manuel ifadesinin kısaltmasıdır, linux sistemlerinde bir komut veya yazılım hakkında bilgi almayı sağlar.

```ShellSession
root@kali:~# man ls
LS(1)       User Commands       LS(1)

NAME
    ls - list directory contents

SYNOPSIS
    ls [OPTION]... [FILE]...

DESCRIPTION
    List information about the FILEs (the current directory by default). Sort entries alphabetically if none of -cftuvSUX nor --sort is speci- fied

    Mandatory  arguments  to  long  options are mandatory for short options too.

    -a, --all
        do not ignore entries starting with .

    -A, --almost-all
        do not list implied . and ..
--snip--
    -l  use a long listing format
--snip--
```

#### Kullanıcı yönetimi
___

* Linux işletim sistemlerinde ayarlanabilirlik ve birden çok kullanıcının aynı anda login olabilmesi mümkündür.
* Windows'taki çoklu kullanıcı hesabı ile benzer değildir.
* Birden çok kullanıcının sisteme login olabilmesi için çok kullanıcılı bir platform sağlanmış olur.
* Linux işletim sisteminde kullanıcı bilgileri `/etc/passwd`dosyasında tutulur.
* Gruplar hakkındaki bilgiler `/etc/group` dosyası içerisinde bulunur.
* Kullanıcı şifrelerinin hasleri `/etc/shadow` dosyasının içerisinde bulunur.
* `/etc/passwd` tüm kullanıcılar görebilir.
* `/etc/shadow` dosyasını sadece root görebilir.

##### /etc/passwd
___

* `/etc/passwd` dosyası kullanıcı bilgilerini saklar.
* Bir ASCII dosyası, her bir kullanıcı için bir girdi kullanarak saklanır. Taslak olarak şöyledir:
    `-isim:şifre:kid:gid:yorum:evdizini:kabuk`
    * `-isim`     : Login ismi
    * `-şifre`    : Encrypt hali ile şifre
    * `-kid`      : Kullanıcı ID
    * `-gid`      : İlk grup ID'si
    * `-yorum`    : Yorum, genellikle gerçek isim yazılır.
    * `-evdizini` : Kullanıcının /home dizinini gösterir.
    * `-kabuk`    : Öntanımlı olan shell'i.

##### /etc/group
___

* `/etc/group`'un içindeki dosyada grupların özellikleri tutulur. Taslak:
    `grup_ismi:grup_şifresi:grup_id:üye`

##### /etc/shadow
___

* Bu dosya şifreleri ve şifrelerle ilgili zaman bazlı bilgileri de tutan, ASCII formatında dosyalanmış bilgileri içerir.
* Yalnızca root tarafından görüntülenebilir.
* Yapısı:
    `isim:şifre:sondeğişim:min:max:warn:inactive:expire:flag`
    * `-isim`       : Kullanıcı adı
    * `-şifre`      : Encrypt edilmiş şifre * yada ! varsa hesap bloklanmıştır
    * `-sondeğişim` : Şifrenin değiştiği günden itibaren kaç gün geçmiş
    * `-min`        : Şifrenin değişmiş olabileceği günden önce kaç gün geçmiş
    * `-max`        : Şifrenin kesin olarak değişmiş olduğu günden sonra kaç gün geçmiş
    * `-warn`       : Şifrenin geçerliliğini dolmadan kaç gün önce uyarı verileceğini bildirir
    * `-inactive`   : Hesap bloklanmış duruma geçtikten sonra kaç gün geçmiş
    * `-expire`     : Hesabın bloklanmış olduğu gün sayısı
    * `-flag`       : Reserve edilmiş alan. (kullanılmıyor)

##### Sisteme Kullanıcı Ekleme

* `useradd` komutu, yeni bir kullanıcı oluşturma ya da var olan bir kullanıcı bilgilerini güncelleme amacıyla kullanılabilir.
* `useradd [kullanıcı_adı]`
* __-g__ parametresi ile eklenecek kullanıcının grubu da belirlenebilir.
* `useradd -g [grup_ismi][kullanıcı_ismi]`
* Kullanıcılara parola vermek için `passwd` komutu kullanılır.
* `passwd [kullanıcı_adı]`
* Normal kullanıcılar eski şifreyi bilmeden bunu yapamazlar. Root kullanıcı yapabilir.

```ShellSession
root@kali:~# adduser cansu
Adding user `cansu' ...
Adding new group `cansu' (1000) ...
Adding new user `cansu' (1000) with group `cansu' ...
Creating home directory `/home/cansu' ...
Copying files from `/etc/skel' ...
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for cansu
Enter the new value, or press ENTER for the default
    Full Name []: Cansu Poyraz
    Work Phone []:
    Home Phone []:
    Other []:
Is the information correct? [Y/n] Y
```

##### Sistemden Kullanıcı Silme

* `userdel` ve `deluser` komutları kullanılabilir.
* `userdel [kullanici_adi]
* __-r__ parametresi ile kullanıcıya ait dizinler de silinebilir.

```ShellSession
root@kali:~# userdel cansu
```

##### Kullanıcı Değiştirme ve Sudo Kullanımı

* Kullanıcı değiştirmek için `su`
* Kullanıcıya root yetkisini vermek için `sudo`

```ShellSession
root@kali:~# su cansu
cansu@kali:/root$ adduser john
bash: adduser: command not found
eorgia@kali:/root$ sudo adduser john
[sudo] password for cansu:
Adding user `john' ...
Adding new group `john' (1002) ...
Adding new user `john' (1002) with group `john' ...
--snip--
cansu@kali:/root$ su
Password:
root@kali:~#
```

#### Dosya Sistemi
___

* Dosya ve dizinler üzerinde çeşitli işlemler yapılabilir.
    * Oluşturulabilir
    * Silinebilir
    * Değiştirilebilir
    * Listelenebilir, çalıştırılabilir
    * Taşıma ve kopyalama yapılabilir
* Dosya ve dizinler için tanımlanmış haklar mevcuttur. Bu haklar ve izinler değiştirilebilir.
    * Sahibi, grubu ve herkes
    * Örneği herkese okuma hakkı ver
* Her dosyanın;
    * Bir sahibi vardır
    * Bir grubu vardır
    * Sahibi, grubu ve herkes olmak üzere üç çeşit erişim izni vardır
    * Bir dosya oluşturulurken varsayılan izinleri umask ile belirlenir.
* Her kullanıcının;
    * UID (login ismi), gid (login grubu) ve diğer gruplara üyeliği vardır
    * UID kimliğinizi gösterir (Kullanıcı ve ID numarası)
    * GID (Grup adı ve numarası)
* Linux için üç çeşit dosya izin kavramı vardır.
    * __READ (r) :__ Dosya veya dizinlerin okunabilmesi için gerekli olan izindir. Dizinlerde listeleme özelliği olarak kullanılır.
    * __WRITE (w) :__ Yeni bir dosya veya dizin oluşturmak, değiştirmek için gerekli olan izindir.
    * __EXECUTE (x) : __ Dosya çalıştırılması ya da dizine giriş hakkı için kullanılan izindir.

|  Sayı değeri |     İzni           |    Binary    |       |
|:------------:|:-------------------|:------------:|:-----:|
|      7       | hepsi              |     111      | ---   |
|      6       | okuma, yazma       |     110      | --x   |
|      5       | okuma, çalıştırma  |     101      | -w-   |
|      4       | sadece okuma       |     100      | -wx   |
|      3       | yazma, çalıştırma  |     011      | r--   |
|      2       | sadece yazma       |     010      | r-x   |
|      1       | sadece çalıştırma  |     001      | rw-   |
|      0       | hiçbiri            |     000      | rwx   |

##### Örnek
```ShellSession
root@kali:~/mydirectory# ls -l myfile
-rw-r--r-- 1 root root 47 Apr 23 21:15 myfile
```

Soldan sağa doğru dosyanın izni (-rw-r--r--), dosyanın sahibi ve sahip olduğu grup (root), dosyanın boyutu (47 byte), dosyanın son değiştirme tarihi (April 23, 21:15) ve sonunda dosyanın ismi (myfile)

```ShellSession
root@kali:~/mydirectory# chmod 700 myfile
root@kali:~/mydirectory# ls -l myfile
-rwx------u1 root root 47 Apr 23 21:15 myfile
```
Şimdi bu komutu çalıştırdıktan sonra, bu dosyaya sadece root erişebilir. Diğer kullanıcılar `access denied` hatasini alirlar.

##### Yeni Bir Klasör veya Dosya Oluşturma

* Yeni boş bir dosya oluşturmak için

```ShellSession
root@kali:# touch dosya_adı
```

* Yeni boş bir klasör oluşturmak için

```ShellSession
root@kali:~# mkdir mydirectory
root@kali:~# ls
Desktop     mydirectory     myfile
root@kali:~# cd mydirectory/
```

##### Kopyalama, Taşıma, Silme

1. Kopyalama `cp`
    __-r__ parametresi ile dizin içerisindeki herşeyi taşır.
    __-p__ parametresi ile taşıma esnasında dosya haklarını korur.
2. Taşıma `mv`
    __-f__ parametresi ile kaynak dosya hedef dosyaya kopyalanır ve herhangi birşey sorulmaz
3. Silme `rm`
    __-r__ parametresi ile rekürsif bir şekilde, verilen dosyanın içindeki tüm dosyalar silinebilir.

```ShellSession
1-root@kali:/mydirectory# cp /root/myfile myfile2
2-root@kali:/mydirectory# mv /root/myfile myfile2
3-root@kali:/mydirectory# rm myfile2
```

#### Metin Editörleri
___

* Linux'ta hemen hemen tüm işlemler dosya üzerinde gerçekleşmektedir.
* Mevcut birçok linux sunuculu sistem kullanıcı arayüzüne sahip değildir. Bu sunucuları yönetmek veya zaman, performans açısından iyi sonuçlar elde edebilmek için metin editörü kullanmak elzemdir.
* Linux'ta en çok kullanılan editörler __nano__ ve __vi__'dir.
* _Nano_, kullanıcı dostudur ve linux ile hazır gelir.
* _Vi_, kullanımı daha zor olan, buna karşın harika yetenekleri bulunan bir metin editörüdür.

##### Nano Editörü

* Gelişmiş metin editörüdür. Kullanıcı dostu bir arayüze sahiptir.
* Kullanımı: `nano [dosya_adi]`
* Aşağıdaki özellikler ile kullanılmaktadır.
    * `Ctrl + X` = Çıkış
    * `Ctrl + K` = Satırı kes
    * `Ctrl + U` = Satırı yapıştır
    * `Ctrl + W` = Arama yapar
    * `Ctrl + K` = Belirtilen texti kes
    * `Ctrl + Z` = Geri al
    * `Ctrl + G` = Yardım ekranını açar

##### Vi Editörü

* Gelişmiş bir metin editörüdür ve kullanımı biraz zordur.
* Vi ilk başta karmaşık görünse de hızı ve verimi ile her kullanıcın işini büyük ölçüde kolaylaştıran bir editördür.
* Çok kullanılan komutları öğrendikten sonra vi'nin gücü ortaya çıkacaktır.
* Linux dağıtımlarıyla birlikte gelmektedir.
* Kullanımı: `vi [dosya_adi]`, dosya mevcut ise onu açar değilse oluşturup öyle açar.

--

Vi editörü iki moda sahiptir:
    1. __Insert Modu:__ Düzenleme yapılan dosya içinde metin işlemlerinin yapıldığı mod.
    2. __Komut Satırı Modu:__ Açılan metin üzerinde arama, değiştirme, kaydetme, kapatma gibi eylemlerin gerçekleştirildiği mod.

--

Vi editörünü kullanırken en çok kullanılan komutlar şunlardır
* `a`           imlecin olduğu yerden itibaren edit moduna geçer.
* `i`           insert moda geçiş yapar.
* `ESC`         insert modu kapatır.
* `u`           geri al.
* `U`           tümünü geri al.
* `dd`          imlecin olduğu satırı sil.
* `x`           imlecin gerisindeki karakteri sil.
* `/kelime`     'kelime' için arama yapar.
* `:w`          metni kaydet.
* `:q`          Belgeyi kapat.
* `:10`         imleci 10. satıra getirir.
* `H`           imleci sayfanın en başına getirme.
* `L`           imleci sayfanın en sonuna götürme
* `o`           imlecin altına yeni bir satır açar. ESC ile çıkılır.
* `O`           imlecin üstüne yeni bir satır açar. ESC ile çıkılır.
* `:q!`         kaydetmeden çık.
* `d`           bulunan ve önceki satırı siler.
* `h`           imlecin soluna doğru devam et.
* `l`           imlecin sağına doğru devam et.
* `?`           imleçten dosyanın başına doğru arama yapar.

##### Vi'de dosya düzenleme

```ShellSession
root@kali:~/mydirectory# vi testfile.txt
we
are
teaching
pentesting
today
~
"testfile.txt"  7L, 46C           1,1
All
```
Nano'da olduğu gibi Vi'de hemen açıldıktan sonra düzenlemeye başlanamıyor. Bir dosyayı düzenlemek için, __I__ basarak ekleme moduna girilmelidir. Ekleme moduna girildiğinde terminalin alt kısmında INSERT görüntülenir. Değişiklikleri tamamladıktan sonra ESC tuşuna basarak komut moduna geri dönüş yapılır. Vi'den çıkmak için de __wq__ yazılır.

--

#### Veri İşleme Komutları

##### cat
___

* `cat` komutu dosya içeriğini okumak ve görüntülemek için kullanılır.
* İçeriğin tamamını görüntüler

```ShellSession
root@kali:~/mydirectory# cat dosyam
1 Pazartesi
2 Kasım
3 Kali
```

##### echo
___

* `echo` komutu kendinden sonra yazılan ifadeyi ekrana yazdırır..
* Ayrıca ortam değişkenlerini de başına $ koyarak `echo` ile yazdırabiliriz.
* `echo yazi > dosyam` dosya içine yazmayı sağlar.

```ShellSession
root@kali:/mydirectory# echo merhaba dunya
merhaba dunya

root@kali:/mydirectory# echo merhaba dunya > dosyam
root@kali:/mydirectory# cat dosyam
merhaba dunya
```

##### grep
___

`grep` komutu, kelime arama komutudur. Verilen data içerisinden istenilen kelimeye uygun satırı getirir.
    * __-i__ büyük küçük harf duyarsızlığı parametresidir.
    * __-r__ ile düzenli ifadeler (regex) kullanılabilir.

```ShellSession
root@kali:~/mydirectory# grep September myfile
1 Derbycon September
3 Brucon September
```

##### sed
___

`sed` bir manipulasyon komutudur. Sadece bu komutu özelliklerini anlatmak için bir kitap yazılabilir, biz sadece basit bir örnekle bahsedip geçelim. `sed` için (/) slaş bir sınırlayıcı bir karakterdir. _myfile_ dosyasında tüm _Blackhat_ sözcüklerini _Defcon_'a çevirmek için.

```ShellSession
root@kali:~/mydirectory# sed 's/Blackhat/Defcon/' myfile
1 Derbycon September
2 Shmoocon January
3 Brucon September
4 Defcon July
5 Bsides *
6 HackerHalted October
7 Hackcon April
```

##### awk
___

Desen eşleştirme komutudur. Örneğin 6 veya daha fazla numaralı konferansları bulmak için:

```ShellSession
root@kali:~/mydirectory# awk '$1 >5' myfile
6 HackerHalted October
7 Hackcon April
```

veya her satırda ilk ve üçüncü kelimeleri bulmak için:

```ShellSession
root@kali:~/mydirectory# awk '{print $1,$3;}' myfile
1 September
2 January
3 September
4 July
5 *
6 October
7 April
```

#### Paket Yönetimi
___

* Kali paket yönetimi komut satırından `apt-get` komutu ile çalıştırılabilir.
* Kali’deki kaynak listesini `/etc/apt/sources.list` içinde bulabilirsiniz.
* Aşağıdaki komutlar ile kali paket yönetimini güncel tutabilirsiniz.
    `# apt-get update & apt-get -y upgrade`
* Kali paket yöneticisinden program yüklemek ve silmek, aratmak oldukça basittir.
    * `apt-get install [paket_adı]`
    * `apt-get remove [paket_adı]`
    * `apt-cache search [paket_adı]`
* Synaptic ile tüm süreçler arayüz ile yönetilebilir.
    `apt-get install synaptic -y


#### Servisler
___

* Kali güvenlik dağıtımı olmasına rağmen üzerinde linux dağıtımlarında bulunan bazı servisleri barındırmaktadır.
* Bu tür servislerin amacı güvenlik testlerinde yardımcı öğeler olarak kullanılabilmesidir.
* Örneğin; Bir sisteme sızma denemesi gerçekleştirildi ve başarıldı, sızılan sistemden tftp ile veri alınması gerekiyor. Bu durumda Kali üzerinde tftp servisi çalıştırılarak gerekli bilgiler sunucudan kolaylıkla transfer edilebilir.

##### Apache servisini başlatma;

Başlatma: `service apache2 start`
Yeniden başlatma: `service apache2 restart`
Durduma: `service apache2 stop`

```ShellSession
root@kali:~/mydirectory# service apache2 start
[....] Starting web server: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.1.1 for ServerName
. ok
```

#### Network Ayarları
___

`ifconfig` komutu ile ağ arayüzlerine IP adresi atanabilir. `ifconfig` komutundan sonra hangi ağ kartının ismi yazılır ise yalnızca o ağ kartının özellikleri görüntülenir.

```ShellSession
root@kali:~# ifconfig
eth0 Link encap:Ethernet HWaddr 00:0c:29:df:7e:4d
    inet addr:192.168.20.9 Bcast:192.168.20.255 Mask:255.255.255.0
    inet6 addr: fe80::20c:29ff:fedf:7e4d/64 Scope:Link
    UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
    RX packets:1756332 errors:930193 dropped:17 overruns:0 frame:0
    TX packets:1115419 errors:0 dropped:0 overruns:0 carrier:0
    collisions:0 txqueuelen:1000
    RX bytes:1048617759 (1000.0 MiB)  TX bytes:115091335 (109.7 MiB)
    Interrupt:19 Base address:0x2024
--snip--
```

Bu sonuçta şimdilik bizi ilgilendiren kısım sadece IP adresimizin `192.168.20.9` olduğudur. Birde _default gateway_ öğrenmemiz lazım. O da `route` komutu ile

```ShellSession
root@kali:~# route
Kernel IP routing table
Destination   Gateway       Genmask         Flags Metric Ref Use Iface
default       192.168.20.1  0.0.0.0         UG    0      0   0   eth0
192.168.20.0  *             255.255.255.0   U     0      0   0   eth0
```

##### Statik IP Belirleme

Normalde network bağlantımız IP adres çekebilmek için varsayılan olarak dinamik yapılandırma protokolünü (DHCP) kullanacaktır. IP adresimizin değişmemesi için `/etc/network/interfaces` dosyasını istediğimiz metin editöründe açarak

Varsayılan `/etc/network/interfaces` dosyası

```ShellSession
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
# The loopback network interface
auto lo
iface lo inet loopback
```

Değiştirelim:

```ShellSession
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
# The loopback network interface auto lo
iface lo inet loopback
auto eth0
iface eth0 inet static
address 192.168.20.9
netmask 255.255.255.0
gateway 192.168.20.1
```

##### Network Bağlantılarını Görüntüleme

```ShellSession
root@kali:~/mydirectory# netstat -antp
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address Foreign Address PID/Program name
tcp6 0 0 :::80 :::* 15090/apache2
State LISTEN
```

##### DAHA FAZLASI İÇİN:
* [BGA Kali linux](http://www.slideshare.net/bgasecurity/kali-linux)
* [Kali ile Linux'e Giriş | IntelRAD](http://www.slideshare.net/mmetince/kali-ile-linuxe-giri-intelrad)