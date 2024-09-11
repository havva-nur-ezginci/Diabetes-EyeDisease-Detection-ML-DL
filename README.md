# Diyabet ve Diyabete Bağlı Göz Hastalıkları Tespiti: Makine ve Derin Öğrenme Yöntemleri

Bu proje, diyabetin ve diyabete bağlı göz hastalıklarının tespitini gerçekleştirmek için makine öğrenmesi ve derin öğrenme yöntemlerinin uygulanmasını içermektedir. Çalışma iki ana başlık altında toplanmıştır: diyabet tespiti ve göz hastalığı tespiti.

## Table of Contents
- [Diyabet Tespiti](#diyabet-tespiti)
- [Göz Hastalığı Tespiti](#göz-hastalığı-tespiti)

## Diyabet Tespiti 

Bu projede, Kaggle'dan alınan kan değerleri veri seti kullanılarak diyabet tespiti amacıyla çeşitli makine öğrenmesi modelleri uygulanmıştır. Farklı modellerin performansı karşılaştırılmış, en iyi sonucu veren model belirlenmiştir.

### Kullanılan Veri Seti

- **Kaynak**: Kaggle
- **Bölme**: Veri seti %80 eğitim, %20 test olarak ayrılmıştır.

### Kullanılan Modeller

Projede aşağıdaki makine öğrenmesi modelleri kullanılmıştır:

- Perceptron
- MLPClassifier (Multi-layer Perceptron)
- Karar Ağacı (Decision Tree)
  - Overfitting’i önlemek amacıyla max_depth parametresi kullanılarak erken budama yapılmıştır (max_depth=5).
- Logistic Regression
- KNeighborsClassifier
- Support Vector Classification (SVC)
- Gaussian Naive Bayes
- Random Forest Classifier

### Yöntemler ve İyileştirmeler

1. **Veri ön işleme** adımı kapsamında, model eğitiminin daha tutarlı ve dengeli olmasını sağlamak amacıyla **StandardScaler** kullanılarak sayısal değişkenler ölçeklendirildi. Bu işlem, her bir değişkenin ortalamasını 0, standart sapmasını 1 yaparak, farklı büyüklüklerdeki verilerin model üzerinde eşit etkiye sahip olmasını sağladı.
2. **Karar Ağacı**: Aşırı öğrenmeyi önlemek için max_depth parametresi ile sınırlama yapılmıştır. 
3. **K-Fold Cross Validation**: Modellerin doğruluğunu artırmak için K-fold çapraz doğrulama yöntemi kullanılmıştır. 5, 10, 15, 20, 25 ve 30 fold değerleri ile çapraz doğrulama yapılmış, her bir modelin maksimum, minimum ve ortalama doğruluk oranları incelenmiştir.
4. **Model Başarımlarının İncelenmesi**: Logistic Regression, Perceptron, MLPClassifier, Decision Tree, KNeighborsClassifier, SVC, GaussianNB, Random Forest modelleri kullanılarak doğruluk değerleri analiz edilmiştir.

### Sonuçlar

Test setinde en yüksek doğruluk oranı **%81** ile **Logistic Regression** modelinden elde edilmiştir.

### Files and Code

[Diyabet Tespiti](https://github.com/havva-nur-ezginci/Diabetes-EyeDisease-Detection-ML-DL/blob/main/Diyabet_Tespiti/DiyabetTahminModelleri.ipynb) dosyasında projeye ait tüm kod ve analizler yer almaktadır.

<!--

>>>>>>>>>>>>    2 . bÖLÜM     >>>>>>>>>>>

-->

## Göz Hastalığı Tespiti

Diyabet (şeker hastalığı) obezite, hareketsiz yaşam, dengesiz beslenme, ileri yaş, stres gibi olumsuz yaşam şartlarıyla beraber son yıllarda görülme sıklığının artmasıyla birlikte birçok önemli hastalığa da zemin hazırlamaktadır. Erken dönemde hastalığın fark edilememesi görme kayıplarına ve ileriki aşamalarda körlüğe kadar gitmektedir. Diyabetik retinopati, katarakt ve glokom hastalıklarının tespitinde göz fundus görüntülerinden sıkça yararlanılır. Bu projede diyabetin sebep olduğu göz hastalıklarından bazıları diyabetik retinopati, katarakt ve glokom hastalıklarının tespiti yapılmıştır. Çalışmada **Ocular Disease Intelligent Recognition (ODIR)** veri seti kullanılmıştır. Veri seti içerisinden **normal, diyabetik retinopati, katarakt ve glokom** sınıfları seçilerek çalışma gerçekleştirilmiştir. Elde edilen veriler ilk hali haricinde farklı veri artırma yöntemleri kullanılarak dengeli veri setleri oluşturulmuştur. Oluşturulan veri setleri state of the art olarak bilinen **VGG16, VGG19** modelleri üzerinde **Stochastic Gradient Descent (SGD), Adaptive Gradient Algorithm (Adagrad), Adaptive Moment Estimation (Adam)** optimizerları kullanılarak eğitimler gerçekleştirilmiştir. Sonuç olarak elde edilen en yüksek başarı oranı **ADASYN** yöntemi ile artırılan veri setinin **VGG16** modelini **Adam** optimizerı ile eğittiğimizde test verisi üzerinde %86 başarı ve %43 hata oranı elde edilmiştir.

### Kullanılan Veri Seti

- **Kaynak**:  [Ocular Disease Recognition](https://www.kaggle.com/datasets/andrewmvd/ocular-disease-recognition-odir5k)
- **Bölme**: Veri seti %80 eğitim, %20 test olarak ayrılmıştır.

Bu bölümde, diyabete bağlı olarak gelişen göz hastalıklarının tespitine odaklanılmıştır. Kaggle'dan alınan veri seti kullanılarak göz hastalıkları tespit edilmiştir.

Gerçekleştirilen çalışmada en iyi sınıflandırma sonucu ADASYN sentetik veri artırma yöntemi kullanılarak oluşturulan veri seti VGG16 modeline ADAM optimizasyon yöntemi uygulanarak %86 başarı oranı elde edilmiştir.

Tespit Edilen Sınıflar:
- Normal
- Diyabetik Retinopati
- Katarakt
- Glokom

Kullanılan Yöntemler:
- Veri seti, SMOTE ve ADASYN yöntemleriyle artırılmıştır.
- VGG16 ve VGG19 derin öğrenme modelleri, SGD, Adagrad ve Adam optimizerları ile eğitilmiştir.
- Eğitim için Google Colab GPU kullanılmıştır.
- 
### Files and Code

[Göz Hastalığı Tespiti](https://github.com/havva-nur-ezginci/Diabetes-EyeDisease-Detection-ML-DL) dosyalarında projeye ait tüm kod ve analizler yer almaktadır.

# Yayınlar ve Sunumlar
Bu projeyle ilgili sunum 9. Uluslararası Bilimsel Çalışmalar Kongresi'nde (UBCAK) gerçekleştirilmiştir: [UBCAK9 pdf](https://www.ubcakcongress.org/ubcak9_tam_metin.pdf)
### Göz Fundus Görüntülerinden Diyabetin Sebep Olduğu Göz Hastalıklarının Tespiti
DEMİRCAN SEMİYE, Ezginci Havva Nur (03.08.2022-05.08.2022), Yayın Yeri: 9. Uluslararası Bilimsel Çalışmalar Kongresi (UBCAK)
<br>Yayın Türü: Ulusal Tam Metin Bildiri (Basılı + Elektronik)
