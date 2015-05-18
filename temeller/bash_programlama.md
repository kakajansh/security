### Bash Programlama

Bu bölümde Bash scripleme komutlarından birkaçının kullanımını göreceğiz. _Bash scriptler_ veya _shell scripleri_ çoklu terminal komandlarını içeren bir dosyalardır. Terminalde çalışan herhangi bir komut scrit dosyasında da çalıştırılabilmektedir.

#### ping
___

İlk scriptimizi `pingscrip.sh` olarak adlandıralım. Çalıştırdığımızda scriptimiz yerel ağımıza Internet Control Message Protocol (ICMP) yanıt verdiğne dair mesaj gönderecek. `ping [IP adress] veya [hostname]`

```ShellSession
root@kali:~/# ping 192.168.20.10
PING 192.168.20.10 (192.168.20.10) 56(84) bytes of data.
64 bytes from 192.168.20.10: icmp_req=1 ttl=64 time=0.090 ms
64 bytes from 192.168.20.10: icmp_req=2 ttl=64 time=0.029 ms
64 bytes from 192.168.20.10: icmp_req=3 ttl=64 time=0.038 ms
64 bytes from 192.168.20.10: icmp_req=4 ttl=64 time=0.050 ms
^C
--- 192.168.20.10 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2999 ms rtt min/avg/max/mdev = 0.029/0.051/0.090/0.024 ms
```
Elde edilen sonuçlar hedefimizdeki Windows XP sanal makinenin çalışmakta olduğunu ve ping problarına yanıt verdiğini görebiliyoruz.

### Basit bir Bash Scripti

İlk satır terminal `bash` yorumlaycısını kullanmasını söylüyor. Diğer `echo` ise kendinden sonra çift tırnak içinde yazdığmız metni ekrana yazar.

```ShellSession
#!/bin/bash
echo "Usage: ./pingscript.sh [network]" 
echo "example: ./pingscript.sh 192.168.20"
```

scriptimizi çalıştırabilme yetkisini verelim;

```ShellSession
root@kali:~/# chmod 744 pingscript.sh
```

scriptimizi çalıştırma esnasına dikkat edeçeğimiz bir konu daha, çalıştıracağamız sciptin olduğu dizinin terminal $PATH değerinde olup olmaması

```ShellSession
root@kali:~/# echo $PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Dikkat edersek bizim scriptin olduğu `/root`dizini yok. O yüzden komutu çalıştırmak için `./pingscript.sh` olarak yazmamız gerekiyor.

```ShellSession
root@kali:~/# ./pingscript.sh 
Usage: ./pingscript.sh [network] 
example: ./pingscript.sh 192.168.20
```

##### if ile koşul ekleme
--

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]"
echo "example: ./pingscript.sh 192.168.20"
fi
```

##### For döngüsü
--

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]" 
echo "example: ./pingscript.sh 192.168.20" 
else
for x in `seq 1 254`; do
ping -c 1 $1.$x
done
fi
```

```ShellSession
root@kali:~/# ./pingscript.sh 192.168.20
PING 192.168.20.1 (192.168.20.1) 56(84) bytes of data.
64 bytes from 192.168.20.1: icmp_req=1 ttl=255 time=8.31 ms

--- 192.168.20.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 8.317/8.317/8.317/0.000 ms
PING 192.168.20.2(192.168.20.2) 56(84) bytes of data.
64 bytes from 192.168.20.2: icmp_req=1 ttl=128 time=166 ms

--- 192.168.20.2 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms rtt min/avg/max/mdev = 166.869/166.869/166.869/0.000 ms
PING 192.168.20.3 (192.168.20.3) 56(84) bytes of data.
From 192.168.20.13 icmp_seq=1 Destination Host Unreachable

--- 192.168.20.3 ping statistics ---
1 packets transmitted, 0 received, +1 errors, 100% packet loss, time 0ms 
--snip--
```

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]"
echo "example: ./pingscript.sh 192.168.20" else
for x in `seq 1 254`; do
ping -c 1 $1.$x | grep "64 bytes"
done
fi
```

```ShellSession
root@kali:~/# ./pingscript.sh 192.168.20
64 bytes from 192.168.20.1: icmp_req=1 ttl=255 time=4.86 ms 64 bytes from 192.168.20.2: icmp_req=1 ttl=128 time=68.4 ms 64 bytes from 192.168.20.8: icmp_req=1 ttl=64 time=43.1 ms
--snip--
```

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]"
echo "example: ./pingscript.sh 192.168.20"
else
for x in `seq 1 254`; do
ping -c 1 $1.$x | grep "64 bytes" | cut -d" " -f4
done
fi
```

```ShellSession
root@kali:~/mydirectory# ./pingscript.sh 192.168.20
192.168.20.1:
192.168.20.2:
192.168.20.8:
--snip--
```

```ShellSession
#!/bin/bash
if [ "$1" == "" ]
then
echo "Usage: ./pingscript.sh [network]"
echo "example: ./pingscript.sh 192.168.20"
else
for x in `seq 1 254`; do
ping -c 1 $1.$x | grep "64 bytes" | cut -d" " -f4 | sed 's/.$//' done
fi
```

```ShellSession
root@kali:~/# ./pingscript.sh 192.168.20 
192.168.20.1
192.168.20.2
192.168.20.8
--snip--
```

```ShellSession
```













