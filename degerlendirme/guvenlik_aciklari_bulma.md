### Güvenlik Açıkları bulma

#### Nessus

Nessus, Linux camiasında sıkça kullanılan, kapsamlı bir güvenlik açığı tarama yazılımıdır. Kişisel ve her tür kurumsal olmayan kullanım için ücretsizdir. Genel amacı, bilgisayar sistemlerinde ve bilgisayar ağlarında potansiyel güvenlik açıklarını tespit etmektir.

Nessus bir port tarama yazılımından çok daha üstün özelliklere sahiptir. Nmap benzeri yazılımlar yalnızca karşıdaki sunucu ya da makine hakkında işletim sistemi, açık port bilgileri verebiliyorken Nessus, servislerdeki açıkları eklentilerinin güncelliğine bağlı olarak test edebilir. Çalışma prensibi istemci/sunucu biçimini kullanır ve test edilecek sistemde Nessus sunucu yazılımının açık olması daha derinlemesine test ve analiz imkânı sunar. [Wikipedia](http://tr.wikipedia.org/wiki/Nessus)

Nessus Kali'de hazır kurulu olarak gelmemektedir, kurulumunu bu konuda anlatmıştık. XXX. Yapacağımız örnekleri bedava sürümü olan Nessus Home ile devam edebiliriz. Bu sürümü 16 IP adresi taramayla sınırlıdır. Nessus'u başlatmadan Nessus daemon uygulamasını çalıştırmamız lazım:

```ShellSession
root@kali:~# service nessusd start
```