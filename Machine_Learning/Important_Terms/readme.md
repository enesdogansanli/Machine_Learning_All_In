# Important Terms In Machine Learning

## İçerik
- [Important Terms In Machine Learning](#important-terms-in-machine-learning)
  - [İçerik](#i̇çerik)
  - [Machine Learning Model](#machine-learning-model)
  - [Overfitting](#overfitting)
  - [Underfitting](#underfitting)
  - [Varyans-Bias](#varyans-bias)
  - [Regularization (Düzenlileştirme)](#regularization-düzenlileştirme)
    - [Lasso Regularization](#lasso-regularization)
    - [Ridge Regurlarization](#ridge-regurlarization)
    - [Elasticnet](#elasticnet)
  - [Referanslar](#referanslar)

## Machine Learning Model

Makine öğrenmesi uygulamalarında temel amaç eldeki veriler üzerinden örüntüler elde etmek ve yeni veriler için bu örüntüler üzerinden doğru tahminler yapabilmektir. Bu tahminleri yapabilmek için makine öğrenmesi uygulamaları sonucunda bir model elde ederiz. Model girdilerin çıktılara eşlenmesi için kullanılan bir sistemdir. Örneğin amacımız ev fiyatlarını tahmin etmek olsun . Bunun için evin metrekare bilgisini girdi olarak kullanan bir model oluştururuz ve çıktı olarak da evin fiyatını elde ederiz.

Makine öğreniminde gelecek veriler hakkında tahmin yapabilmek için verilerimizi eğitim verileri (train) ve test verileri olmak üzere iki alt kümeye ayırıyoruz. Modelimizi eğitim verilerinden elde edilen örüntülere göre oluşturuyoruz. Bu işlem sonucunda iki şeyden biri olabilir; modelimiz aşırı öğrenebilir veya eksik öğrenebilir. Bu durumda modelimiz yeterli öngörüde bulunamayacak ve tahminlerimizde hata oranı yüksek 
olacaktır.

## Overfitting

Eğer modelimiz, eğitim için kullandığımız veri setimiz üzerinde gereğinden fazla çalışıp ezber yapmaya başlamışsa ya da eğitim setimiz tek düze ise overfitting olma riski büyük demektir. Eğitim setinde yüksek bir skor aldığımız bu modele, test verimizi gösterdiğimizde muhtemelen çok düşük bir skor elde edeceğiz. Çünkü model eğitim setindeki durumları ezberlemiştir ve test veri setinde bu durumları aramaktadır. En ufak bir değişiklikte ezberlenen durumlar bulunamayacağı için test veri setinde çok kötü tahmin skorları elde edebilirsiniz. **Overfitting problemi olan modellerde yüksek varyans, düşük bias durumu görülmektedir.**

Overfitting problemi aşağıdaki yöntemler uygulanarak çözülebilmektedir;

* Öz nitelik sayısını azaltmak: Birbirleriyle yüksek korelasyonlu olan kolonlar silinebilir ya da faktör analizi gibi yöntemlerle bu değişkenlerden tek bir değişken oluşturulabilir.
* Daha fazla veri eklemek : Eğer eğitim seti tek düze ise daha fazla veri ekleyerek veri çeşitliliği arttırılır.
* Regularization (Düzenleme) : Düzenleme, modelin karmaşıklığını azaltmak için bir kullanılan tekniktir. Bunu kayıp fonksiyonunu cezalandırarak yapar. Yani modelde ağırlığı yüksek olan değişkenlerin ağırlığını azaltarak bu değişkenlerin etki oranını azaltır. Bu yöntem, aşırı öğrenme probleminin çözülmesine yardımcı olur. Kayıp fonksiyonu, gerçek değer ile öngörülen değer arasındaki farkın karelerinin toplamıdır. Değişkenlerin ağırlığını azaltmak için regularization değerini arttırmak gerekmektedir. En popüler Regularization metotları **Lasso** ve **Ridge** teknikleridir.

## Underfitting

Aşırı öğrenmenin aksine, bir model yetersiz öğrenmeye sahipse, modelin eğitim verilerine uymadığı ve bu nedenle verilerdeki trendleri kaçırdığı anlamına gelir. Ayrıca modelin yeni veriler için genelleştirilemediği anlamına da gelir. Tahmin ettiğiniz gibi bu problem genellikle çok basit bir modelin sonucudur (yetersiz tahminleyici bağımsız değişken eksikliği).

Underfitting sorunu olan modellerde hem eğitim hem de test veri setinde hata oranı yüksektir. **Düşük varyans ve yüksek bias’a sahiptir.** Bu modeller eğitim verilerini çok yakından takip etmek yerine, eğitim verilerinden alınan dersleri yok sayar ve girdiler ile çıktılar arasındaki temel ilişkiyi öğrenemez.

## Varyans-Bias

Varyans, model eğitim veri setinde iyi performans gösterdiğinde, ancak bir test veri kümesi veya doğrulama veri kümesi gibi, eğitilmemiş bir veri kümesinde iyi performans göstermediğinde ortaya çıkar. Varyans, gerçek değerden tahmin edilen değerin ne kadar dağınık olduğunu söyler.

Bias, gerçek değerlerden tahmin edilen değerlerin ne kadar uzak olduğudur. Tahmin edilen değerler gerçek değerlerden uzaksa, bias yüksektir.

* Yüksek Bias Düşük Varyans: Modeller tutarlıdır, ancak ortalama hata oranı yüksektir. (Underfitting)
* Yüksek Bias Yüksek Varyans : Modeller hem hatalı hem de tutarsızdır .
* Düşük Bias Yüksek Varyans: Modeller bir dereceye kadar doğrudur ancak ortalamada tutarsızdır. Veri setinde ufak bir değişiklik yapıldığında büyük hata oranına neden olmaktadır. (Overfitting)
* Düşük Bias Düşük Varyans: Modeller ortalama olarak doğru ve tutarlıdır. Modellerimizde bu sonucu elde etmek için çabalamaktayız.

![](photo/1.PNG)

> Temel olarak bias dediğimiz şey train hatasını ifade ediyor. Train hatası ne kadar yüksek ise bias değerimiz o kadar yüksek demektir. Bu da underfitting yani modelin veri setini öğrenmediğini ifade ediyor.

> Varyansı anlamak içinse train hatası ve test hatasını bakmak yerinde olacaktır. Train hatası ve test hatası arasındaki fark bize varyansı verecektir. Varyans değeri yüksek ise model yeni bir veri gördüğü zaman başarı gösteremiyor demektir. Bu da bize modelimizin overfitting olduğunu gösterir.

![](photo/2.jpg)

![](photo/3.png)

## Regularization (Düzenlileştirme)

Modellerin daha karmaşık hale gelmesi, veri seti boyutunun ve değişken sayısının artması model eğitiminde farklı optimizasyon yöntemlerinin uygulanmasını kaçınılmaz hale getirmiştir. Bu optimizasyon temel olarak iki şekilde sağlanabilir: (*i*) çoklu doğrusal bağlantıya yol açan ya da hedef değişkeni öngörmede gereksiz olan değişkenleri çıkarmak, (*ii*) öznitelik değişkenlerinin tahmin parametrelerini hedef değişkeni öngörmedeki öden derecelerine göre ağırlıklandırmaktır. Bu şekilde modelin karmaşıklığını modelin yanlılığına bağlı hata ile varyansına bağlı hata arasında denge kurarak düzelten optimizasyon tekniğine düzenlileştirme (regularization) denir.

### Lasso Regularization

Tüm değişkenler ile model kurar. İlgisiz olan değişkenleri direkt olarak sıfır yapar.

### Ridge Regurlarization

Tüm değişkenler ile model kurar. Değişkenleri ağırlıklandırır. İlgisiz olan değişkenleri sıfıra yaklaştırır.

### Elasticnet

Lasso Regularizaton veya Ridge Regularization arasında seçim yapmamızı sağlar.



## Referanslar

* https://medium.com/@gulcanogundur/overfitting-a%C5%9F%C4%B1r%C4%B1-%C3%B6%C4%9Frenme-underfitting-eksik-%C3%B6%C4%9Frenme-ve-bias-variance-%C3%A7eli%C5%9Fkisi-b92bef2f770d
