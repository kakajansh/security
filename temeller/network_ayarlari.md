### Network Ayarları

_VMware Player/VirtualBox_ kurulduktan sonra bilgisayarınızda 2 adet sanal ağ kartı oluşacaktır. Bu ağ kartları ile kullandığınız sanal makineler IP alırlar ve fiziksel işletim sistemi üzerinde internete çıkarlar  

* __NAT Mod:__ Kullandığınız sanal işletim sistemine IP'yi sanal ağ kartının ataması işlemidir. Bu durumda sanal işletim sistemi, üzerinde çalıştığı fiziksel işletim sistemi ile aynı networkte çalışan diğer bilgisayarlar ile iletişime geçemezler. NAT mode, kısaca; Sanal network oluşturulmasıdır.
* __Bridge Mod:__ Bridge mod'a alınan sanal makine IP talebinde bulunduğunda, IP talebi sanal ağ kartından değilde, üzerinde çalıştığı fiziksel işletim sisteme ip veren DHCP tarafından cevaplanır. Bu sayede fiziksel network dahil olmuş bir sanal makine kullanılabilmektedir.
* __Host Only:__ Sanal makineler için yaratılmış bir ağ ortamı sunar. İnternete çıkış yoktur ve sanal olarak kurulmuş tüm makineler birbirleri ile iletişim sağlayabilir.

Biz __Bridge Mode__'nu seçeceğiz
![](../resim/kurulum/net.png)

Şimdi ise Kali bize otomatik olarak bir IP adresi atamış olması lazım. Bunu terminal açarak `ifconfig` komutu ile öğrenebiliriz. 

```ShellSession
root@kali:~# ifconfig
eth0    Link encap:Ethernet HWaddr 00:0c:29:df:7e:4d
        inet addr:192.168.20.9 Bcast:192.168.20.255 Mask:255.255.255.0
        inet6 addr: fe80::20c:29ff:fedf:7e4d/64 Scope:Link 
--snip--
```

Şimdi ise internet bağlantımızı control edelim.

```ShellSession
root@kali:~# ping www.google.com
```

Buna benzer bir ekranla karşılaştıysak, demek ki sorunsuz internete bağlanmışız.

```ShellSession
PING www.google.com (50.0.2.221) 56(84) bytes of data.
64 bytes from cache.google.com (50.0.2.221): icmp_req=1 ttl=60 time=28.7 ms 
64 bytes from cache.google.com (50.0.2.221): icmp_req=2 ttl=60 time=28.1 ms 
64 bytes from cache.google.com (50.0.2.221): icmp_req=3 ttl=60 time=27.4 ms 64 bytes from cache.google.com (50.0.2.221): icmp_req=4 ttl=60 time=29.4 ms 
64 bytes from cache.google.com (50.0.2.221): icmp_req=5 ttl=60 time=28.7 ms 
64 bytes from cache.google.com (50.0.2.221): icmp_req=6 ttl=60 time=28.0 ms 
--snip--
```

