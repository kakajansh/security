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

Bu çalışma, metasploit framework projesinde bulunan farklı encoderları kullanarak meterpreter içeriğini antivirusler tarafından tanınmaz yapıp, ayrıca masum bir uygulama imajı kazandırmak üzere bir kaç satır kod eklemektedir.



##### DAHA FAZLASI İÇİN

* [Antivirüs Programları Nasıl Çalışır?](http://www.elektrikport.com/teknik-kutuphane/antivirus-programlari-nasil-calisir/11475)
* [Kendi Backdoor'unuzu Oluşturun](http://onuraktas.net/kendi-backdoorunuzu-olusturun/)