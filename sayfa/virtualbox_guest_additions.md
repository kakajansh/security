### VirtualBox Guest Additions

Kali dağıtımını VirtualBox aracılığı ile kullanıyorsanız, kullandığınız windows veya linux masaüstünden dosya işlemleri, kopyala yapıştır vb. işlemler için VirtualBox Guest Additions kurulumuna ihtiyaç olacaktır.

1. Sistemimiz kullanıma hazır olduktan sonra artık komutlarımızı çalıştırabilirz. Ama son birşey daha, güncelleştirme. Tabii ki de isteğe bağlı ve internet hızına göre biraz uzun sürebilir. 
    `apt-get update && apt-get -y upgrade`

2. Daha sonra VirtualBox ekranında üstten __Devices__ sekmesine tıklanır. Devices sekmesinden __Install Guest Additions__ sekmesine tıklanır.

3. Ekrana gelen uyarıda __Cancel__ seçeneği tıklanır.
    ![][va1]

4. Daha sonra VBoxLinuxAdditions.run dosyasının olduğu dizine gidip çalıştırma yetkisi verip çalıştırıyoruz.
    ```
    cp /media/cd-rom/VBoxLinuxAdditions.run /root/
    chmod 755 /root/VBoxLinuxAdditions.run
    ./VboxLinuxAdditions.run
    ```
    ![][va2]

5. Sistemi tekrardan başlatalım. Terminal 'de `reboot` yazabiliriz. Sistem açıldıktan sonra, Sistem tam ekran olma, kopyala yapıştır gibi özelliklerin geldiğni göreceksiniz.

[va1]: ../resim/kurulum/va1.png
[va2]: ../resim/kurulum/va2.png

