# Performance Evaluation Metrics

## İçerik
- [Performance Evaluation Metrics](#performance-evaluation-metrics)
  - [İçerik](#i̇çerik)
  - [Giriş](#giriş)
  - [Regresyon Modellerinin Değerlendirilmesi](#regresyon-modellerinin-değerlendirilmesi)
    - [Mean Absolute Error(MAE)](#mean-absolute-errormae)
    - [Mean Squared Error(MSE)](#mean-squared-errormse)
    - [Root Mean Squared Error(RMSE)](#root-mean-squared-errorrmse)
    - [R²](#r)
    - [Adjusted R²](#adjusted-r)
  - [Sınıflandırma Modellerinin Değerlendirilmesi](#sınıflandırma-modellerinin-değerlendirilmesi)
    - [Confusion Matrix(Karışıklık Matrisi)](#confusion-matrixkarışıklık-matrisi)
    - [AUC-ROC CURVE](#auc-roc-curve)
  - [Referanslar](#referanslar)

## Giriş

Makine Öğrenimi algoritmaları, belirli bir durum için kullanılır ve benzer durumdaki bilinmeyenler için sonuç tahmin etmek için kullanır. Bu algoritmalar aslında problemi çözmek için kullanır. Bu problemlerden ikisi regresyon ve sınıflandırma problemleridir.

**Regresyon**, temel olarak değişkenler arasındaki ilişkiyi bulmak için istatistiksel bir yaklaşımdır. Makine öğreniminde, veri kümesinden elde edilen değişkenler arasındaki ilişkiye dayalı olarak bir olayın sonucunu tahmin etmek için kullanılır.

**Sınıflandırma**, veri öğelerinin ait olduğu sınıfı belirtir ve çıktıda sonlu ve ayrık değerler olduğunda kullanılır. Bir giriş değişkeni için bir sınıf öngörür. Bir veya daha fazla girdi verildiğinde, bir sınıflandırma modeli bir veya daha fazla sonucun değerini tahmin etmeye çalışacaktır.

![](photo/1.PNG)

Görüldüğü üzere aslında regresyon ve sınıflandırma ikisi de denetimli öğrenme modelidir. Yani her ikisi de tahmin yapmak için etiketlenmiş eğitim veri kümelerini kullanır. Bir başka deyişle denetimli öğrenme algoritmaları, hedef tahmin çıktısı ile girdi özellikleri arasındaki ilişkileri ve bağımlılıkları modellemeye çalışır. Böylece önceki veri kümelerinden öğrendiği ilişkilere dayanarak yeni veriler için çıktı değerlerini tahmin edebiliriz. 

**Bir regresyon modeli** sürekli değerleri öngörür. Örneğin, regresyon modelleri aşağıdaki gibi soruları cevaplayan tahminlerde bulunur:

* Aydın’da bir evin değeri nedir?
* Bir kullanıcının bu reklamı tıklama olasılığı nedir?

**Bir sınıflandırma modeli** kategorik değerleri öngörür. Örneğin, sınıflandırma modelleri aşağıdaki gibi soruları cevaplayan tahminlerde bulunur:

* Belirli bir e-posta iletisi spam mi yoksa spam değil mi?
* Bu bir köpek, kedi veya bir hamster görüntüsü mü?

## Regresyon Modellerinin Değerlendirilmesi

### Mean Absolute Error(MAE)

Mutlak hata, tahmin edilen değerler ile gerçek değerler arasındaki farktır. Tam olarak ifade etmek gerekirse, veri kümesinin tüm örneğinde, o örnek için gerçek değer ile öngörülen değer arasındaki her bir farkın mutlak değerinin ortalamasıdır.

![](photo/2.PNG)

* y, gerçek değerdir.
* y^ tahmin edilen değerdir.

> Düşük bir değer daha iyi doğruluğu gösterir.

```py
from sklearn.metrics import mean_absolute_error
mean_absolute_error(y_true, y_pred)
```

### Mean Squared Error(MSE)

Ortalama Kare Hatası (MSE) en sık kullanılan regresyon kaybı fonksiyonudur. MSE, tüm veri kümesinde örnek başına ortalama kare kaybıdır. MSE’yi hesaplamak için, tek tek örnekler için tüm kare kayıplarını toplayın ve daha sonra örnek sayısına bölün.

![](photo/3.PNG)

* x, modelin tahminde bulunmak için kullandığı özelliktir.
* prediction(x) anlamı, x özelliğine göre tahmin edilen değerdir.
* y, gerçek değerdir.
* N, örnek sayısıdır.

> Düşük bir değer daha iyi doğruluğu gösterir.

```py
from sklearn.metrics import mean_squared_error
mean_squared_error(y_true, y_pred)
```

> Kare nedeniyle, büyük hataların MSE üzerinde küçük hatalardan daha fazla etkisi vardır. Bu nedenle MAE, kareden faydalanmadığı için aykırı değerlere karşı daha sağlamdır.

> Verilerde aykırı değer varsa ve bunları yok saymak istiyorsanız, MAE daha iyi bir seçenektir ancak bunları kayıp fonksiyonunuzda hesaba katmak istiyorsanız MSE / RMSE’ye gidin.

### Root Mean Squared Error(RMSE)

Ortalama Kare Hatasının kökünün alınmış değerini ifade eder.

![](photo/4.PNG)

### R²

R², verilerin yerleştirilmiş regresyon hattına ne kadar yakın olduğunun istatistiksel bir ölçüsüdür. Ayrıca belirleme katsayısı veya çoklu regresyon için çoklu belirleme katsayısı olarak da bilinir. Daha basit bir dilde söylemek gerekirse R-kare, doğrusal regresyon modelleri için uygunluk ölçüsüdür.

Aynı veri seti için, daha yüksek R-kare değerleri, gözlemlenen veriler ve fit edilen değerler arasında daha küçük farkları temsil eder.

![](photo/5.PNG)

> R-kare, bir regresyon modelinin verilerinize yeterli bir uyum sağlayıp sağlamadığını göstermez. İyi bir model düşük bir R-kare değerine sahip olabilir. Öte yandan, taraflı bir model yüksek bir R-kare değerine sahip olabilir!

Örneğin bazı çalışma alanları, doğası gereği daha fazla miktarda açıklanamayan varyasyona sahiptir. Bu alanlarda, R-kare değerleriniz daha düşük olmak zorundadır. Mesela insan davranışını açıklamaya çalışan çalışmalar genellikle % 50'nin altında R-kare değerlerine sahiptir. İnsanları tahmin etmek, fiziksel süreçler gibi şeylerden daha zordur.

Model için R-kare’nin ne kadar yüksek olması yararlı tahminler üretir? Bu, ihtiyaç duyduğunuz hassasiyete ve verilerinizde bulunan varyasyon miktarına bağlıdır. Kesin tahminler için yüksek bir R-kare gereklidir ancak yüksek R-kare değerleri her zaman mükemmel mi?

Hayır! Yüksek R-kare değerine sahip bir regresyon modelinde çok sayıda sorun olabilir. Örneğin, ‘overfitting’ durumunda yüksek R-kare değerlerine ulaşabilirsiniz.

R-kare oldukça basit görünen aslında derinliklerine inilmesi gereken bir metriktir.

```py
from sklearn.metrics import r2_score
sklearn.metrics.r2_score(y_true, y_pred)
```

![](photo/6.PNG)

### Adjusted R²

Bir modele eklenen her ek bağımsız değişken her zaman R² değerini artırır.

> Bağımsız değişken eklendikçe model karmaşıklaşır, model karmaşıklaşınca ‘overfitting’ ortaya çıkar. Dolayısıyla R-kare artar.

Bu tarz problemlere çözüm olması için Ayarlanmış R-kare devreye girer. Ayarlanmış R-kare, her bir bağımsız değişkeni telafi eder ve yalnızca verilen her değişken, modeli mümkün olanın üstünde geliştirdiğinde artar.

```py
# n = örnek boyutu sayısı
# p = bağımsız değişken sayısı
adj_r2 = 1-(1-R2)*(n-1)/(n-p-1)
```

## Sınıflandırma Modellerinin Değerlendirilmesi

### Confusion Matrix(Karışıklık Matrisi)

Makine öğrenimi sınıflandırma problemi için bir performans ölçümüdür. Öngörülen ve gerçek değerlerin 4 farklı kombinasyonunu içeren bir tablodur.

![](photo/7.PNG)

Karışıklık matrisinde, bilmeniz gereken bazı terimler vardır. Bunlar daha sonra çeşitli metrikleri hesaplamak için kullanılabilir. Bu terimleri size basit bir şekilde şöyle söyleyebilirim.

> TP (True positive — Doğru Pozitif): Hastaya hasta demek.

> FP (False positive — Yanlış Pozitif): Hasta olmayana hasta demek.

> TN (True negative — Doğru Negatif): Hasta olmayana hasta değil demek.

> FN (False negative — Yanlış Negatif): Hasta olana hasta değil demek.

Yandaki karmaşık matrisinin hasta olan ve hasta olmayan insanların sınıflandırılması olarak düşünelim. Görülmektedir ki oluşturulan model 27 tane hastalığı olmayan kişinin 24 tanesini doğru bilmekte iken hasta olan 34 hastanın da 31 tanesinin hasta olduğunu doğru bir şekilde tahmin edebilmiştir.

Bu şekilde karmaşıklık matrisinden modelimizin performansını açıklayabiliriz.

Yukarıdaki terimler ile hesaplayabileceğimiz bazı metrikler vardır.

![](photo/8.PNG)

**Doğruluk(Accuracy)**, doğru olarak sınıflandırılan örneklerin yüzdesidir.

**Duyarlılık(Recall)**, pozitif olarak tahmin etmemiz gereken işlemlerin ne kadarını pozitif olarak tahmin ettiğimizi gösteren bir metriktir. “Gerçek pozitiflerin ne kadarı doğru bir şekilde tanımlandı?”

**Kesinlik(precision)**, pozitif olarak tahminlediğimiz değerlerin gerçekten kaç adedinin pozitif olduğunu göstermektedir.

Kesinlik ve Duyarlılık tanım olarak birbirine çok benzemektedir ve bu karışıklığa sebep olabilir. Aralarındaki farkı çok güzel bir şekilde gösteren diyagrama bakalım.

![](photo/9.PNG)

```py
# Confusion Matrix
from sklearn.metrics import confusion_matrix
confusion_matrix(y_true, y_pred)
# Accuracy
from sklearn.metrics import accuracy_score
accuracy_score(y_true, y_pred)
# Recall
from sklearn.metrics import recall_score
recall_score(y_true, y_pred, average=None)
# Precision
from sklearn.metrics import precision_score
precision_score(y_true, y_pred, average=None)
```

**F1 skoru**, bir testin doğruluğunun bir ölçüsüdür —kesinlik ve duyarlılığın harmonik ortalamasıdır. Maksimum 1 (mükemmel kesinlik ve duyarlılık) ve minimum 0'a sahip olabilir. Genel olarak, modelinizin kesinliğinin ve sağlamlığının bir ölçüsüdür. Örneğin iki modeli düşük kesinlik ve yüksek duyarlılık ile karşılaştırmak zordur veya tersi de geçerlidir. Bu yüzden onları karşılaştırılabilir hale getirmek için F1 Skoru kullanıyoruz.

![](photo/10.PNG)

```py
# Yöntem 1: sklearn
from sklearn.metrics import f1_score
f1_score(y_true, y_pred, average=None)
# Yöntem 2: Manuel Hesaplama
F1 = 2 * (precision * recall) / (precision + recall)
```

### AUC-ROC CURVE

AUC — ROC eğrisi çeşitli eşik ayarlarında sınıflandırma problemi için bir performans ölçümüdür. ROC bir olasılık eğrisidir ve AUC ayrılabilirliğin derecesini veya ölçüsünü temsil eder. AUC, ROC eğrisinin altında kalan alandır. Modelleri sınıflar arasında ne kadar ayırt edebildiğini anlatır. AUC yükseldikçe, model tahmin etmede daha iyi demektir. Örneğin, AUC ne kadar yüksekse, model hastalığı olan ve olmayan hastaları ayırt etmekte daha iyidir.

> Eşikler probleme bağlıdır ve bu nedenle probleme göre ayarlamanız gereken değerlerdir.

Bilmemiz gereken iki önemli terim vardır.

**Gerçek Pozitif Oran (Hassasiyet)**: Gerçek Pozitif Oran(TPR), tüm pozitif veri noktalarına göre pozitif olarak kabul edilen pozitif veri noktalarının oranına karşılık gelir.

> Örneğin, Hassasiyet bize kalp hastalığı olan insanların yüzde kaçının gerçekte doğru olarak tanımlandığını söyler.

![](photo/11.PNG)

**Yanlış Pozitif Oran (Özgüllük)**: Yanlış Pozitif Oran(FPR), tüm negatif veri noktalarına göre yanlışlıkla pozitif olarak kabul edilen negatif veri noktalarının oranına karşılık gelir.

> Örneğin, Özgüllük bize kalp hastalığı olmayan insanların yüzde kaçının gerçekte doğru bir şekilde tanımlandığını söyler.

![](photo/12.PNG)

![](photo/13.PNG)

Yukarıdaki grafikte kırmızı dağılım, hastalığı olmayan tüm hastaları ve yeşil dağılım, hastalığı olan tüm hastaları temsil etsin. Sınıflandırma eşik değerimizi de 0.5 olarak varsayalım.

Eşiğin üzerindeki tüm pozitif değerler “Gerçek Pozitifler(TP)” ve eşiğin üzerindeki negatif değerler, pozitif olarak yanlış tahmin edildiği için “Yanlış Pozitif(FP)” olacaktır.

Eşiğin altındaki tüm negatif değerler “Gerçek Negatifler(TN)” ve eşiğin altındaki pozitif değerler, negatif olarak yanlış tahmin edildiği için “Yanlış Negatif(FN)” olacaktır.

![](photo/14.PNG)

Eşik değerimizi 0.5’ten 0.6’ya çekelim. Açıkça görülmektedir ki sınıflandırma eşiğini yükseltmek, daha fazla öğeyi ‘hasta olmayan’ olarak sınıflandırır, böylece hem Yanlış Pozitifleri hem de Gerçek Pozitifleri düşürür.

> Pozitifleri doğru bir şekilde tanımlamak bizim için önemliyse, daha yüksek Hassasiyetli bir model seçmeliyiz. Bununla birlikte, negatifleri doğru bir şekilde tanımlamak daha önemliyse, ölçüm metriği olarak Özgüllüğü seçmeliyiz.

![](photo/15.PNG)

## Referanslar

* https://medium.com/deep-learning-turkiye/model-performans%C4%B1n%C4%B1-de%C4%9Ferlendirmek-metrikler-cb6568705b1
