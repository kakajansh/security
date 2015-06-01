### Güvenlik Açıkları bulma

#### Nessus

Nessus, Linux camiasında sıkça kullanılan, kapsamlı bir güvenlik açığı tarama yazılımıdır. Kişisel ve her tür kurumsal olmayan kullanım için ücretsizdir. Genel amacı, bilgisayar sistemlerinde ve bilgisayar ağlarında potansiyel güvenlik açıklarını tespit etmektir.

Nessus bir port tarama yazılımından çok daha üstün özelliklere sahiptir. Nmap benzeri yazılımlar yalnızca karşıdaki sunucu ya da makine hakkında işletim sistemi, açık port bilgileri verebiliyorken Nessus, servislerdeki açıkları eklentilerinin güncelliğine bağlı olarak test edebilir. Çalışma prensibi istemci/sunucu biçimini kullanır ve test edilecek sistemde Nessus sunucu yazılımının açık olması daha derinlemesine test ve analiz imkânı sunar. [Wikipedia](http://tr.wikipedia.org/wiki/Nessus)

Nessus Kali'de hazır kurulu olarak gelmemektedir, kurulumunu bu konuda anlatmıştık. XXX. Yapacağımız örnekleri bedava sürümü olan Nessus Home ile devam edebiliriz. Bu sürümü 16 IP adresi taramayla sınırlıdır. Nessus'u başlatmadan Nessus daemon uygulamasını çalıştırmamız lazım:

```ShellSession
root@kali:~# service nessusd start
```

Servisi başlattıktan sonra https://kali:8834 adresine gidelim, ve önceki bölümlerde girmiş olduğumuz kullanıcı adı ve parola ile giriş yapalım. 

##### Nessus Policies

Nessus web arayüzünün ekranın üst kısmında birkaç sekmesi vardır. _Policies_ sekmesi ile başlayalım. _Nessus Policies_ güvenlik açığı aramalarımızda  çalıştırdığımız port tarama, açık kontrolü gibi işlemlerin saklandığı ayar dosyası hizmetini görmektedir.

Yeni bir _policy_ oluşturmak için sağ kısımda bulunan __New Policy__ tıklanır. Karşımıza çıkacak yardımcı sihirbazı bizim amacımıza göre _policy_ oluşturmamıza yardımcı olacaktır. Basit bir örnek olarak __Basic Network Scan__ seçelim.

Şimdi bizden _policy_ hakkında isim, açıklama, erişilebilirlik gibi bazı temel sorular sorulacaktır. Tamamlayınca, __Next__

Sonra dahili mi yoksa harici tarama yapılacağına dair sayfa açılacak. __Internal__ seçelim ve __Next__

Eğer kimlik bilgileriniz varsa, Nessus hostlar ile kimlik doğrulamasını yapacak ve güvenlik açığı için arama yapacaktır. Bu özellik genelde dahili olarak ağ güvenligi tespit etmek için kullanılır. Kimlik bilgileri sonraki adımlarda da girilebilmektedir. Şimdilik, boş bırakalım ve __Save__

Sonra oluşturduğumuz _policy_ _Policy tab_ altında sıralanmış olduğunu göreceksiniz.

##### Nessus ile Tarama

Şimdi ise, _Scans_ sekmesine geçelim ve hedef makinelerimize karşı Nessus'u çalıştıralım. __Scans > New Scan__ basalım ve resimdeki gibi bilgileri dolduralım. 
* Name: yaptığımız aramanın ismi
* Policy: oluşturduğumuz _policy_'lardan bir tanesini seçiyoruz
* Targets: taranacak hedef makineleri

Nessus olabildiğine fazla bilgi ve hata bulabilmek için hedefimize karşı prob serisini çalıştıracaktır. Çalışan taramalar _Scans_ sekmesinde görüntülenecektir.

Tarama bitiminde, sonuçlarına bakalım.

Gördüğünüz gibi, Nessus Windows XP ve Ubuntu sistemlerinde kritik sorunlar buldu, Windows 7 sisteminde ise sadece bilgi amaçlı veri bulabildi. Ayrıntılı bilgi için _host_'lardan bir tanesini seçelim. Aşağıda Windows XP için ayrıntılı olarak verilmiştir.

Açıkları tarama araçları hakkında ne derseniz deyin, ama Nessus kadar az çaba gerektiren hem-de iyi ve hızlı sonuçlar alınabilen başka bir araç zor bulunur. Mesela, Nessus'un sonuçlarına bakarsak hedefimizdeki Windows XP sisteminin önceden de bahsettiğimiz MS08-067 yaması eksik olduğunu belitiyor. Ve görülüyor ki diğer Microsoft yamalarının eksikliği SMB sunucusunu etkilemektedir.

Hangi açık sızmak için daha elverişli? Nessus'un verdiği çıktılara bakarsak, bir açık hakkında kullanabileceğimiz sızma yöntemleri hakkında da bilgi vermektedir. Mesela, MS08-067 çıktısına baktığımızda Metasploit ve buna benzer Core Impact, Canvas araçları ile sızma yapılabileceğimizi göstermekte.

Nessus taraması tamamlanınca, _Export_ butonuna tıklayarak çıktısını alabiliriz. Başlıca PDF, HTML, XML, CSV dosyalarına kaydedilebilir.

















