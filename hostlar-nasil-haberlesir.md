# Hostlar Nasıl Haberleşir ?

Bu bölümde host cihazlarının birbiri ile iletişim kurabilmesi için gereken şartlardan bahsediyor olacağız.

## Aynı Ağdaki Cihazlar Nasıl Haberleşir ?

Bir host aynı ağda olduğu bir başka hosta veri göndereceği zaman, hedef hostun IP adresini bilmesinin yanında MAC adresini de bilmek zorunda. Çünkü daha önce ele aldığımız OSI ve TCP/IP modellerinde de bizzat gördüğümüz gibi cihazların IP adresinden önce MAC adresi tanınıyor. 

![de-layer2.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/osi-modeli/de-layer2.webp)

Doğru MAC eşleşmesi olmadan IP adresinin kontrolü de gerçekleşmediği için öncelikle MAC adresi belirtilmeli. 

Örneğin ethernet ile birbirine bağlı olan cihazlarda veri iletişimi için öncelikle hedef cihazı temsil eden MAC adresine ihtiyacımız var. Neticede ağ bağlantısı aslında ağ kartı ile gerçekleştiriliyor ve bu ağ kartlarının kimlikleri de benzersiz MAC adresleridir. Dolayısıyla MAC adresini bilmeden verileri doğru makineye iletemeyiz.

Ağ yapısı gereği MAC adresleri donanımlara kalıcı olarak tanımlanmışken, IP adresleri mantıksal olarak tanımlanmış adreslerdir. Dolayısıyla duruma göre zaman içinde aynı cihaza farklı IP adresleri tanımlanabiliyor. Bu sebeple IP adresi ile MAC adreslerini arasında organik bir bağ yoktur. Bizim IP adresini bildiğimiz cihaza veri gönderebilmek için bu cihazın MAC adresini öğrenmemizi sağlayan ARP protokolünü kullanmamız gerek.

**ARP** ifadesi “**A**ddress **R**esolution **P**rotocol” yani “adres çözümleme protokolü” ifadesinin kısaltmasından geliyor. Nasıl çalıştığını hemen örnek üzerinden ele alalım.

Aşağıdaki gibi iki LAN ağının birbirine router ile bağlı olduğunu varsayalım.

![LAN-to-LAN.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/LAN-to-LAN.webp)

192.168.1.20 IP numaralı host, 192.168.1.10 IP adresli hosta veri göndermek isterse öncelikle bu hostun MAC adresini öğrenmesi gerek. Bunun için ARP broadcast yayını ile herkese bu IP adresinin MAC adresini sorabilir. Bu ARP paketinde da kendi IP ve MAC adresi ve hedef IP adresi yer alır.

![ARP-1.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP-1.webp)

Bu ARP sorgusu lokal ağdaki tüm cihazlara gönderilir. Router özellikle konfigüre edilmediği sürece broadcast yayınını diğer ağlara taşımaz. Bu sebeple ARP mesajı yalnızca lokal ağdaki cihazlara ulaştırılır.

![ARP-2.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP-2.webp)

ARP mesajını da yalnızca hedefteki IP adresine sahip olan host yanıtlar. Yanıtlama işlemi sırasında da kaynağın IP ve MAC bilgisini öğrendiği için bunları, daha sonra kullanmak üzere kendi ARP tablosuna ekler. Kaynak adresini öğrendiği için de yanıtı doğrudan kaynağa unicast olarak iletir.

![ARP3.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP3.webp)

![ARP4.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP4.webp)

ARP yanıtı sayesinde B hostu da, A hostunun IP ve MAC bilgisini kendi ARP tablosuna ekler. Bu sayede artık B hostuna yani 192.168.1.10 IP adresini veri iletmek istediğinde MAC adresini buradan kontrol edip doğrudan o hosta veri iletebiliyor olacak. En yalın haliyle lokal ağdaki bir cihazın MAC adresinin öğrenilmesi bu şekilde gerçekleşiyor.

Tam da bu noktada, “*MAC adresi bilinmeden cihazlara veri gönderilemiyorken nasıl ARP sorgusu gönderilebiliyor?*” diye düşünmüş olabilirsiniz.

ARP gönderilirken broadcast yani tüm cihazları hedefleyerek gönderildiği için hedef MAC adresi olarak da tüm cihazları temsil eden özel bir MAC(FFFF.FFFF.FFFF) adresi kullanılıyor. Bu sayede daha öncesinde MAC adresini bilmeye gerek kalmadan ağdaki tüm cihazlara broadcast yayını ile mesajı göndermek mümkün oluyor.

Lokal ağdaki cihazların MAC adresini nasıl öğrenebileceğimize değindik. Şimdi kısaca harici ağlardaki hostlar ile nasıl iletişime geçebileceğimizi ele alalım.

## Farklı Ağdaki Cihazlar Nasıl Haberleşir ?

Bir host harici bir ağdaki host ile iletişime geçmek istediğinde, hedef IP adresine bakarak bu hostun kendi ağına dahil olmadığını biliyor. Çünkü kendi IP adresini ve alt ağ maskesini yani subnet mask değerini biliyor. Bu sayede kendi ağındaki IP aralığını kontrol edip, bu ağın kendi ağındaki bir host olmadığını öğrenebiliyor. 

Elbette bu bilgi yeterli değil çünkü hedef cihazın MAC adresinin de bilinmesi gerekiyor. Bu noktada devreye router aygıtının yardımı giriyor. Router bağlı olduğu ağlardaki cihazların IP ve MAC kayıtlarını kendi tablosunda tuttuğu için paketlerin hangi cihazlara gönderilmesi gerektiğini belirleyebiliyor.

![router-ip-table.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/router-ip-table.webp)

Daha önce routerların ağlar arasındaki “gateway” olduğundan bahsetmiştik. Bu sebeple her host bağlı olduğu gateway adresini yani routerın bu ağdaki IP adresini biliyor. Bu sebeple eğer iletişime geçeceği IP adresi kendi ağında değilse bu paketi gateway olarak bilinen routera teslim ediyor. Fakat teslim etme işlemi için de elbette ilk olarak bu routerın MAC adresini bilmesi gerek. Çünkü sizin de bildiğiniz gibi yalnızca IP adresi ile veri iletilemez. 

Host, Router aygıtının MAC adresini öğrenmek üzere ARP ile bu IP adresinin MAC adresini broadcast şeklinde kendi ağındaki herkese soruyor. 

![ARP5.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP5.webp)

![ARP6.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP6.webp)

Bu ARP sorgusuna yalnızca hedef IP adresine sahip olan router cevap veriyor. Bu sayede hem router hem de sorgu yapan host birbirilerinin IP ve MAC bilgilerini kendi tablolarına kaydediyorlar. 

![ARP7.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP7.webp)

![ARP8.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP8.webp)

Artık böylelikle lokal ağ dışındaki bir hosta veri göndermek için bu verileri routera teslim etmemiz gerekiyor. Yani hedef IP olarak harici ağdaki hostun IP adresini belirtiyorken, MAC adresi olarak default gateway olan router aygıtının MAC adresini belirtiyoruz.

![ARP9.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP9.webp)

Bu sayede bu frame halindeki veri paketi routera ulaştığında router bu frame’i açarak hangi IP adresine gönderildiğini öğreniyor. Bu IP adresi kendisine bağlı olan ağdaysa bunu ilgili adrese iletiyor. 

![ARP10.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP10.webp)

![ARP11.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/ARP11.webp)

Paketi alan host, gönderici IP adresi olarak diğer ağdaki hostun olduğunu öğrendiği için yanıt verirken benzer yolu izleyerek yanıtı ilgili hosta ulaştırabiliyor.

Router bağlı olduğu ağlardaki cihazların IP ve MAC bilgilerini de ARP ile öğrenip kendi tablosunu tuttuğu için ağlar arasında yönlendirme işlemi gerçekleştirebiliyor. Bu sayede lokal ağımızın dışında bulunan bir ağdaki host ile veri alışverişinde bulunabiliyoruz. 

![router-ip-arp-table.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/hostlar/router-ip-arp-table.webp)

Örneğin geniş ağ olan internet üzerinde başka bir IP adresine paket iletmek istediğinizde, yine kendi ağınızdaki default gateway olarak kullanılan routera bu paketi teslim ediyorsunuz. Default gateway da internet servis sağlayıcınıza bağlı olduğu için ilgili paketin hedefe ulaştırılması bu noktadan sonra onların yönlendirmesine bağlı oluyor. Zaten servis sağlayıcınız da internet ağına bağlı olduğu için ilgili paket internet ağı üzerinden hedefe ulaştırılmış oluyor. 

İleride switch ve router cihazları üzerinde biraz daha durduğumuzda buradaki anlatımlar pekişmiş olacak.
