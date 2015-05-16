## Sanal Lab Ayarları

* Kali Linux nedir
* VirtualBox (VMware) nedir
* VirtualBox & Kali kurulumu

### Kali Linux nedir ?

* Kali bir Linux dağıtımıdır.
* Güvenlik testleri gerçekleştiren pentest, audit ekiplerinin kullanabileceği offensive security araçlarını bünyesinde barındırır.
* Kali Linux iki farklı şekilde kullanılabilir;
    1. Hazır CD den çalıştırma yolu ile
    2. Hard Disk'e kurulum, VMware aracılığı ile

> CD den çalıştırma yönteminin performansı cd okuyucunun hızına bağlıdır. Tavsiye edilen yöntem; Kali' yi diske kurmak veya sanallaştırma platformlarında çalıştırmak

* Masaüstü ortamı olarak BackTrack'teki gibi KDE seçeneği yoktur, yalnızca GNOME masaüstü ortamı kullanılabilir durumdadır.
* Masaüstü kullanarak erişilebilecek proğramların çoğu, komut satırından çalışan program haline getirilmiştir.
* İndirme linki [http://www.kali.org/downloads/](http://www.kali.org/downloads/)

### VirtualBox (VMware) nedir ?

* VirtualBox bir sanallaştırma yazılımıdır.
* İştetim sistemlerini fiziksel makinelere kurmak yerine, VirtualBox aracılığı ile sanal olarak kurulabilir ve sanal network oluşturabilirsiniz.
* VirtualBox ve VMware amaçları aynı farklı proğramlardır, VMware Mac desteklemediği için VirtualBox ile devam edeceğiz.
* İndirme linkleri:
    * [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
    * [VMware](www.vmware.com/go/downloadplayer)

### VirtualBox & Kali kurulumu

#### VirtualBox

İlk önce VirtualBox sitesine gidip proğramı indirdiyseniz ve sonrasında da bilgisayarınıza kurduysanız, ayarlarmalarına devam edebiliriz.

1. __New__ tıklayarak yeni bir sanal makine oluşturalım. Sonradan sıkıntı olmaması için isimlendirmeyi benimkiyle aynı devam edebilirsiniz.
![][vb1]

2. Makinemizin kullanacağı RAM ı belirledikten sonra __Continue__
![][vb2]

3. __Create a virtual hard drive now__ seçerek __Create__
![][vb3]

4. __VDI__ seçerek __Continue__
![][vb4]

5. __Dynamically allocated__ seçerek __Continue__
![][vb5]

6. Şimdi Linux'un belleğimizde kullanacağı alanı belirliyoruz, ben 10 GB seçtim __Create__
![][vb6]

7. Oluşturduğumuz _Kali Linux_ seçerek __Settings__ den ayarlarını yapalım. __System > Processor > Enable PAE/NX__ işaretleyelim.
![][vb7]

> 8 - __Storage__ gelelim ve CD ikonu üstüne tıklayarak, indirdiğimiz _Kali Linux .iso_ dosyasına yönlendirelim ve __OK__ tıklayarak ayarlamalarımızı tamamlayabiliriz.
![][vb8]

[vb1]: ../resim/kurulum/vb1.png
[vb2]: ../resim/kurulum/vb2.png
[vb3]: ../resim/kurulum/vb3.png
[vb4]: ../resim/kurulum/vb4.png
[vb5]: ../resim/kurulum/vb5.png
[vb6]: ../resim/kurulum/vb6.png
[vb7]: ../resim/kurulum/vb7.png
[vb8]: ../resim/kurulum/vb8.png

#### Kali Linux

![][lx3]

[lx1]: ../resim/kurulum/lx1.png
[lx2]: ../resim/kurulum/lx2.png
[lx3]: ../resim/kurulum/lx3.png
[lx4]: ../resim/kurulum/lx4.png
[lx5]: ../resim/kurulum/lx5.png
[lx6]: ../resim/kurulum/lx6.png
[lx7]: ../resim/kurulum/lx7.png
[lx8]: ../resim/kurulum/lx8.png
[lx9]: ../resim/kurulum/lx9.png
[lx10]: ../resim/kurulum/lx10.png
[lx11]: ../resim/kurulum/lx11.png
[lx12]: ../resim/kurulum/lx12.png
[lx13]: ../resim/kurulum/lx13.png
[lx14]: ../resim/kurulum/lx14.png
[lx15]: ../resim/kurulum/lx15.png
[lx16]: ../resim/kurulum/lx16.png
[lx17]: ../resim/kurulum/lx17.png
[lx18]: ../resim/kurulum/lx18.png
[lx19]: ../resim/kurulum/lx19.png
[lx20]: ../resim/kurulum/lx20.png
[lx21]: ../resim/kurulum/lx21.png

#### VirtualBox Guest Additions

Kali dağıtımını VirtualBox aracılığı ile kullanıyorsanız, kullandığınız windows veya linux masaüstünden dosya işlemleri, kopyala yapıştır vb. işlemler için VirtualBox Guest Additions kurulumuna ihtiyaç olacaktır.

* Guest Additions'ı yüklemeden önce linux kernel header'ların kurulması gerekiyor.
    `apt-get update && apt-get install -y linux-header-$(uname -r)`
* Daha sonra VirtualBox ekranında üstten __Devices__ sekmesine tıklanır. Devices sekmesinden __Install Guest Additions__ sekmesine tıklanır.

#### Youtube
[Kali Linux Vmware Kurulumu](https://www.youtube.com/watch?v=wtRIMvOy8Pk)
[Virtualbox veya VWmare Kali Linux kurulumu](https://www.youtube.com/watch?v=lwkzurg5_lY)
[Install Kali Linux in VirtualBox](https://www.youtube.com/watch?v=Rka5MqnCn1E) < _Benim takip ettiğim yol_