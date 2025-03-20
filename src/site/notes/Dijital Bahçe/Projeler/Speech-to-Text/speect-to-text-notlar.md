---
{"dg-publish":true,"permalink":"/dijital-bahce/projeler/speech-to-text/speect-to-text-notlar/","title":"Aktif Notlar","tags":["notlar","tohum"],"noteIcon":"","created":"2025-03-19T23:46:19.899+03:00","updated":"2025-03-20T14:38:08.545+03:00"}
---


# Aktif Notlar (Nisan Yağmurları)

[[Dijital Bahçe/Projeler/Speech-to-Text/Speech-to-Text\|Nisan Yağmurları]]

**2023/2024** 
Bu dönemdeki tüm ses kayıtlarımı, herzamanki ustalığımla kaybettim.
Ancak hangi konularda ilerlemeler olduğnu aklımda kaldığınca bahsedeyim..

#### Ses kayıtlarınının senkronizasyonu

[Syncthing](https://syncthing.net/) kütüphanesi, bildiğim kadarıyla aynı ağ üzerinde iki makine arasında klasör paylaşımını yapan bir kütüphane.. Açıkçası dökümantasyonu ile fazla ilgilenmedim bile. Youtube vidyoları benim amacım için yeterliydi..

Kendi bilgisayarımda  [Syncthing](https://syncthing.net/)  server kurulumandan sonra  dinlemesi gereken konfigurasyonu yapıp aynı aşamaları mobil tarafda gerçekleştirdim. 

Daha sonra [Inotifywait](https://linux.die.net/man/1/inotifywait) kütüphanesi kullanarak bir bash script yazdım.. 
Amacım eşitlenen , bilgiayarımda eşitlenen klasörü dinlemekti.. Yeni bir dosya yaratıldığında onu bir şekilde speech to text prosesine sokmalıydım. 

Başlangıçta google'a ait servislere baktım. Ücretsiz olanlar tercihimdi. Ancak ses dosyalarım genelde 10dk lık büyüklükte oluyordu.. 
Google ın ücretsit api desteği bu uzunlukta değildi.. 
Öncelikle ses dosyalarını mantıklı parçalara böldüm. Sanırım bunun için ffmeg kullandım..

Klasör dinleme dışında, diğer iş parçacıklarını; [python](https://www.python.org/) programlama dili üzerinden gerçekleştirdim.. 

Genel olarak yapı proje bütünü şu sırada ilerliyordu.. 
- Telefona ses dosyasını kaydet.
- Telefond üzerinden synchthing uygulaması aç. Dosyanın eşitlenmesini bekle.
- Dosya bilgisayarda belirtilen klasöre eşitlenir.
- Klasörü dinleyen script, yeni dosya üretildiğinde , işlem karmaşasını önlemek için, üretilen dosyayı /tmp/destination klasörüne taşır ve [flask](https://flask.palletsprojects.com/en/stable/)  web server'a yeni dosya yolunu, 
  [curl](https://curl.se/) ile POST eder.
-  Yeni dosya yolunu alan web-server async bir işlem ile dosyayı yerinde bulur. Parçalara ayırır, loop ile istek atar. Gelen yanıtları biriktirip birleştirir.
- Tabi loop ile google a istek atmak çok verimsiz bir işlem olduğu için , o zamanki tecrübemle time ile loop işlemini geçiktirdim. Aklıma daha iyisi gelmedi. Açıkçası GPT 3.5 yeni yayınlanmıştı. Prompt yazma konusunda pek becerikli değildim.


İlk aşama bu şekilde gelişti. Daha sonra ek olarak flask kullanmak yerine scrpitler arası [rabbitMQ](https://www.rabbitmq.com/) kullanmayı denedim. 

Watcher(Bash) | rabbit queue | audio trascriber (python)

Bu noktadan sonra bir iş serüvenim oldu, Yaklaşık 1 yıl hiçbir şekilde ilgilenmedim..

**2024/2025** 
#### Yeniden hedefleme

...

---



