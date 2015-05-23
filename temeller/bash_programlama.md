### Bash Programlama

Bu bölümde Bash scripleme komutlarından birkaçının kullanımını göreceğiz. _Bash scriptler_ veya _shell scripleri_ çoklu terminal komandlarını içeren bir dosyalardır. Terminalde çalışan herhangi bir komut scrit dosyasında da çalıştırılabilmektedir.

#### ping
___

İlk scriptimizi `pingscrip.sh` olarak adlandıralım. Çalıştırdığımızda scriptimiz yerel ağımıza Internet Control Message Protocol (ICMP) yanıt verdiğne dair mesaj gönderecek. `ping [IP adress] veya [hostname]`

```ShellSession
root@kali:~/# ping 192.168.2.10
PING 192.168.2.10 (192.168.2.10) 56(84) bytes of data.
64 bytes from 192.168.2.10: icmp_req=1 ttl=64 time=0.090 ms
64 bytes from 192.168.2.10: icmp_req=2 ttl=64 time=0.029 ms
64 bytes from 192.168.2.10: icmp_req=3 ttl=64 time=0.038 ms
64 bytes from 192.168.2.10: icmp_req=4 ttl=64 time=0.050 ms
^C
--- 192.168.2.10 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2999 ms rtt min/avg/max/mdev = 0.029/0.051/0.090/0.024 ms
```
Elde edilen sonuçlar hedefimizdeki Windows XP sanal makinenin çalışmakta olduğunu ve ping problarına yanıt verdiğini görebiliyoruz.

### Basit bir Bash Scripti

İlk satır terminal `bash` yorumlaycısını kullanmasını söylüyor. Diğer `echo` ise kendinden sonra çift tırnak içinde yazdığmız metni ekrana yazar.

```ShellSession
#!/bin/bash
echo "Usage: ./pingscript.sh [network]" 
echo "example: ./pingscript.sh 192.168.2"
```

scriptimizi çalıştırabilme yetkisini verelim;

```ShellSession
root@kali:~/# chmod 744 pingscript.sh
```

scriptimizi çalıştırma esnasına dikkat edeceğimiz bir konu daha, çalıştıracağamız sciptin olduğu dizinin terminal $PATH değerinde olup olmaması

```ShellSession
root@kali:~/# echo $PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Dikkat edersek bizim scriptin olduğu `/root` dizini burda sıralanmamış. O yüzden komutu çalıştırmak için `./pingscript.sh` olarak yazmamız gerekiyor.

```ShellSession
root@kali:~/# ./pingscript.sh 
Usage: ./pingscript.sh [network] 
example: ./pingscript.sh 192.168.2
```

##### if ile koşul ekleme

Şimdi yukarda yazdığımız basit bir bash scriptine koşul eklemeyi öğrenelim. Scriptin yapacağı işlem, kullanıcının herhangi bir argument girip girmediğini kontrol etmek. Kullanıcın girdiği ilk argumente erişebilmek için `$1` kullanıyoruz, yani bash dilinde `if ['$1' == '']`, $1 argumenti boş ise `echo` ile ekrana yazdır diyoruz.

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]"
echo "example: ./pingscript.sh 192.168.2"
fi
```

Bu scriptimizi çalıştırdığımızda, gördüğünüz gibi herhangi bir parametre vermediğimiz için ekrana yazdırdı.

```ShellSession
root@kali:~/# ./pingscript.sh 
Usage: ./pingscript.sh [network] 
example: ./pingscript.sh 192.168.2
```

##### For döngüsü

Şimdi ise `then`'den sonra `else` ile devam ederek, herhangi bir parametre girdiğimizde yapacağı işlemi yazalım. Yapacağımız işlem yerel ağımızdaki 192.168.2.1 den 192.168.2.254 kadar tüm ağları kontrol etmek. Bunun için `for-loop` döngüsünü kullanıyoruz. 
* `for` döngüsü `done` ile bitirilmelidir
* `seq 1 254` anlamı 1den 254 kadar olan sayılarda
* `ping -c 1` pingin kullanım klavuzına bakarsak, `-c` parametresi girdiğimiz sayı kadar ping'i çalıştıracak. Burda `-c 1` girdiğimiz için sadece bir kere çalışacaktır.
* `$1.$x` = `[girdiğimiz_parametre.x_değeri]

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]" 
echo "example: ./pingscript.sh 192.168.2" 
else
for x in `seq 1 254`; do
ping -c 1 $1.$x
done
fi
```

`./pingscript.sh [yerel_ag]` olarak çalıştırıyoruz. Aşağıdaki sonuca bakarak söyleyebiliriz ki; __192.168.2.1__ ağından __ICMP__ yanıtı aldığım için bu ağ çalışmaktadır; diğer taraftan ise __192.168.2.2__ ağından __Destination Host Unreachable__ hatasını aldığım için bu ağ kullanılmaktadır.

```ShellSession
root@kali:~/# ./pingscript.sh 192.168.2
PING 192.168.2.1 (192.168.2.1) 56(84) bytes of data.
64 bytes from 192.168.2.1: icmp_req=1 ttl=255 time=8.31 ms

--- 192.168.2.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 8.317/8.317/8.317/0.000 ms
PING 192.168.2.2(192.168.2.2) 56(84) bytes of data.
64 bytes from 192.168.2.2: icmp_req=1 ttl=128 time=166 ms

--- 192.168.2.2 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms rtt min/avg/max/mdev = 166.869/166.869/166.869/0.000 ms
PING 192.168.2.3 (192.168.2.3) 56(84) bytes of data.
From 192.168.2.13 icmp_seq=1 Destination Host Unreachable

--- 192.168.2.3 ping statistics ---
1 packets transmitted, 0 received, +1 errors, 100% packet loss, time 0ms 
--snip--
```

Şimdi bu yazdığımız script çalışıyor, ama terminalden o kadar bilginin içinden hangisinin çalışıp çalışmadığnı kontrol etmek yerine sadece çalışmakta olanları listeleyerek daha güzel bir görünüm sağlayabiliriz. Bunun için, önceki konularda gördüğümüz `grep` komutu ile filtreleme yapacağız.

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]"
echo "example: ./pingscript.sh 192.168.2" else
for x in `seq 1 254`; do
ping -c 1 $1.$x | grep "64 bytes"
done
fi
```

Bu scripti çalıştırdıktan sonra göreceğiz ki, `grep` komutu ile sadece `64 bytes` olan kısımı almışız, yani sadece çalışmakta olanları.

```ShellSession
root@kali:~/# ./pingscript.sh 192.168.2
64 bytes from 192.168.2.1: icmp_req=1 ttl=255 time=4.86 ms 
64 bytes from 192.168.2.5: icmp_req=1 ttl=128 time=68.4 ms 
64 bytes from 192.168.2.8: icmp_req=1 ttl=64 time=43.1 ms
--snip--
```

Şimdi aldığımız son sonuçlarıda daha güzel bir görünüme getirmek için sadece IP adreslerini ekrana yazdıralım. `cut` komutu ile sadece dördüncü sütünda bulunan verileri yazdırabiliriz.
* `-d  --delimiter`   => sütünların bölüneceği karakter, `-d" "` her boşluğun olduğu yer birer sütün
* `-f --fields`      => kaçıncı sütünün alınacağı, `-f4` dördüncü sütün

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]"
echo "example: ./pingscript.sh 192.168.2"
else
for x in `seq 1 254`; do
ping -c 1 $1.$x | grep "64 bytes" | cut -d" " -f4
done
fi
```

Scriptimizi çalıştırdıktan sonra sadece IP adreslerimizin ekrana yazdırıldığını göreceğiz. Ama eğer dikkat ettiyseniz, her IPden sonra __:__ işareti var. Bu genel anlamda sorun olmaz, ama aldığımız sonuçlardan sonra bir işlem daha yapmak istersek, bunu düzetmemiz lazım olabilir.

```ShellSession
root@kali:~/mydirectory# ./pingscript.sh 192.168.2
192.168.2.1:
192.168.2.2:
192.168.2.8:
--snip--
```

`sed` komutu ile yerine getirebiliriz; işlem her satırın son karakterini kesecek.

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]"
echo "example: ./pingscript.sh 192.168.2"
else
for x in `seq 1 254`; do
ping -c 1 $1.$x | grep "64 bytes" | cut -d" " -f4 | sed 's/.$//' done
fi
```

Sonuç olarak ekranımıza aşağıdaki gibi güzel çıktılar alabiliriz. İstersek sadece ekrana yazdırmak yerine `>>` ile bir dosyaya da aktarabiliriz.

```ShellSession
root@kali:~/# ./pingscript.sh 192.168.2 
192.168.2.1
192.168.2.2
192.168.2.8
--snip--
```












