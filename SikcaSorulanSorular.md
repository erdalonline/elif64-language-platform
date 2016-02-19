## Temel Yapı ##

  1. Sadece Linux işletim sistemi desteklenecek.
  1. Sadece 64-bit PC mimarisi (yani x86\_64) desteklenecek.
  1. Elif64 derlenen bir dildir. Sadece Linux Kernel API'sine ihtiyaç duyacak. GNU libc kütüphanesine veya herhangi bir altyapıya ihtiyaç duymayacak.
  1. Dinamik bellek yönetimi dahili heap-manager tarafından sağlanacak. İstenen belleğin geri verilmesi işlemi ile çöp toplayıcı(GC) ilgilenecek. Böylece programcı bellek kaçakları ile uğraşmak zorunda kalmayacak.
  1. Programcı tarafında çok yüksek seviyeli Elif64 programlama dili kullanılacak.
  1. Dilin temel kütüphanesi tam optimize edilmiş olarak %100 el yapımı 64-bit Assembly ile yazılacak.
  1. Çalıştırılabilir dosya, Elif64'ün x86\_64 Assembly diline yorumlanması ve temel kütüphane ile birleştirilmesi sonrasında oluşan Assembly kodunun Nasm(The Netwide Assembler) ile derlenmesi sonucunda elde edilecek.
  1. Çok büyük ve çok küçük belleği olan PC'leri destekleyecek.
  1. Birden fazla işlemciye destek veren özelliklerle birlikte gelecek.
  1. Elif64 dili için renklendirme, tamamlama gibi özelliklere sahip bütünleşik yazılım geliştirme ortamı (IDE) yazılacak.


## Projenin Çıkış Noktaları ##
  1. Derleyicilerin kötü kod üretmesi.
  1. 64-bit PC sahibi iken hala 32-bit uygulamaları kullanmak zorunda kalmak.
  1. 64-bit derlenmiş uygulamaların 64-bit için optimize çalışmamaları.
  1. Yüksek seviyeli bir dil ve zengin kütüphanesi için bilgisayara framework kurmak zorunda kalmak.
  1. Yüksek seviyeli bir dil ve zengin kütüphanesi için nesne yönelimli programlamanın programcıya dayatılması.
  1. Düşük seviyeli dillerin güçlü editörlere, gelişmiş bazı özelliklere sahip olmamaları ve standart kütüphanelerinin küçük olması.


## Üstün Tarafları ##
  1. %100 el yapımı, x86\_64 Assembly ile en iyi şekilde yazılmış kütüphaneye sahip olması, mimarinin kapasitesini sonuna kadar kullanabilmesi.
  1. Daha hızlı ve daha küçük kod üretilmesinin mümkün olmaması.
  1. Çalıştığı mimariye göre içine dahil edilmiş gereksiz kodları temizlemesi. (Intel/AMD optimizasyonları, 3DNow!/SSE destekleri)
  1. Elif64 programlama dili hem düşük seviyeli dillerin hem de yüksek seviyeli dillerin yazım özelliklerine sahip olacak. Bunun yanında kod yazmayı kolaylaştıran/basitleştiren tekniklere ve çok yüksek seviyeli fonksiyonlara sahip olacak. Bir işi yapmanın birden çok yolu olacak, böylece programcı istediği yerde ayrıntıya girip hakimiyeti eline alabilecek.
  1. Pek çok optimizasyon zamanı geldiğinde uygulanacak. (Fonksiyon geçişlerinde gereksiz yere belleğin kullanılması yerine verimli şekilde registerların kullanımı(ABI uyumsuz iç yapı), bellek yönetimine müdahele edilebilmesi, vs)
  1. Diğer programlama dillerinde gerçekleştirilmesi zor olan birçok özelliğe(crack koruması, uzaktaki makinaya kod yollama, vs) gelecekte destek verebilecek olması.


## Zayıf Tarafları ##
  1. Linux dışında diğer işletim sistemleri desteklenmemektedir.
  1. 32bit eski işlemciler desteklenmemektedir.
  1. PC mimarisi dışındaki mimariler desteklenmemektedir.
  1. Diğer uygulamalar ve kütüphanelerle nasıl ortak çalışılacağı henüz tasarlanmamıştır.
  1. Projenin hayata geçmesi uzun yıllar alacaktır.


## Karara Bağlanmamış veya Belirsiz Olan Kısımlar ##
  1. Nesne yönelimli programlama desteği. (olsun?/olmasın?)
  1. Sistem programlama desteği. (olsun?/olmasın?)
  1. heap-manager yerleşimi. (gömülü?/ayrı?)
  1. Diğer uygulamalar ve kütüphanelerle ortak çalışma. (!henüz tasarlanmadı!)


## Hedefler ##
  1. Zevk aldığım konularla(Assembly ve Linux) ilgilenerek bu konudaki bilgi ve deneyimimi artırmak.
  1. Assembly konusunda Türkçe dökümantasyon oluşturmak.
  1. Güçlü bir dil tasarlayarak bu konudaki bilgi ve deneyimimi artırmak, dökümantasyon oluşturmak.
  1. Proje tamamlandığında güçlü, verimli, hızlı, esnek bir yazılım geliştirme platformuna sahip olmak, elimdekileri diğer insanlarla paylaşmak ve bu platformla yazılım geliştirmek.