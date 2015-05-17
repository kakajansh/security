### Temel Linux Bilgisi

* Terminal Nedir? Nasıl açılır?
* Linux Komutları serisi - 1
* Hostname ve Network Ayarları
* Servisler
* Linuxta Kullanıcı Yönetimi
* Linux Dosya Sistemi
* Linux Komutları Serisi - 2
* Metin Editörleri
* Process
* Paket Yönetim Sistemi
* Sistem İzleme

#### Terminal 

* Terminal Gnome masaüstü aracının komut satırı aracıdır.
* Linux'un en güçlü olduğu taraf terminal (shell) sistemidir.
* Kali grafik arayüzüne sahip olsa da, komut satırında grafik ara biriminde yapılanlardan daha çok eylem gerçekleştirebilir
* Kali'de terminali komut satırından açmak için `ctrl + alt + T` kombinasyonu kullanılır.

#### Linux Komutları Serisi - 1

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

##### Kullanıcı yönetimi
* Linux işletim sistemlerinde ayarlanabilirlik ve birden çok kullanıcının aynı anda login olabilmesi mümkündür.
* Windows'taki çoklu kullanıcı hesabı ile benzer değildir.
* Birden çok kullanıcının sisteme login olabilmesi için çok kullanıcılı bir platform sağlanmış olur.
* Linux işletim sisteminde kullanıcı bilgileri `/etc/passwd`dosyasında tutulur.
* Gruplar hakkındaki bilgiler `/etc/group` dosyası içerisinde bulunur.
* Kullanıcı şifrelerinin hasleri `/etc/shadow` dosyasının içerisinde bulunur.
* `/etc/passwd` tüm kullanıcılar görebilir.
* `/etc/shadow` dosyasını sadece root görebilir.

##### /etc/passwd

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

* `/etc/group`'un içindeki dosyada grupların özellikleri tutulur. Taslak:  
    `grup_ismi:grup_şifresi:grup_id:üye`

##### /etc/shadow

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

##### Sisteme Kullanıcı Silme

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

#### Dosya Dizin İşlemleri

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
2. Taşıma `mv`
3. Silme `rm`

```ShellSession
1-root@kali:/mydirectory# cp /root/myfile myfile2
2-root@kali:/mydirectory# mv /root/myfile myfile2
3-root@kali:/mydirectory# rm myfile2
```






##### cat

* `cat` komutu dosya içeriğini okumak ve görüntülemek için kullanılır.
* İçeriğin tamamını görüntüler

```ShellSession
root@kali:~/mydirectory# cat dosyam 
1 Pazartesi
2 Kasım
3 Kali
```

##### echo

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

#####
```ShellSession
```

#####
```ShellSession
```

#####
```ShellSession
```

#####
```ShellSession
```










