### C Programlarını Yazma ve Derleme

Son olarakta yazacağımız C proğramlarını Linux'ta nasıl çalıştıracağımıza bakalım. Diğer Bash ve Python gibi scripleme dilleri gibi direk çalıştırlmamakla beraber, ilk önce programımızı bilgisayarın anlayacağı dile çevirip öyle çalıştırmamız lazım. Kali Linux bunu yapabilmemiz için kendisinde GNU derleyicisini bulundurmaktadır. O zaman basit bir örneğe bakalım:

```ShellSession
#include <stdio.h>
int main(int argc, char *argv[])
{
    if(argc < 2)
    {
        printf("%s\n", "Pass your name as an argument");
        return 0;
    }
    else
    {
        printf("Hello %s\n", argv[1]);
        return 0;
    }
}
```

* C programını derleyeceğimiz için diğer Python ve Bash'da olduğu gibi hangi yorumlayıcı kullanacağımızı göstermeyiz. 
* `#include <stdio.h>` diyerek C'de standard giriş çıkış bilgilerini almak için kullanılan dosyayı dahil ediyoruz.
* Herbir C programında `main` fonksiyonu olmak zorundadır. Program ilk başladığında çalışır.
* `argc` gireceğimiz argument sayısı
* `argv[1]` girdiğimiz argumentlerden birincisi
* `printf` ekrana çıktı yazma
* C programları `return` ile bitirilir

Şimdi programımızı `cprogram.c` olarak kaydedelim ve aşağıda gösterdiğimiz gibi __GCC__ ile derleyelim.
* `-o [isim]` derlenen programın ismini belirleriz.

```ShellSession
root@kali:~# gcc cprogram.c -o cprogram
```

Programımızı argument atamadan çalıştırdığımızda _Pass your name as an argument_ hatası alırız.

```ShellSession
root@kali:~# ./cprogram
Pass your name as an argument
```

Argument atadığımızda ise, _Hello cansu_

```ShellSession
root@kali:~# ./cprogram cansu
Hello cansu
```