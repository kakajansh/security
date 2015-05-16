### Network Ayarları

_VMware Player/VirtualBox_ kurulduktan sonra bilgisayarınızda 2 adet sanal ağ kartı oluşacaktır. Bu ağ kartları ile kullandığınız sanal makineler IP alırlar ve fiziksel işletim sistemi üzerinde internete çıkarlar  

* __NAT Mod:__ Kullandığınız sanal işletim sistemine IP'yi sanal ağ kartının ataması işlemidir. Bu durumda sanal işletim sistemi, üzerinde çalıştığı fiziksel işletim sistemi ile aynı networkte çalışan diğer bilgisayarlar ile iletişime geçemezler. NAT mode, kısaca; Sanal network oluşturulmasıdır.
* __Bridge Mod:__ Bridge mod'a alınan sanal makine IP talebinde bulunduğunda, IP talebi sanal ağ kartından değilde, üzerinde çalıştığı fiziksel işletim sisteme ip veren DHCP tarafından cevaplanır. Bu sayede fiziksel network dahil olmuş bir sanal makine kullanılabilmektedir.
* __Host Only:__ Sanal makineler için yaratılmış bir ağ ortamı sunar. İnternete çıkış yoktur ve sanal olarak kurulmuş tüm makineler birbirleri ile iletişim sağlayabilir.

Biz __Bridge Mode__'nu seçeceğiz

Şimdi ise Kali bize otomatik olarak bir IP adresi atamış olması lazım. Bunu terminal açarak. 
ifconfig

İnternet bağlantımızı control edelim

ping www.google.com

