Eğer protokol isimleri sebebiyle doğrudan bu sayfayı okumaya başladıysanız, buradaki açıklamaların ağ temellerini ele alan eğitimin bir parçası olduğunu belirtmek isterim. Eğer ağ temellerini öğrenme gayreti içerisindeyseniz bu eğitim serisine baştan sona göz atabilirsiniz.

Söz konusu, verilerin ağ üzerinden iletilmesi olduğunda çeşitli amaçlara hizmet edebilmesi için geliştirilmiş olan özel protokolleri kullanıyoruz. Protokol adı altında belirlenmiş olan kurallar sayesinde karşılıklı olarak aynı protokolleri kullanan tüm yapıların birbiri ile veri alışverişinde bulunması da mümkün oluyor. Biz bu bölümde teknik detaylara girmeden, eğitim içerisinde de yeri geldikçe atıfta bulunduğumuz bazı sık kullanılan protokollerin en genel işlevlerini çok kısaca ele alacağız. 

# ARP - Address Resolution Protocol

ARP protokolü IP adresleri üzerinden MAC adresinin öğrenilmesini mümkün kılan bir protokoldür. Yalnızca IP adresinin bilindiği durumda; hedef IP adresine, kendi MAC adresimiz ve IP adresimizi de barındıran bir MAC sorgusu göndeririz. 

![ARP-step1.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/ARP-step1.webp)

Hedef bu paketi aldığında gönderen host’un IP ve MAC bilgisini kendi ARP tablosuna yazar. Bu sayede daha sonra bu IP adresi ile haberleşmek istediğinde bu IP-MAC eşleşmesini tekrar kullanabilir. Nitekim ARP sorgusuna yanıt olarak da bu bilgileri kullanarak kaynağa kendi IP ve MAC adresini gönderir.

![ARP-step2.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/ARP-step2.webp)

Kaynak aldığı ARP yanıtına bakarak IP ve MAC adresini kendi ARP tablosuna kaydeder.

![ARP-step3.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/ARP-step3.webp)

Bu sayede gördüğünüz gibi karşılıklı olarak iletişim için gereken IP-MAC bilgileri alınmış olur. İşte ARP protokolünün en temel çalışma yapısı bu şekildedir. 

# FTP - File Transfer Protocol

Uygun ağ bağlantısı bulunan taraflar birbiri ile dosya paylaşmak üzere FTP protokolünü kullanabiliyor. Zaten isim kısaltması da Türkçe olarak “Dosya Transfer Protokolü”’dür.

Buradaki örneğimizde istemci durumundaki bilgisayarımız, FTP sunucusuna spesifik bir dosyayı istediğini belirtiyor. FTP sunucusu da yanıt olarak ilgili dosyayı istemciye iletiyor.

![FTP.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/FTP.webp)

FTP sayesinde karşılıklı olarak dosya transferi mümkün. Yani buradaki örneğimizde esasen “client-istemci” durumundaki bilgisayarımız da dilerse FTP sunucusuna dosya yükleyebilir. Yani FTP sunucusuna dosya gönderilmesi mümkündür. 

# SMTP - Simple Mail Transfer Protocol

SMTP, e-posta iletiminde kullanılan bir transfer protokolüdür. Kullanım alanını açıklamak için örnek olarak, **ali@gmail.com** adresinden **can@outlook.com** adresine bir e-posta gönderileceğini düşünelim. Bu durumda Ali'nin e-posta istemcisi, e-posta iletişimini gönderme isteği olarak Ali'nin e-posta sunucusuna (Gmail SMTP sunucusu) iletecektir. 

![SMTP-to-gmail.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/SMTP-to-gmail.webp)

Gmail SMTP sunucusu da, iletiyi alıcının e-posta sunucusuna SMTP üzerinden iletir. 

![gmail-to-outlook.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/gmail-to-outlook.webp)

Alıcının e-posta sunucusu (Outlook SMTP sunucusu), iletiyi alıcı olan Can'ın hesabına teslim alır. Eğer Can e-postayı okumak istiyorsa, e-posta istemcisi (örneğin, Outlook veya başka bir istemci) POP3 veya IMAP gibi protokoller aracılığıyla e-postayı sunucudan alır. 

![POP3-IMAP.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/POP3-IMAP.webp)

Sonuç olarak, e-posta iletimi için SMTP kullanılırken, e-postaların alınması ve yönetimi için POP3 veya IMAP gibi protokoller kullanılır.

![SMTP-POP3-IMAP.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/SMTP-POP3-IMAP.webp)

POP3 protokolü kullanıldığında, sunucudaki mesajlar istemci tarafından alındıktan sonra genellikle sunucudan bu mesajlar silinir. Yani artık bu mesaj istemcide tutulur. 

IMAP protokolü kullanıldığında ise, sunucu ile senkronizasyon sağlanarak her defasında bu mesajın sunucundan talep edilmesi sağlanır. Dolayısıyla mesaj içeriği istemcide değil, sunucuda barındırılır.

Bu protokollerin detayları temel ağ eğitiminin kapsamı dışında, ancak merak ediyorsanız çok kısaca araştırabilirsiniz.

# HTTP - Hyper Text Transfer Protocol

HTTP, esasen bilgisayarlar arasında metin, resim ve video gibi çeşitli verileri iletmek için kullanılan bir protokoldür. Genellikle web tarayıcılarının web sunucularıyla iletişiminde kullanılıyor. Örneğin Chrome gibi bir web tarayıcısını kullanarak bir web sayfasını görüntülemek istediğimizde, bu web sayfasının html dosyasını barındıran web sunucusuna bu sayfayı istediğimizi belirtiriz. 

![HTTP.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/HTTP.webp)

Bu sunucu da olumlu görürse bu html sayfasını bize yanıt olarak iletir. 

![HTTP-response.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/HTTP-response.webp)

Bu sayede web sayfasının içeriğini kendi web tarayıcımızda görüntüleyebiliriz. 

![HTTP-Webpage.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/HTTP-Webpage.webp)

Benzer yaklaşım diğer çeşitli veri türlerinin iletimi için de aynen geçerli. Neticede web sayfalarının tüm içeriklerinin bize ulaşmasını sağlayan bu protokoldür. 

# SSL - TLS

Client ve server arasında şifreli veri iletimini mümkün kılan protokollerdir. Örneğin HTTP protokolü normalde tüm verileri okunabilir şekilde ağ üzerinde iletir. Bu durumda ağın herhangi bir noktasındaki gözlemci bu iletinin içeriğini okuyabilir. 

![HTTP-security.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/HTTP-security.webp)

Fakat bu iletiyi **SSL** veya **TLS** ile şifrelediğimizde HTTP protokolü **HTTPS** halini alır ve mesaj içeriği gözlemciler tarafından okunamaz.

![HTTPS.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/HTTPS.webp)

Yalnızca uygun anahtarı bulunan alıcı bu mesajı okuyabilir. 

![HTTPS-key.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/HTTPS-key.webp)

![HTTPS-read.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/HTTPS-read.webp)

Benzer şekilde sunucu da yanıtını yine HTTPS üzerinden şifreli şekilde iletir. 

![HTTPS-response.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/HTTPS-response.webp)

Bu sayede veri alışverişi karşılıklı olarak şifreli şekilde gerçekleştirilmiş olur. Bu yaklaşımda taraflar harici hiç kimse bu iletilen verileri okuyamaz. Yani gördüğünüz gibi TLS şifrelemesi protokole güvenlik katmak için kullanılabiliyor. 

Ben örnek olması için HTTP protokolü ele aldım ancak diğer pek çok protokolün güvenliği için de SSL-TLS şifrelemesinden faydalanılıyor. Örneğin FTP protokolünde dosya alışverişini şifreli şekilde gerçekleştirmek üzere **TLS** şifrelemesi gerçekleştirilebiliyor ve bu protokole de **FTPS**(FTP Secure) deniyor.

Ayrıca açıklamalar sırasında SSL-TLS şeklinde ifade ettim ancak günümüzde daha gelişmiş ve güvenli versiyon olduğu için TLS kullanıyor. Örneğin bir web sayfasını ziyaret ettiğinizde “bu web sayfası güvenli değil” gibi bir uyarı alıyorsanız, muhtemelen o sayfanın TLS sertifikası bulunmadığı veya artık geçersiz olduğu için şifreli iletişim kurulamadığından web tarayıcınız size uyarı veriyordur. 

![cert-date-invalid-error.jpg](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/cert-date-invalid-error.jpg)

# SSH - Secure Shell | Telnet

SSH, güvenli bir şekilde uzak sunuculara erişim sağlamak için kullanılan bir ağ protokolüdür. SSH sayesinde fiziksel olarak uzakta bulunan bir sunucuda oturum açıp sunucuyu yönetmek üzere, bulunduğumuz ağ ile sunucu arasında güvenli bir iletişim kanalı oluşturabiliyoruz. 

![SSH.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/SSH.webp)

SSH ile sağlanan bağlantıda tüm trafik şifreli şekilde yalnızca ilgili tarafların okuyabileceği formda taşınır. Dolayısıyla SSH trafiği güvenlidir. Bu sayede herhangi bir sunucuya herhangi bir cihazdan güvenli şekilde bağlanıp, sunucuyu yönetebiliriz. Örneğin ben web sunucumu yönetmek için telefonumdan SSH bağlantısı yapıp sunucumda oturum açabilirim. Telefonum ve web sunucum internete bağlı olduğu sürece dünyanın herhangi bir yerinde, herhangi bir ağ üzerinden bu bağlantıyı güvenle kurabilirim. 

SSH sayesinde bağlantı kuran taraflar arasında her türlü veri transferi gerçekleştirilebiliyor. Örneğin FTP protokolü yerine dosyaları güvenli şekilde SSH bağlantısı ile aktarmamızı sağlayan SFTP isimli bir protokol vardır. Bu protokol FTP trafiğini SSH protokolü sayesinde şifreleyerek güvenli dosya transferini mümkün kılar.

Esasen güvenli bağlantıya ihtiyaç duyulan pek çok alanda SSH protokolü kullanılıyor. Dolayısıyla pek çok farklı protokol ile birlikte kullanıldığına da şahit olabilirsiniz.

SSH, hem kullanıcı adı/parola kombinasyonları hem de anahtar tabanlı kimlik doğrulama gibi yöntemlerle istemci cihazların sunucuya güvenli bir şekilde kimlik doğrulamasını sağlıyor. Dolayısıyla doğru şekilde konfigüre edildiği sürece son derece güvenli bir kanaldır.

SSH haricinde, benzer görev için geliştirilmiş olan ama şifreleyerek güvenli taşıma kanalı sunmayan “**Telnet**” isimli daha eski bir protokol de mevcut. Fakat Telnet, SSH’ın sunduğu güvenlik çözümlerini sunmadığı için günümüzde Telnet yerine SSH kullanılmakta. 

# DNS - Domain Name System

Daha önce eğitim içerisinde kısaca izah ettiğimiz gibi, “server” yani “sunucu” olarak isimlendirdiğimiz cihazların aslında içerisinde gerekli hizmeti sunabilecek yazılımlar kurulu sıradan bilgisayarlar olduğunu biliyorsunuz. Örneğin HTTP isteklerine yanıt vermek için gereken yazılımları bir bilgisayara kurup bu bilgisayarı websitemizi sunması için internete açtığımızda, websitemizi ziyaret etmek isteyen istemciler bu bilgisayara HTTP isteği gönderiyor olacaklar. Bu durumda websitesinin dosyalarını isteyen taraf client iken, bu dosyaları HTTP vasıtası ile istemcilere ileten ise server yani sunucu olacaktır.

![client-server.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/client-server.webp)

Dolayısıyla aslında sunucular da IP adresine sahip olan birer host cihazlarıdır. Host cihazlarının birbiri ile iletişim kurmak için IP adreslerini kullandığını da biliyoruz. Bu sebeple **sunucular ile iletişim kurmak istediğimizde bu sunucuların IP adresini bilmek zorundayız**. 

Fakat IP adreslerini akılda tutması kolay değil. Örneğin **linuxdersleri.net** websitesine erişmek için **185.199.108.153** IP adresini akılda tutmak ve her defasında eksiksiz olarak yazmak oldukça zahmetli. Kaldı ki tüm internet yalnızca tek bir websitesinden ibaret olmadığı için tüm websitelerinin IP adreslerini hatırlamamız ve eksiksiz olarak yazmamız pek olası değil.

Zaten bizler de bu sebeple domain olarak geçen alan isimlerini kullanıyoruz. Örneğin linuxdersleri.net websitesini ziyaret etmek için yalnızca bu ismi tarayıcımıza yazıp onaylamamız yeterli oluyor. Bu domain ismi arka planda, IP adresine dönüştürülerek bizim doğru sunucu ile iletişim kurmamız da mümkün oluyor. 

Hostlar arasında iletişim kurmak için IP adreslerinin bilinmesi gerektiğinden, bir sunucu ile iletişim kurmak istediğimizde bu sunucun IP adresini bilmek zorundayız. İşte burada dönüşümü gerçekleştiren yapı da **DNS** olarak geçen protokoldür. 

IP ve domain bilgileri DNS server üzerinde tutuluyor. Biz de domain adresi üzerinden gerekli olan IP bilgisini almak için bu DNS sunucusuna başvuruyoruz. 

Eğer harici olarak bir konfigürasyon gerçekleştirmediyseniz bu DNS sunucusu sizin internet servis sağlayıcınızdır. Örneğin Google’ın DNS sunucusu olan 8.8.8.8 sunucusunu kullandığınızı varsayacak olursak sorgulama işlemi aşağıdaki gibi gerçekleşir.

![DNS.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/DNS.webp)

Yani DNS aslında internet dünyası için son derece önemli bir protokoldür. Örneğin internet servis sağlayıcınız sizin bazı sitelere erişmenize engel olmak isterse, kendi DNS sunucuları üzerinde bu domain adreslerinin karşılığı olan IP adreslerini geçersiz olarak tanımlayabilirler. Genellikle hostun kendi lokal IP adresi olan 127.0.0.1 adresi tanımlanır. Bu sayede gitmek istediğiniz domain’in IP adresi bulunamadığı için ilgili web sunucusu ile iletişim kuramazsınız. 

![DNS-block.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/DNS-block.webp)

Bu sebeple sıklıkla Google Cloudflare gibi DNS hizmeti sağlayan harici DNS sunucuları kullanılır.

Ayrıca, harici DNS sunucuları dışında kullanmakta olduğunuz cihazın işletim sistemi içerisinde de dahili DNS hizmeti bulunur. Bu sayede cihazdaki programların hangi sunuculara erişip hangilerine erişmeyeceğini cihaz bazında kısıtlamamız da mümkün oluyor. 

Windows Hosts Dosyası: ***C:\Windows\System32\drivers\etc/hosts***

Linux Hosts Dosyası: ***/etc/hosts***

Esasen DNS konusu çok daha fazla detayı barındırıyor olmasına karşın en temel amacı burada izah ettiğimiz gibidir. Daha fazlası için kısa bir ek araştırma yapabilirsiniz.

# DHCP - Dynamic Host Configuration Protocol

İnternet bağlantısı için her hostun 4 bilgiye ihtiyacı var. Bunlar:

- IP adresi
- Subnet Mask değeri
- Default Getway bilgisi
- DNS Server IP adresi

Şimdi sırasıyla neden bu 4 bilgiye ihtiyaç olduğunu kısaca izah edelim.

IP adresi hostların ağ üzerindeki kimliğidir. IP adresi olmadan hostların birbirinden ayırt edilmesi mümkün olmaz.

![IP.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/IP.webp)

Subnet mask değeri, hostun hangi ağda olduğunu ve ağın büyüklüğünün bilgisini verir. Bu sayede hangi IP adreslerinin lokal ağda, hangilerinin harici ağlarda olduğu bilinebilir.  

![Subnet-mask.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/Subnet-mask.webp)

Yani IP ve subnet mask değerine sahip olan tüm hostlar lokal ağda iletişim kurabilirler. Fakat bir host harici bir ağdaki hostla iletişim kurmak istiyorsa, verileri harici hosta yönlendirecek router cihazının IP adresini de bilmesi gerekiyor. Örneğin bizim internet ağına bağlanmamızı sağlayan evimizdeki router görevini gören “modem” cihazıdır. Biz modeme bağlanırız bu modem de bizi internete bağlar. Bizi dış ağa bağlayan router cihazı da “ağ geçidi” yani “getway” olarak ifade ediliyor. Zaten yukarıdaki görsele bakacak olursanız router cihazının bizi dış ağa bağlandığını kendiniz de görebilirsiniz. Bu sebeple bir hostun harici ağlar ile iletişim kurmak için, varsayılan ağ geçicinin(default getway) IP adresini de bilinmesi gerekiyor. 

![default-getway.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/default-getway.webp)

Bu bilgiler internet ağına bağlanıp IP adresleri üzerinden diğer hostlar ile iletişim kurmamızı sağlar. 

Eğer alan adı yani “domain” ismi üzerinden bir adresi ziyaret etmek istiyorsak bu noktada domain adresini IP adresine dönüştürecek olan DNS sunucusuna da ihtiyacımız var. Dolayısıyla bir hostun domain isimleri üzerinden webte gezinebilmesi için DNS sunucusunun IP adresini bilmesi gerekiyor. 

![DNS-network.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/DNS-network.webp)

İşte tüm bu sebeplerle bir hostun internet üzerinde gezinebilmek için “IP, Subnet Mask, Default Getway, DNS” bilgilerine sahip olması gerekiyor. Bu hostun ne tür bir cihaz olduğu önemsiz. Burada bahsi geçen host; laptop, telefon, yazıcı veya internete bağlanabilen herhangi bir cihaz olabilir. Hepsinin bu 4 bilgiye ihtiyacı var.

Fakat muhtemelen ben özellikle ele alana kadar internet gezintisi için bu 4 bilgiye ihtiyacınız olduğunun bile farkında değildiniz. Bu durumun sebebi bu bilgilerin **DHCP** isimli protokol tarafından hostlara otomatik olarak tanımlanıyor olmasıdır. 

DHCP sunucusu olarak görev yapan sunucu, ağa katılan tüm hostlara bu bilgileri uygun şekilde tanımlama görevindedir. Bir cihaz ağa yeni katıldığında, ağın DHCP sunucusuna keşif mesajı gönderir.

![DHCP-discover.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/DHCP-discover.webp)

DHCP sunucusu da yanıt olarak uygun olan bilgileri bu cihaza tanımlayarak ağa katılmasını sağlar.

![DHCP-offer.webp](https://raw.githubusercontent.com/taylanbildik/network-temelleri/main/protokoller/DHCP-offer.webp)

DHCP sayesinde gerekli olan temel bilgiler otomatik olarak atanıyor. DHCP görevini de, genellikle ev veya küçük işletme ağlarında modem ya da router cihazı üstleniyor. 

Böylelikle sık kullanılan temel birkaç protokolden çok kısaca bahsetmiş olduk. Elbette her bir protokolün çok daha fazla detayı bulunuyor olmasına karşın ağın çalışma yapısını temel düzeyde anlamak için gereken bilgiye artık sahip olduğumuzu düşünüyorum. Eğer yalnızca bu yazıyı okuduysanız belki anlatımlar sizin için yeterince anlaşılır gelmemiş olabilir. Bu durumun nedeni tüm eğitimin ağ temellerini açıklamak üzere sırasıyla bölüm bölüm ele alınması. Bu bölümde anlatılanları ve ağ temellerini daha iyi anlamak için tüm eğitim serisine baştan sona göz atmanızı tavsiye edebilirim.
