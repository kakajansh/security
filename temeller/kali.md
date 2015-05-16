### Kali Linux nedir ?

* Kali bir Debian tabanlı Linux dağıtımıdır.
* Güvenlik testleri gerçekleştiren pentest, audit ekiplerinin kullanabileceği offensive security araçlarını bünyesinde barındırır.
* Penetrasyon test araçlarını içerir. Yoksa hepsini teker teker kurmak gerçek bir başağrısı olmakla beraber, büyük bir zaman kaybıdır.
* Kali Linux iki farklı şekilde kullanılabilir;
    1. Hazır CD den çalıştırma yolu ile
    2. Hard Disk'e kurulum, VMware aracılığı ile

> CD den çalıştırma yönteminin performansı cd okuyucunun hızına bağlıdır. Tavsiye edilen yöntem; Kali' yi diske kurmak veya sanallaştırma platformlarında çalıştırmak

* Masaüstü ortamı olarak BackTrack'teki gibi KDE seçeneği yoktur, yalnızca GNOME masaüstü ortamı kullanılabilir durumdadır.
* Masaüstü kullanarak erişilebilecek proğramların çoğu, komut satırından çalışan program haline getirilmiştir.
* İndirme linki [http://www.kali.org/downloads/](http://www.kali.org/downloads/)

#### Kurulumu

1. 
![][lx1]

2. Makina çalıştığında farklı kurma seçenekleri geliyor. Ben __Install__ tercih ederek, normal kuruluma devam ediyorum.
![][lx2]

3. Karşımıza kurulumu hangi dil ile yapacağımızı gösteren bir ekran geliyor. __English__ seçerek devam ediyorum
![][lx3]

4. Buna benzer bir ekranla karşı karşıya kalacaksınız.. Biraz sabredip bekliyoruz.
![][lx4]

5. _Hostname:_ __kalilinux__ yaz __Continue__
![][lx5]

6. _Domain name:_ __private.edu__ yaz __Continue__  
    Not: resim az farklılık gösterebilir, sonradan _private.edu_ yaptım.
![][lx6]

7. Çıkan ekranda root şifresini belirliyoruz.  
    _Root password:_ bir şifre belirleyip devam ediyoruz. Ben __password__ yazdım ama, uzun seçmenize şimdilik gerek yok, kısa birşeyle devam edin.
![][lx7]

8. _Re-enter password to verify:_ şifremizi bir tekrarlayalım.
![][lx8]

9. Saat ayarlarını yapacağımız ekran açılıyor.  
    _Select your time zone:_ __Eastern__ > __Enter__
![][lx9]

10. Bu adımda diskin nasıl yapılandırılacağını soruyor. Tek parça isteniyorsa ilk seçenek seçilerek devam edilir.  
    _Partitioning method:_ __Guided - use entire disk__ > __Enter__
![][lx10]

11. Kurulumun hangi diske yapılacağını soruyor. Tek disk var ise aşağıdaki gibi gözükecektir.  
    __Enter__
![][lx11]

12. Bu aşamada Linux da bulunan Home, usr, var, tmp gibi alanların farklı partitionlara kurulabileceğini söylüyor. Hepsini tek partitiona kurmak için ilk seçenek seçilir.  
    __Enter__
![][lx12]

13. Disk ayarlarının özetini gösteriyor. Ayarlar kontrol edildikten sonra devam edilir.  
    __Enter__
![][lx13]

14. Burda otomatik seçenek __NO__ olcak, onu acele etmeden __Yes__ seçelim ve __Enter__
![][lx14]

15. Şimdi böylelikle başlanğıç ayarlamalarımızı bitirmiş oluyoruz. Kurulum başlıycak, bir kahve molası..
![][lx15]

16. __YES__
![][lx16]

17. Boş geçelim __Continue__
![][lx17]

18. __YES__
![][lx18]

19. __Continue__
![][lx19]

20. Tebrik ederim! Böylelikle Sanal makinemizin kurulumunu yapmış bulunmaktayız. Makine yeniden başladıktan sonra, bu ekran gelecek karşımıza.  
    _Username:_ __root__
    _Password:_ __password__ (kurulum sırasında belirlediğimiz)
![][lx20]

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
