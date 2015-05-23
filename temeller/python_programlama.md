### Python Programlama

Linux sistemleri genelde Python, Perl ve diğer scriptleme dillerinin yorumlayıcıları ile beraber gelmektedir. Kali de buna hariç olmadığı için, herhangi bir Python kurma endişemiz yoktur, yazdığımızı direk çalıştırabiliriz. Şimdi bazı temel Python komutlarına bakalım.

Bu örneğimizde sistemimizde olan port'lardan birinin izlenip izlenmediğini kontrol edeceğiz. Başlangıç olarak:

```ShellSession
#!/usr/bin/python
ip = raw_input("Enter the ip: ")
port = input("Enter the port: ")
```

Bir önceki bölümde, scriptimizin ilk satırı terminalin hangi yorumlayıcı kullanacağını gösteriyoruz demiştik. Burda da aynı, _/usr/bin/python_ dosyasında bulunan python yorumlayıcısına yönlendiriyoruz. 
* `raw_input` = kullanıcıdan veri girişi alma
* `input` = kullanıcının gireceği veriyi, sayı olarak atayacağımız için

Programı çalıştırabilmek için `chmod 744` ile yetkiyi verelim, ve deneyelim. Ekran:

```ShellSession
root@kali:~/mydirectory# chmod 744 pythonscript.py
root@kali:~/mydirectory# ./pythonscript.py
Enter the ip: 192.168.2.10
Enter the port: 80
```

Kullanıcıdan veriyi aldıktan sonra, işlem yapmaya bakalım. Network ilgili komutlar için Python'un socket kütüphanesini `import socket` komutu ile dahil edelim. Python komutları hakkında websitesine yüz tutulabilir, kısaca biz burda gireceğimiz port'a bağlanmasını istiyoruz. Socket kütüphanesinin `connect` ve `connect_ex` metodları bulunmaktadır, ancak bizim burda ikincisini seçmemizin sebebi: bağlantı gerçekleşirse 1 (true), değilse 0 (false) değeri alacağımızdan.

```ShellSession
#!/usr/bin/python
import socket
ip = raw_input("Enter the ip: ")
port = input("Enter the port: ")
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
if s.connect_ex((ip, port)):
    print "Port", port, "is closed"
else:
    print "Port", port, "is open"
```

Şimdi scriptimizi çalıştırıyoruz. İstenen bilgileri girelim, 192.168.2.10:80 portu açık olduğundan; __Port 80 is open__ sonucu aldık. Bir kere daha tekrar çalıştırarak port numarasını 81 girelim; __Port 81 is closed__ sonucunu alacağız.

```ShellSession
root@kali:~/# ./pythonscript.py
Enter the ip: 192.168.2.10
Enter the port: 80
Port 80 is open
```

--

##### DAHA FAZLASI İÇİN:

* [Python Programlama Dili](http://belgeler.istihza.com/py3/)
* [Bilgisayar Bilimcisi gibi Düşünmek](http://yzgrafik.ege.edu.tr/%7Etekrei/dersler/bbgd_p/BBGD_PIO.pdf)