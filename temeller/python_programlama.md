### Python Programlama

```ShellSession
#!/usr/bin/python
ip = raw_input("Enter the ip: ")
port = input("Enter the port: ")
```

```ShellSession
root@kali:~/mydirectory# chmod 744 pythonscript.py
root@kali:~/mydirectory# ./pythonscript.py
Enter the ip: 192.168.20.10
Enter the port: 80
```

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

```ShellSession
root@kali:~/# ./pythonscript.py
Enter the ip: 192.168.20.10
Enter the port: 80
Port 80 is open
```

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

```ShellSession
root@kali:~# gcc cprogram.c -o cprogram
```

```ShellSession
root@kali:~# ./cprogram
Pass your name as an argument
```

```ShellSession
root@kali:~# ./cprogram cansu
Hello cansu
```

http://belgeler.istihza.com/py3/
http://yzgrafik.ege.edu.tr/%7Etekrei/dersler/bbgd_p/BBGD_PIO.pdf







