### BookApp Kurulumu

BookApp dosyasını http://nostarch.com/pentesting/ linkininden indirdikten sonra, 7-zip programıyla açalım. Şifresi: _1stPentestBook?!_ Aşağıda adım adım Windows 7 sistemimize nasıl yükleyeceğimizi göstereceğiz.

#### Komutları Administrator Yetkisi ile Çalıştırma
Bu talimatta çalıştıracağımız tüm komutları administrator erişimi ile çalıştırmamız gerekiyor. Sağ tıklayarak __Run as administrator__ seçilir.

![b1]

#### ISS Kurulumu

_Step1-install-iss.bat__ dosyasını administrator olarak açalım. Kurulum tamamlandıktan sonra pencerenin kendisi kapanacaktır.

![b2]

#### MS SQL 2008 Express'in Araçları ile Kurulumu

1. SQL Server 2008'i kurmak için _BookApp/SQL_ dizininde bulunan _SQLEXPRWT_x86_ENU.EXE_ dosyasını çalıştıralım. Uyumluluk hatası alırsanız, bunu __Run program__ basarak boşverebilirsiniz.

![b3]

2. _SQL Server Installation Center_ açılması lazım. Solda __Installation__ basalım.

![b4]

3. _New SQL Server stand-alone installation or add features to an existing installation_ basalım. _Setup Support Rules_ penceresi açılacaktır.

4. _Setup Support Rules_ kurulumu bitince, __OK__ basalım.

![b5]

5. Çıkan _Product Key_ diyalogunu da __Next__ ile geçelim.

![b6]

6. __I accept the license terms__ işaretleyerek __Next__.

![b7]

7. Şimdi, __Install__

![b8]

8. Karşımıza çıkan pencereleri __Next__ diyerek geçiştirelim.

9. _Feature Selection_ penceresinde __Select All__ basalım, ve tekrar __Next__

![b9]

10. _Instance Configuration_ penceresinde, _Named instance:_ __SQLExpress__ girelim, ve __Next__

![b10]

11. _Disk Space Requirements_ penceresinde __Next__

12. _Server Configuration_ penceresinde, _SQL Server Database Engine_ listesinden _account name_ __NT AUTHORITY\SYSTEM__ seçelim. _SQL Server Browser's startup type_ ise __Automatic__ seçerek __Next__

![b11]

13. _Database Engine Configuration_ penceresinde, _authentication mode_ __Mixed Mode__ olarak değiştirelim ve şifresini __database__ yapalım. __Add Current User__ basarak __Next__

14. Karşımıza çıkan __Error and Usage Reporting__ ve __Installation Rules__ pencerelerini de __Next__ diyerek geçiyoruz. Sonrasında ise __Install__. Kurulum tamamlandıktan sonra __Close__ diyerek kapatıyoruz.

#### SQL SP3 Kurulumu

Gene _BookApp/SQL_ dizininden _SQLServer2008SP3-KB2546951-x86-ENU.exe_ dosyasını çalıştıralım, ve _License Terms_ penceresini kabul ederek varsayılan özelliklerle __Next__ basarak devam edelim. _Ready to Update_ penceresinde __Update__ basalım, bitince de __Close__ ile kapatabiliriz.

##### Named Pipes Etkinleştirme

1. _Sql Server Configuration Manager_ açalım; __Start > All Programs > Microsoft SQL Server 2008 > Configuration Tools > SQL Server Configuration Manager__ 

2. _SQL Server Confiration Manager_'in sol taradında, __SQL Server Network Configuration__ seçelim. Aşağısında açılan __Protocols for SQLEXPRESS__ çift tıklayalım.

![b12]

3. __Named Pipes__ üstüne gerek sağ tıklayalım ve __Enabled__ seçelim. Servisi yeniden başlatmanız gerektiğine dair mesaj alacaksınız.

4. Şimdi ise, soldaki panelden __SQL Server Services__ seçelim, __SQL Server (SQLEXPRESS)__ sağ tıklayalım ve __Restart__

5. _SQL Server Configuration Manager_ kapatalım.

![b13]

##### SQL ve ISS Inboud Firewall Kurallarını Oluşturma

_Step2-Modify-FW.bat_ dosyasını administrator olarak çalıştırıyoruz.

##### SQL XML Desteğinin Kurulumu

_BookApp/SQL_ dizininden _sqlxml_x86-v4.msi_ dosyasını çalıştıralım. License koşullarını kabul ederek, çıkan pencereleri varsayılan değeri ile __Install__ basalım.

##### Kitapçı Uygulamamızın Kurulumu

1. __Start > All Programs > Accessories__ gelerek __Command Prompt__ üstüne sağ tıklayarak __Run as administrator__ seçelim.

![b14]

2. _Command prompt_ girdikten sonra, __cd__ komutu ile Kitapçı uygulamamızın olduğunu dizinine gidelim. (C:/Users/IEUser/Desktop/BookApp). __dir__ komutu çalıştırarak _Step3-Install-App.bat_ dosyasının olduğnu bir kontrol edelim. Sonra __Step3-Install-App.bat__ yazarak çalıştıralım. __Extract__ basıyoruz.

3. _Command prompt_'dan çıkmak için __exit__ yazıyoruz.

![b15]

##### Uygulama Verilerini MS SQL Ekleme

1. __Start > All Programs > Microsoft SQL Server 2008 > SQL Server Management Studio__ gidelim

2. _Authentication_ seçeneğini __SQL Server Authentication__ olarak değiştirelim. _Login:_ __sa__ _Password:_ __database__ ve __Connect__

![b16]

3. __File > Open > File__ seçerek _BookApp_ dizininde bulunan _db_insert.sql_ dosyasını açalım. __Execute__ basarak çalıştıralım ve sonrasında __SQL Server Management Studio__ kapatalım.

4. Şimdi ise, _Windows Explorer_ ile _C:\inetpub\wwwroot\Book_ gidelim. _AuthInfo.xml_ dosyası üstünde sağ tıklama, __Properties > Security__ seçelim. _SYSTEM_ seçili iken _Permissions_ altındaki __Edit__ basalım. __ISS_USERS__ seçelim, __Full Control__ yanındaki __Allow__ işaretleyelim, ve __Apply__ sonra da __OK__.

![b17]

5. Son olarak, Internet Explorer ile http://localhost/bookservice/ adresine gidelim. Herşeyi doğru takip ettiyseniz, sitemizin anasayfasını göreceksiniz.

![b18]

[b1]: ../resim/book/b1.png
[b2]: ../resim/book/b2.png
[b3]: ../resim/book/b3.png
[b4]: ../resim/book/b4.png
[b5]: ../resim/book/b5.png
[b6]: ../resim/book/b6.png
[b7]: ../resim/book/b7.png
[b8]: ../resim/book/b8.png
[b9]: ../resim/book/b9.png
[b10]: ../resim/book/b10.png
[b12]: ../resim/book/b12.png
[b13]: ../resim/book/b13.png
[b14]: ../resim/book/b14.png
[b15]: ../resim/book/b15.png
[b16]: ../resim/book/b16.png
[b17]: ../resim/book/b17.png
[b18]: ../resim/book/b18.png