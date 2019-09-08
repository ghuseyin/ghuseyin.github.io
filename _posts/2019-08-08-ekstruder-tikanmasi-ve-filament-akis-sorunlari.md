Ekstruder Tıkanması ve Filament Akış Sorunları

 Sorunun nerede olabileceğine bakmadan önce bir ekstrüzyon sisteminin nasıl çalıştığına bakarsak sorunu daha kolay çözebiliriz.

* Tipik Bir Ekstrüzyon Sistemi
Tab 1. Motor ve İtiş
Tab 2. Dişli Sistemi
Tab 3. Yay(lar)
Tab 4. Cold End (Soğuk kısım)
Tab 5. Hot End (Sıcak kısım)
* Sorunlar
1. Gevşek Setskur Vida
2. Filament Makarası Sorunları
3. Nozülün Tıkanması
4. Filamentin Kendi Yolunu Kapatarak Tıkanması
5. Yay Gerginlik Ayarı
6. Hot End Vida Bağlantılarından Filament Sızması

## Tipik Bir Ekstrüzyon Sistemi

### 1. Motor ve İtiş
 Genelde motorun miline takılan ve *hobbed gear* denilen bir dişli ve bu dişlinin karşına gelen bir rulman bulunur. Filament bu dişli ve rulman arasına sıkıştırılır. Motor miline bağlı dişlinin dönmesiyle de filament hareket etmiş olur.

Fotoğraf https://reprap.org/forum/thumbcache/944/b40/25a/182/0a0/914/c1f/736/93e/0f8/c9_800x400.png

 Bazı ekstruderlerde hareketi kolaylaştırmak ve hassaslaştırmak için dişli sistemleri ile tork kazancı sağlanır. Bu tür sistemlerde motor miline küçük bir dişli, küçük dişlinin döndürdüğü büyük bir dişli ve büyük dişliye bağlı dişli vida (hobbed bolt) bulunur.

Fotoğraf yeşil dişliler
Fotoğraf hobbed bolt

### 2. Yay(lar)
 Hobbed bolt ve rulman arasına sıkıştırılan filament her zaman aynı genişlikte değildir. Mesela aldığınız filamentin kutusunda 1.75mm yazıyor olabilir ama aynı filamentin bazı yerleri 1.70, bazı yerlerde 1.80 olabilir. Hobbed bolt ve rulman arasındaki mesafenin de buna göre değişebilmesi gerekir. Filament inceldiğinde daralmalı, kalınlaştığında genişlemelidir. Yoksa extrüzyon durur. Bu yüzden rulmanı direk vida ile değil, araya yay ekleyerek tutturulur. Bazı ekstruderlerde 1, bazılarında 2 yay kullanılır.

Fotoğraf yaylar

 Yaylar, filament inceldiğinde rulmanı tutan parçayı iterek rulmanı hobbed bolta yaklaştırır ve boşluk oluşmamasını sağlar.
 Tam tersi durumda, yani filament kalınlaştığında da rulmanın geri gelerek filamentin geçebilmesini sağlar.
 Eğer uygun bir yay bulamadıysanız tükenmez kalem yayı kullanabilirsiniz. Bazı tükenmez kalemlerin yayları kullanılabilir.

Fotoğraf - Tüm extruder monte

### 3. Cold End (Soğuk Kısım)
 Filament itildikten sonra eritilmek için sıcak uca ulaşmadan önce genelde alüminyum olan soğuk bir radyatörden ardında da çelik bir barelden geçer. Buraya kadar filament hâlâ katıdır.

Fotoğraf Sıralı parçalar demonte - üzerlerine isimleri yazılacak
Fotoğraf Tam demonte - yine isim yazılacak

### 4. Hot End (Sıcak Kısım)
 Çelik barelin ucunda ısıtılmış alüminyum bloğa bağlı nozül'e (nozzle) ulaşır ve burada erir. 

## Sorunlar

### 1. Gevşek Setskur Vida
 Ekstruder motorunun miline takılan dişlinin setskur vidası gevşemişse motor mili dönecek ama ona bağlı dişli dönmeyecektir. Eğer dişli, plastikse çok fazla sıkarsanız kırılabilir.

Fotoğraf Setskur

### 2. Filament Makarası Sorunları
 Extruder motoru kolay dönebilen bir makaradan filamenti çekebilir ama filament makarası kolay dönmüyorsa motor filamenti çekemeyecektir.

 Makaranın yeterince kolay dönüp dönmediğini kontrol etmek için filamenti elinizle çekmeyi deneyebilirsiniz. Eğer elinizle zorlamadan çekemiyorsanız motor da çekemeyecektir.

Çok kolay bir işlem değil ama yay gerginliği ile alakalı bir sorununuz varsa anlamınızı sağlayacaktır.

### 3. Nozülün Tıkanması
Nozülün tıkanması filamentle birlikte içeri giren tozdan kaynaklanıyor olabilir. Filamentin temiz ve kuru olduğundan emin olun. Temizlemeniz gerekirse:
**Nozül sıcakken kesinlikle elinizle dokunmayın!**
1. Nozülü 100°C'a ısıtıp yaylı vidaları söküp filamenti çıkarın.
2. Nozülü sıcakken sökün. Soğuduğunda sökülmeyebilir. Hâlâ sökülmüyorsa yazdırma sıcaklığına kadar ısıtabilirsiniz. ( **Sakın elinizle dokunmayın!** )
3. Nozülü söktükten sonra penseyle tutup metal bir şeyle temizleyebilirsiniz. Soğuyan plastik çıkmıyorsa çakmakla da ısıtabilirsiniz.

### 4. Filamentin Kendi Yolunu Kapatarak Tıkanması
 3D yazıcılarda ekstruderin tıkanmasına sebep olan sorunlardan en sık görülenidir. Sıcak alüminyum bloktaki ısı önce çelik barele, ordan da alüminyum radyatöre geçecektir. Bu da alüminyum radyatörün ısınması anlamına gelir. Alüminyum radyatör ısınırsa filament erimesi gereken yerden çok daha geride yumuşayıp şekil değiştirecek ve şekil değiştirdikten sonra katılaşarak yolunu tıkayacaktır. Alüminyum bloğun soğutulması ve PTFE (Teflon) boru kullanılarak filamentin yumuşadığında şekil değiştirmesinin önlenmesi gerekir.

 30x30mm bir fan alüminyum bloğu soğutmak için yeterli olacaktır.

Fotoğraf Fan ve Alüminyum Blok

 Asıl önemli nokta bu fan sadece yazdırma sırasında değil, yazıcı açık olduğu sürece **her zaman** çalışmalıdır. RAMPS üzerinde fanın bağlanması gereken yer:

Fotoğraf RAMPS extruder fanı bağlantısı

Alüminyum radyatörün başlangıcından başlayıp nozülün başlangıcına kadar devam eden bir teflon boru, filamentin yumuşadığında kendini tıkamasını engelleyecektir. Bazı ekstruderlerin yanında gelen, çelik barelden nozüle kadar olan teflon boru yetersizdir. Eğer böyle bir extrudere sahipseniz radyatörün başlangıcından çelik barele kadar bir teflon boru daha eklemeniz gerekir. 

Fotoğraflar Teflon fotoları

### 5. Yay Gerginlik Ayarı
 Yaylar çok gevşekse ekstruder filamenti kavrayamayacak ve itemeyecektir. Eğer çok fazla sıkarsanız da motor hobbed boltu çeviremeyecektir.

Yayların gerginliğini kontrol etmek için:
1. Filamenti çıkartın.
2. Alüminyum radyatörden itibaren filamentin geçeceği bütün parçaları söküp ayırın. (Sökebilmek için ısıtmanız gerekebilir.)
3. Gücü kesin.
4. Extruder motorunun kablosunu çıkartın.
5. Ekstruderi elinizle hızlıca çevirerek filamentin yeterince hareket edip etmediğine bakın.

### 6. Hot End Vida Bağlantılarından Filament Sızması
 Isıtılan alüminyum bloğa bağlı nozül çelik barelin vida dişlerinin arasından erimiş plastik sızabilir. Nozül ve çelik bareli söküp (sökmek için ısıtmak gerekebilir) vida dişlerine tesisatçıların kullandığı PTFE (Teflon) bant sarmak gerekir.
1. Vida dişlerini kir, plastik vb. her şeyden tamamen temizleyin.
2. Teflon bandı biraz gererek **saat yönünde** sarın. Tersi yönde sararsanız vidayı takarken bant sökülecektir.

Fotoğraf Teflon bantlı hotend

Eğer yeterince teflon sardıysanız ve hâlâ filament sızmaya devam ediyorsa nozül tıkanmıştır. 

