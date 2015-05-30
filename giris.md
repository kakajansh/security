## Giris 

Günümüz dünyasında her geçen gün bireyler, şirketler, kurumlar ve devletler için __"bilgi = daha çok güç"__ haline geldiği gibi, bilgi teknolojileri geliştikçe güvenlik sorunları da artmaktadır. Sistemimizin güvenliğini sağlayabilmek için zamanla saldırganın gözüyle bakmamız da faydalı olacaktır. Bu sebeple, birileri sisteminize saldırmadan kendize bir saldırı düzenleyebilmeniz için, saldırı yöntemleri hakkında genel bir bilgi vermek için, gerekirse saldırganın araç-gereçleri ile sizleri tanıştırma amaçlı kaleme alınmıştır. Çalışmamızın faydalı olacağını ümit ediyoruz..

##### __Amaç__

* Bilgisayar güvenliği konusunda türkçe kaynak neredeyse yok denebilecek kadar azdır. Google'ın herşeyi bildiğine dair ne kadar inancımız olsa da, bu konuda sağlam bir bilgi sahibi olmak oldukça zordur. Araştırma yaptıysanız göreceksiniz ki _herşey hakkında hiçbir şey_ bilgi denizine dalacaksınız. Bilgilerin çoğu ya eski ya da yeterli uygulama örnekleri bulunmadığından takip edilmesi zordur. Yaptığımız çalışmanın her örneği şahsımız tarafından denenmiş, ve sizin de kolayca takip edebilmeniz için adım adım anlatımı resimlerle gösterilmiştir.

##### __Çalışmanızın kaynağı nedir?__

* Çalışmamızın ana kaynağı __Georgia Weidman__ tarafından __2014__ senesinde yazılmış __PENETRATION TESTING__ kitabıdır. Yanı sıra türkçe kaynaklarından da faydalanarak ekleme çıkarma yapılmıştır. Ayrıca konuların son kısmında bulunan __DAHA FAZLASI__ bölümünde o konu için kendizi ilerletebileceğiniz bir kaynak listesi oluşturulmuştur.

* __Beklentilerim ne olmalı?__

> _Linux, terminal, bash, python, sql injections, xss, exploit, payload, metasploit_ vb terimleri duymuşsanız, ama bir türlü bir araştırma yapmak için zaman ve mekan musait olmadığından öğrenememişseniz; iyi bir başlangıç noktası olabilir.

* __Beklentilerim ne olmamalı?__

> Dikkat ettiyseniz çalışmamız, bir kuruma zarar verme, şifre kırma, hesap çalma için amaçlanmamıştır. Kurduğumuz sistemde saldırgana karşı alacağımız önlemleri öğrenmek amaçlıdır.

* __Hata buldum, ne yapmalıyım?__

> Yazı, dilbigisi hataları, anlatım bozuklukları, tekniki hatalar olabilir. Github'a giriş yaparak __Issues__ bölümünden bildirebilirsiniz. Bir yabancı olarak Türkçe yazdığımızdan normaldir :) 

* __Yaptığın çalışmayı tebrik etmek isterim__

> Yukarıda bir __STAR__ :star: tıklayarak memnuniyetinizi bildirebilirsiniz.

* __Niye PDF veya Word dosyası değilde Github?__

> Aslında, şahsen Github'y ilk kez bu şekil büyük çaplı bir çalışmada kullanıyorum. O yüzden ilk başta Markdown öğrenme, dosya düzenlemeleri baya bir karmaşık gelmişti. Ama Markdown yazı stiline alışınca, diğerlerine göre daha hızlı bir sonuç elde edilebilmektedir. Eminim siz de bu tercihi yaptığıma memnun kalacaksınız :) 
Fark olarak başlıca şunlar:
* Kod kısmı için daha güzel görünüm
* Kolayca kod kısımlarından kopyala yapıştır yapılabilmesi
* PDF, HTML, vb formatlarına çevirebilme
* Güncellemesi kolay, ve aynı anda herkese erişilebilir
* Mac kullanıcısı olarak extradan bir Word kurma derdi yok
* __Fork__ yaparak çalışma devamı, herhangi biri tarafından sürdürülebilmesi