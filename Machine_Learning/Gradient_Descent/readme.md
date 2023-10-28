# Gradient Descent (Gradyan Azalma)

## İçerik
- [Gradient Descent (Gradyan Azalma)](#gradient-descent-gradyan-azalma)
  - [İçerik](#i̇çerik)
  - [Giriş](#giriş)
  - [İşlem adımları](#i̇şlem-adımları)
  - [Stochastic Gradient Descent](#stochastic-gradient-descent)
  - [Mini-Batch Gradient Descent](#mini-batch-gradient-descent)
  - [Basic Example](#basic-example)
    - [Example Code](#example-code)
  - [Referanslar](#referanslar)

## Giriş

Her öğrenme algoritmasının temelde 3 bölüme sahip olduğunu söylemek mümkündür.

1. Kayıp fonksiyonu
2. Kayıp fonksiyonuna dayanan bir optimizasyon ölçütü (örn. maliyet fonksiyonu)
3. Optimizasyon ölçütüne çözüm bulmak için eğitim verilerini kullanan optimizasyon rutini

Makine öğrenmesi ile ilgili modern literatürü okuduğumuzda, genel olarak gradyan iniş veya stokastik gradyan iniş ile karşılaşırız. Bunlar, optimizasyon ölçütünün farklılaştırılabildiği durumlarda en sık kullanılan iki optimizasyon algoritmasıdır. Gradyan iniş (Gradient Descent), bir fonksiyonun minimumunu bulmak için tekrarlanan bir optimizasyon algoritmasıdır. Bu algoritma kullanılarak bir fonksiyonun yerel minimum değerini bulmak için, rastgele bir noktada başlar ve geçerli noktadaki fonksiyonun dradyanının (veya yaklaşık gradyanın) negatifiyle orantılı adımlar atar.

![Gradient](photo/1.PNG)

Gradyan iniş, doğrusal ve lojistik regresyon, SVM ve sinir ağları için en uygun parametreleri bulmak için kullanılabilir. Lojistik regresyon veya SVM gibi birçok model için optimizasyon ölçütü dışbükeydir. Dışbükey fonksiyonların sadece bir minimum değeri vardır ve bu geneldir (küreseldir). Sinir ağları için optimizasyon ölçütleri dışbükey değildir; ancak uygulamalarda yerel minimum değerini bulmak bile yeterli olacaktır.

![Gradient](photo/2.PNG)


## İşlem adımları

1. Her parametre için Kayıp Fonksiyonun (loss function) türevini al.
   
![Gradient](photo/3.PNG)

2. Parametreler için rastgele değerler topla ve toplanan değerleri parametrelere gönder.
3. Adım büyüklüğü (step size) hesapla.

![Gradient](photo/4.PNG)

4. Yeni parametreyi hesapla.

![Gradient](photo/5.PNG)

5. Minimum seviyeye ulaşana kadar 2. adıma dön.

Gradient Descent temelinde türev olan bir optimizasyon işlemidir aslında. Bu işlemde temelde iki soru karşımıza çıkar aslında. Birincisi işlem adımı olarak tanımlayabileceğimiz *learning rate*, ikincisi ise başlangıç noktası olarak tanımlayabileceğimiz *start point*'dir.

![Gradient](photo/6.PNG)

## Stochastic Gradient Descent

Her adımda rastgele alınan 1 veri üzerinde işlem yapar. Noktalar sürekli değişerek optimum noktaya ulaşmayı amaçlar. Batch Gradient Descent’e göre daha hızlıdır. Stochastic Gradient Descent ile iyi bir sonuca ulaşılır ama optimum sonuca ulaşılamayabilir.

![Gradient](photo/7.PNG)

## Mini-Batch Gradient Descent

Veri seti içerisinden rastgele alınan örneklemler ile öğrenir. Diğer ikisinden daha hızlıdır. Stochastic Gradient Descent’e göre daha dengeli ilerler, onun kadar çok savrulmaz.

![Gradient](photo/8.PNG)

## Basic Example

![Gradient](photo/10.PNG)

![Gradient](photo/9.PNG)

> f(x) = x^2

> f'(x) = 2x

> Start Point = 3

> Learning Rate = 0.1

### Example Code

```py
import numpy as np
from typing import Callable


def gradient_descent(start: float, gradient: Callable[[float], float],
                     learn_rate: float, max_iter: int, tol: float = 0.01):
    x = start
    steps = [start]  # history tracking

    for _ in range(max_iter):
        diff = learn_rate*gradient(x)
        if np.abs(diff) < tol:
            break
        x = x - diff
        steps.append(x)  # history tracing
  
    return steps, x
```

![Gradient](photo/11.PNG)


```py
def func1(x:float):
    return x**2-4*x+1

def gradient_func1(x:float):
    return 2*x - 4
```

```
history, result = gradient_descent(9, gradient_func1, 0.1, 100)
```

![Gradient](photo/12.PNG)


## Referanslar

* https://medium.com/deep-learning-turkiye/gradient-descent-nedir-3ec6afcb9900
* https://towardsdatascience.com/gradient-descent-algorithm-a-deep-dive-cf04e8115f21
