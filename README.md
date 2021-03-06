# selenium-grid-demo
Selenium Grid 4.0.0 Demo Example 

![Ekran Resmi 2021-07-09 11 16 47](https://user-images.githubusercontent.com/28295071/125047213-6abf1500-e0a7-11eb-81da-b0650ab6b076.png)


Öncelikle selenium grid jar dosyasını bilgisayarımıza indiriyoruz. 
Link: https://www.selenium.dev/downloads/

Ben bu proje için 4.0.0-beta-4 versiyonunu kullandım.

Selenium Grid kurulumu için 4 adet yöntem var. Bunlar:
Standalone
Hub and Node
Distributed
Docker

Ben burada Standalone, Classical Grid (Hub and node) ve Distributed adımlarıyla kurulumlar yaptım.

Standalone için;

java -jar selenium-server-4.0.0-alpha-7.jar standalone

konutunu terminalde çalıştırıyoruz.


Hub and Node Mode için;

java -jar selenium-server-4.0.0-alpha-7.jar hub

java -jar selenium-server-4.0.0-alpha-7.jar node --detect-drivers true


Distributed içinse sırasıyla aşağıdaki komutları çalıştırmamız gerekli;

java -jar selenium-server-4.0.0-alpha-7.jar  event-bus

java -jar selenium-server-4.0.0-alpha-7.jar sessions

java -jar selenium-server-4.0.0-alpha-7.jar sessionqueue

java -jar selenium-server-4.0.0-alpha-7.jar distributor --sessions http://localhost:5556 --sessionqueue http://localhost:5559 --bind-bus false

java -jar selenium-server-4.0.0-alpha-7.jar router --sessions http://localhost:5556 --distributor http://localhost:5553 --sessionqueue http://localhost:5559

java -jar selenium-server-4.0.0-alpha-7.jar node --detect-drivers true


Router: Yönlendirici, isteği doğru bileşene iletmekle ilgilenir.
Yönlendirici, istekleri daha iyi işleyebilecek bileşene göndererek gridteki yükü dengelemeyi amaçlar.

Distributor: Dağıtıcının görevi yeni bir session isteği almak ve session ın oluşturulabileceği uygun bir Node bulmaktır.

Session Map:Session id ile nodu eşler.

New Session Queue: İstekleri sıraya koyar ve zaman aşımı ve yeniden deneme adımlarını yönetir.

Event Bus: Nodes, Distributor, New Session Queuer, ve Session Map  arasındaki iletişimi sağlar.

Hub: Router, Distributor, Session Map, New Session Queuer, Event Bus ın birleşimidir.

GRID 3:

![grid3](https://user-images.githubusercontent.com/28295071/124995936-c7dbac00-e050-11eb-97f7-17f4029ec271.png)

GRID 4:

![grid_4](https://user-images.githubusercontent.com/28295071/124996059-ffe2ef00-e050-11eb-8dd3-a430eab5d918.png)

Ayrıca selenium grid 4 kapsamlı bir docker konfigurasyonu ile gelmiştir.
