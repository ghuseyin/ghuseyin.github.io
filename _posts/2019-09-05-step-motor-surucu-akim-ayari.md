---
layout: post
title: Step Motor Sürücü Akım Ayarı ve Isınma Sorunu
date: 2019-09-05 13:14:15
description: A4988 ve DRV8825 step motor sürücülerinin akım ayarını yaparak 3D yazıcının step motorlarının aşırı ısınma ve adım kaçırma sorununu çözeceğiz...
img: a4988-drv8825.jpg
tags: [A4988, DRV8825, elektronik, 3D]
---

Bu yazıda *A4988* ve *DRV8825* step motor sürücülerinin akım sınırlama ayarını yaparak 3D yazıcının step motorlarının aşırı ısınmaya bağlı adım kaçırma sorununu çözeceğiz. Bu işlem için bir avometreye veya voltmetreye ihtiyacımız olacak.

Sırasıyla yapacaklarımız:
1. Step Motor Sürücümüzü Tanıyalım
	* Pololu A4988
	* Çin malı A4988
	* DRV8825
2. Step Motorumuzu Tanıyalım
3. Vref Değerinin Hesaplanması
	* A4988 için Vref
	* DRV8825 için Vref
4. Ayar
5. Test 

Başlamadan önce bir uyarı:
> Motor sürücü kartının gücünü kesmeden kesinlikle motorun kablosunu çıkarmayın, takmayın!

## 1. Step Motor Sürücümüzü Tanıyalım

Step motor sürücümüzü ayarlayabilmemiz için ilk olarak sürücümüzün *Rcs* değerini kesinlikle tam olarak bilmemiz gerekiyor. Bu değeri nasıl öğrenebileceğimize bakalım. 

### Pololu A4988 Step Motor Sürücü Kartı
Pololu marka bir A4988'e sahipseniz görünüşü şöyledir:
![Pololu A4988 Step Motor Sürücü Kartı](https://a.pololu-files.com/picture/0J10065.180.jpg?b63f11341129426340f57ab54e30c6fb)

Rcs değerini bu fotoğrafa bakarak öğrenebilirsiniz.
![Pololu A4988 Rcs]({{site.baseurl}}/assets/img/pololu-rcs.jpg)

Rcs değerinizi öğrendiyseniz bunu not alın ve bir sonraki kısma geçin. Eğer step motor sürücünüzün A4988 olduğuna eminseniz ama fotoğraftakilerin ikisi de değilse muhtemelen Çin malı A4988'e sahipsiniz. Şimdi onlara bakalım.

### Çin Malı A4988 Step Motor Sürücü Kartı
Genelde kırmızı veya yeşil PCB'ye sahiptirler. Farklı Rsc değerlerine sahip modelleri var. 
![Kırmızı PCB A4988 Step Motor Sürücü](https://reprap.org/mediawiki/images/thumb/f/f5/StepStick_china_red_front.jpg/204px-StepStick_china_red_front.jpg)
![Yeşil PCB A4988 Step Motor Sürücü](https://reprap.org/mediawiki/images/thumb/9/9c/Inexpensive_stepper_driver_board_a4988_1a.jpg/212px-Inexpensive_stepper_driver_board_a4988_1a.jpg)

Renginin Rsc değeri ile bir alakası yok, bu sizi şaşırtmasın. Rsc değerini öğrenmek için entegrenin hemen yanındaki dirençlere bakmamız gerekiyor. Bu dirençler bazı modellerde S1 S2 gibi veya R4 R5 gibi yazılarla işaretleniyor. Kart üzerinde göstermek gerekirse bu fotoğrafta S1 ve S2 ile gösterilmiş:
![A4988 Rsc Direnç S1 S2](https://reprap.org/mediawiki/images/thumb/3/31/A4988_detail_current_sense_r_1a.jpg/320px-A4988_detail_current_sense_r_1a.jpg)

Bu fotoğrafta ise R5 ve R5 ile:
![A4988 Rsc Direnç R4 R5]({{site.baseurl}}/assets/img/A4988_step_motor_surucu.jpg)

İlk fotoğrafta R100, ikincide R10 olarak görünen dirençler sizde farklı olabilir. Eğer sizde 
* R100 veya R10 ise Rsc değeriniz 0.1 Ohm'dur.
* R200 veya R20 ise Rsc değeriniz 0.2 Ohm'dur.
* R050 veya R05 ise Rsc değeriniz 0.05 Ohm'dur.
* R068 ise Rsc değeriniz 0.068 Ohm'dur.

Eğer farklı bir değer yazıyorsa doğru dirence baktığınızdan emin olun. Eğer eminseniz küçük bir araştırmayla direncin üzerindeki yazının değer karşılığını bulabilirsiniz ama muhtemelen hâlâ yanlış dirence bakıyorsunuz.

### DRV8825 Step Motor Sürücü Kartı
Pololu üretimi DRV8825 step motor sürücü kartı bu şekilde görünür:
![Pololu DRV8825 Step Motor Sürücü](https://a.pololu-files.com/picture/0J4227.250.jpg?7479185b591b5fa757c5687a5ee3b7d2)

Çin malı olanları da mor PCB'ye sahip. Standart DRV8825 kartların Rsc değeri 0.1 Ohm'dur. Standart olduğu için DRV8825 kullanacaksanız bu değeri not almanıza gerek yok.

## 2. Step Motorumuzu Tanıyalım

Kullanmak istediğiniz step motorun özelliklerini bilmeniz gerekiyor. Model numarası ile birlikte aratıp kullanmanız gereken akım ve gerilim değerlerine ulaşabilirsiniz. 3D yazıcıların X, Y ve Z eksenlerinde kullanılan NEMA17 step motorlar 12Volt gerilimde genelde 0.7-0.8 Amper akıma ayarlanırlar.

## 3. Vref Değerinin Hesaplanması

Avometreyi 20V DC voltaj ölçme konumuna alıp "+" kablosunu step motor sürücünün ayar potuna, "-" kablosunu GND pinine değdirdiğimizde ölçmemiz gereken değere *Vref* değeri diyoruz. (Henüz bunu yapmayın.)

### A4988 için Vref
Vref değerini A4988 için şu şekilde hesaplayabiliriz:
> Vref = 8 x Akım x Rcs

Örneğin A4988 kullanıyorsak, akımı 0.7 Amper olarak ayarlayacaksak ve Rcs değerimiz 0.2 Ohm ise denklemimiz şöyle olacaktır: 
> Vref = 8 x 0.7 x 0.2
> Vref = 1.12
Ayarlamak istediğimiz akım yine 0.7 Amper ama Rcs değerimiz 0.05 Ohm ise denklemimiz şöyle olur:
> Vref = 8 x 0.7 x 0.05
> Vref = 0.28

Gördüğünüz gibi aynı akıma ayarlamamıza rağmen Rcs değerinden dolayı Vref değeri 4 kat değişti. İşte bu yüzden A4988 kullananlar için Rcs değerini bilmek çok önemli. Eğer Rcs değerinizi bilmiyorsanız lütfen 1. kısma geri dönün.

### DRV8825 için Vref
Vref değeri DRV8825 için şu şekilde hesaplanır:
> Vref = Akım / 2
Örneğin 0.7 Amper akıma ayarlayacaksak Vref değerimiz:
> Vref = 0.7 / 2
> Vref = 0.35

## 4. Ayar

**Step motor sürücüler elektriğe bağlıyken step motorun kablolarını kesinlikle çıkarmayın veya takmayın.**
**Önce step motor sürücünün gücünü kesin ve step motorun kablolarını ayırın.**
**Ayar sırasında step motorlar, sürücüye bağlı olmamalı.**

Gücü kesip step motorun kablolarını sürücüden ayırdıktan sonra sürücüye yeniden güç vermemiz gerekiyor. Son durumda motorlar sürücüye bağlı değil ve sürücü çalışır durumda olmalı.

Son olarak GND pinini de bilmemiz gerekiyor. GND pini A4988 step motor sürücü kartlarında şekildeki gibidir:


DRV8825 için GND pini:


> Farklı model kartların GND pinleri farklı yerlerdedir. Her kartın altında veya üstünde GND pini yazıyla da belirtilmiş olmalı. Emin olmak için kartınızdaki yazıyı kontrol edin. **Eğer yanlış yere değdirirseniz sürücü yanacaktır.**
 
![GND Pini](https://reprap.org/mediawiki/images/thumb/f/f3/Stepper_drivers_a4988_drv8825_4a.jpg/320px-Stepper_drivers_a4988_drv8825_4a.jpg)

![Step Motor Sürücü Akım Ayarı]({{site.baseurl}}/assets/img/StepSurucuAkimAyari.jpg)

Avometreyi 20V DC voltaj ölçme konumuna alıp "+" ucunu motor sürücünün ayar potuna, "-" ucunu da GND pinlerinden birine değdirmemiz gerekiyor. Bunu yaparken birinden yardım almanızda fayda var. Avometredeki değere bakarken eliniz biraz kayarsa kablo yanlış pine değecek ve sürücü büyük ihtimalle yanacaktır. Kabloları tutan kişi gözünü sürücüden ayırmadan kabloları tutarken başka biri avometrede görünen değeri okursa muhtemel bir kazanın önüne geçilmiş olur.

Eğer okuduğunuz değer ayarlamak istediğiniz Vref değerinden farklıysa ayar potunu ince, yalıtılmış bir tornavidayla çok çok az çevirdikten sonra yeniden ölçün. 

> Değeri arttırmak-azaltmak için çevirme yönü karta göre değişir. En iyisi deneyerek arttırma-azaltma yönünü bulmak.

Ayar potları çok hassas olduğu için istediğiniz değere ayarlamanız zor olabilir ama bunu yapmalısınız.

İstediğiniz değere ayarladıktan sonra kartın gücünü kesip step motorları bağlayabilirsiniz.

## 5. Test

Step motorları yeniden sürücüye bağladıktan sonra karta güç verebilirsiniz. Kullanmadan önce step motor sürücünüzün üzerine alüminyum soğutucu blok yerleştirmeniz ve fan ile aktif soğutma yapmanız önerilir. Aksi hâlde sürücülerinizin aşırı ısınıp adım kaçırması ve buna bağlı olarak eksen kayması yaşamanız muhtemeldir.

![RAMPS Soğutma]({{site.baseurl}}/assets/img/RAMPS_Sogutma.jpg =250x)

Çalışma sırasında da step motorların sıcaklığını kontrol etmelisiniz. Elinizi yakacak kadar ısınıyor ve adım kaçırma devam ediyorsa yaptıklarınızı gözden geçirmeli ve akımı biraz daha kısmalısınız. Eğer motor serin çalışıyor ve adım kaçırıyorsa muhtemelen akımı fazla kısmışsınızdır.

Yazdırma hızınız yüksek değilse (RepRap 3D yazıcılarda genelde 60mm/sn kullanılır) motorun miline bağlı kasnağın vidası gevşemiş olabilir. Kayışın da yeterince gergin olduğuna emin olun. Step motorun kablosunu çıkardığınızda ekseni elinizle rahatlıkla hareket ettirebiliyor olmalısınız. Eğer ettiremiyorsanız millerin paralelliğini kontrol edin. 

Eksen kayması devam ediyorsa kullandığınız yazılımdan ivme ve *jerk* değerlerini düşürmeniz gerekiyor olabilir. Özellikle Z ekseninde bu değerleri yarıya indirmekten çekinmeyin.

Bütün bunlara rağmen eksen kayması yaşıyorsanız kayma yaşadığınız eksenin motor ve sürücüsünü kayma yaşamadığınız bir ekseninkiyle değiştirip sorunun diğer eksene geçip geçmediğine bakabilirsiniz. Eğer geçtiyse sorun diğer eksene taşıdığınız parçalardadır, geçmediyse muhtemelen mekanik veya yazılımsaldır.

## Kaynakça

> https://reprap.com/wiki/A4988

> https://reprap.com/wiki/DRV8825

> https://reprap.org/wiki/A4988_vs_DRV8825_Chinese_Stepper_Driver_Boards

> https://www.pololu.com/product/1182

> https://www.pololu.com/product/2133
