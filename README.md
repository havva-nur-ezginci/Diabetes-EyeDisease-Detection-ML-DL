# Diyabet ve Diyabete Bağlı Göz Hastalıkları Tespiti: Makine ve Derin Öğrenme Yöntemleri
[![Kaggle](https://img.shields.io/badge/Kaggle-Dataset-blue?logo=kaggle)](https://www.kaggle.com/datasets/andrewmvd/ocular-disease-recognition-odir5k)

Bu proje, diyabetin ve diyabete bağlı göz hastalıklarının tespitini gerçekleştirmek için makine öğrenmesi ve derin öğrenme yöntemlerinin uygulanmasını içermektedir. Çalışma iki ana başlık altında toplanmıştır: diyabet tespiti ve göz hastalığı tespiti.

## Table of Contents
- [Diyabet Tespiti](#diyabet-tespiti)
- [Göz Hastalığı Tespiti](#göz-hastalığı-tespiti)

## Diyabet Tespiti 

Bu projede, Kaggle'dan alınan kan değerleri veri seti kullanılarak diyabet tespiti amacıyla çeşitli makine öğrenmesi modelleri uygulanmıştır. Farklı modellerin performansı karşılaştırılmış, en iyi sonucu veren model belirlenmiştir.

### Kullanılan Veri Seti

- **Kaynak**: [Diabetes](https://github.com/havva-nur-ezginci/Diabetes-EyeDisease-Detection-ML-DL/blob/main/Diyabet_Tespiti/Dataset/Diyabet/diabetes.csv) veri seti projeye eklenerek kullanılmıştır.
- **Bölme**: Veri seti %80 eğitim, %20 test olarak ayrılmıştır.

<details> 
  <summary>Learn More</summary> 
  <p>Bu veri seti, 768 örnek içermektedir. Bu örneklerden 500'ü diyabet bulunmayan (0) ve 268'i diyabetli (1) olarak etiketlenmiştir. Etiketler, 0 diyabetin olmadığını, 1 ise diyabetin varlığını ifade eder.
   Veri seti, Ulusal Diyabet, Sindirim ve Böbrek Hastalıkları Enstitüsü'nden alınmış olup, hastaların belirli tanısal ölçümlere dayanarak diyabetli olup olmadıklarının tahmin edilmesini amaçlamaktadır. Tüm
   hastalar, Pima Kızılderili mirasına sahip en az 21 yaşında kadınlardır.</p>
   
   <h3>Veri Seti Özellikleri</h3>
   <ul>
    <li><strong>Pregnancy</strong>: Hamile kalma sayısı</li>
    <li><strong>Glucose</strong>: Plazma glukoz konsantrasyonu</li>
    <li><strong>Blood Pressure</strong>: Diyastolik kan basıncı (mm Hg)</li>
    <li><strong>Insulin</strong>: Serum insülin seviyeleri (mu U/ml)</li>
    <li><strong>BMI</strong>: Vücut kitle indeksi (ağırlık (kg) / boy (m)^2)</li>
    <li><strong>Diabetes Pedigree Function</strong>: Diyabet soy ağacı işlevi</li>
    <li><strong>Age</strong>: Yaş (yıl)</li>
    <li><strong>Outcome</strong>: Sınıf değişkeni (0: Hasta değil, 1: Hasta)</li>
   </ul>
</details>

### Kullanılan Modeller

Projede aşağıdaki makine öğrenmesi modelleri kullanılmıştır:

- Perceptron
- MLPClassifier (Multi-layer Perceptron)
- Karar Ağacı (Decision Tree)
- Logistic Regression
- KNeighborsClassifier
- Support Vector Classification (SVC)
- Gaussian Naive Bayes
- Random Forest Classifier

### Yöntemler ve İyileştirmeler

1. **Veri ön işleme** adımı kapsamında, model eğitiminin daha tutarlı ve dengeli olmasını sağlamak amacıyla **StandardScaler** kullanılarak sayısal değişkenler ölçeklendirildi. Bu işlem, her bir değişkenin ortalamasını 0, standart sapmasını 1 yaparak, farklı büyüklüklerdeki verilerin model üzerinde eşit etkiye sahip olmasını sağladı.
2. **Karar Ağacı**: Aşırı öğrenmeyi önlemek için max_depth parametresi kullanılarak erken budama ile sınırlama yapılmıştır(max_depth=5). Karar ağacının özellikler için vermiş olduğu önem değerleri incelenmiştir. Her özellik için 0 ile 1 arasında bir sayıdır; 0=>"hiç kullanılmamış" ve 1 => "hedefi mükemmel şekilde tahmin ediyor" anlamına gelir. Alınan sonuçlar için matplotlib.pyplot kullanarak grafik çizdirilmiş ve değerler Tablo 1 de görselleştirilmiştir:

**Tablo 1: Karar Ağacı Sonucunda Alınan Özellik Önem Değerleri:**
<table>
  <tr>
    <td>
      <table border="1">
        <tr>
          <th>Özellik</th>
          <th>Önem Değeri</th>
        </tr>
        <tr>
          <td>Pregnancy</td>
          <td>0.01147274</td>
        </tr>
        <tr>
          <td>Glucose</td>
          <td>0.37701637</td>
        </tr>
        <tr>
          <td>Blood Pressure</td>
          <td>0.07524925</td>
        </tr>
        <tr>
          <td>SkinThickness</td>
          <td>0.06196233</td>
        </tr>
        <tr>
          <td>Insulin</td>
          <td>0.06910943</td>
        </tr>
        <tr>
          <td>BMI</td>
          <td>0.19682277</td>
        </tr>
        <tr>
          <td>Diabetes Pedigree</td>
          <td>0.05909082</td>
        </tr>
        <tr>
          <td>Age</td>
          <td>0.1492763</td>
        </tr>
      </table>
    </td>
    <td>
      <img src="https://github.com/user-attachments/assets/302eb5b7-c5db-4815-b925-26371336637c" alt="3-Karar Ağacı özellik önem grafiği" >
    </td>
  </tr>
</table>

  
3. **K-Fold Cross Validation**: Modellerin doğruluğunu artırmak için K-fold çapraz doğrulama yöntemi kullanılmıştır. 5, 10, 15, 20, 25 ve 30 fold değerleri ile çapraz doğrulama yapılmış, her bir modelin maksimum, minimum ve ortalama doğruluk oranları incelenmiştir.
4. **Model Başarımlarının İncelenmesi**: Logistic Regression, Perceptron, MLPClassifier, Decision Tree, KNeighborsClassifier, SVC, GaussianNB, Random Forest modelleri kullanılarak doğruluk değerleri analiz edilmiştir.

### Eğitim ve Test Sonuçları

Tablo2 : Diyabet testpiti için farklı modellerin 80:20 ayrılan veri seti eğitim ve test sonuçlarını göstermektedir:

| Model                     | Eğitim Sonuçları | Test Sonuçları |
|---------------------------|------------------|----------------|
| **Perceptron**                | 0.72             | 0.79           |
| **MLP**                       | 0.82             | 0.77           |
| **Karar Ağacı**               | 0.85             | 0.78           |
| **Logistic Regression**       | 0.76             |**0.81**           |
| **K-Nearest Neighbors (KNN)**  | 0.78             | 0.80           |
| **Support Vector Classifier (SVC)** | 0.76         | 0.79           |
| **Gaussian Naive Bayes**      | 0.74             | 0.78           |
| **Random Forest Classifier**  | 0.98             | 0.79           |

Test setinde en yüksek doğruluk oranı **%81** ile **Logistic Regression** modelinden elde edilmiştir.

### Files and Code

[Diyabet Tespiti](https://github.com/havva-nur-ezginci/Diabetes-EyeDisease-Detection-ML-DL/blob/main/Diyabet_Tespiti/DiyabetTahminModelleri.ipynb) dosyasında projeye ait tüm kod ve analizler yer almaktadır.

<!--

>>>>>>>>>>>>    2 . bÖLÜM     >>>>>>>>>>>

-->

## Göz Hastalığı Tespiti

Diyabet (şeker hastalığı) obezite, hareketsiz yaşam, dengesiz beslenme, ileri yaş, stres gibi olumsuz yaşam şartlarıyla beraber son yıllarda görülme sıklığının artmasıyla birlikte birçok önemli hastalığa da zemin hazırlamaktadır. Erken dönemde hastalığın fark edilememesi görme kayıplarına ve ileriki aşamalarda körlüğe kadar gitmektedir. Diyabetik retinopati, katarakt ve glokom hastalıklarının tespitinde göz fundus görüntülerinden sıkça yararlanılır. Bu projede diyabetin sebep olduğu göz hastalıklarından bazıları diyabetik retinopati, katarakt ve glokom hastalıklarının tespiti yapılmıştır. Çalışmada Kaggle'dan alınan **Ocular Disease Intelligent Recognition (ODIR)** veri seti kullanılmıştır. Veri seti içerisinden **normal, diyabetik retinopati, katarakt ve glokom** sınıfları seçilerek çalışma gerçekleştirilmiştir. Elde edilen veriler ilk hali haricinde farklı veri artırma yöntemleri kullanılarak dengeli veri setleri oluşturulmuştur. Oluşturulan veri setleri state of the art olarak bilinen **VGG16, VGG19,ResNet50,AlexNet** modelleri 
üzerinde **Stochastic Gradient Descent (SGD), Adaptive Gradient Algorithm (Adagrad), Adaptive Moment Estimation (Adam), RMSprop, Adadelta** optimizerları kullanılarak eğitimler gerçekleştirilmiştir. Farklı modellerin performansı karşılaştırılmış, en iyi sonucu veren model belirlenmiştir. Sonuç olarak elde edilen en yüksek başarı oranı **ADASYN** yöntemi ile artırılan veri setinin **VGG16** modelini **Adam** optimizerı ile eğittiğimizde test verisi üzerinde %86 başarı ve %43 hata oranı elde edilmiştir.


## Veri Seti
[![Kaggle](https://img.shields.io/badge/Kaggle-Dataset-blue?logo=kaggle)](https://www.kaggle.com/datasets/andrewmvd/ocular-disease-recognition-odir5k)

Proje, [Ocular Disease Recognition](https://www.kaggle.com/datasets/andrewmvd/ocular-disease-recognition-odir5k) veri setini kullanmaktadır. 


<details>
  <summary>Learn More</summary>

ODIR veri seti, 2019 yılında Shanggong Medical Technology Co., Ltd. tarafından Çin'deki hastanelerden/tıp merkezlerinden toplanmıştır. 5.000 hastanın fundus fotoğraflarını içeren bu veri seti, sekiz farklı göz hastalığını kapsar: Normal (N), Diyabet (D), Glokom (G), Katarakt (C), Yaşa Bağlı Makula Dejenerasyonu (A), Hipertansif Retinopati (H), Miyopi (M) ve diğer hastalıklar (O). 

Bu çalışmada Diyabetik Retinopati, Katarakt, Glokom ve Normal sınıfları kullanılmıştır.
</details>

Tespit Edilen Sınıflar:

- **Normal**: Sağlıklı göz
- **Diyabetik Retinopati**: Diyabetin neden olduğu retina hasarı
- **Katarakt**: Göz merceğinin bulanıklaşması
- **Glokom**: Göz içi basıncının artmasıyla meydana gelen optik sinir hasarı

Veri setinden alınmış örnek fundus fotoğrafları:
![Örnek fundus fotoğrafı](https://github.com/user-attachments/assets/fb9cba79-2580-48d3-9a4b-a5ef23367321)
  
## Kullanılan Yöntemler:

## 1. Veri Ön İşleme
   - Göz fundus görüntüleri, başlangıçta cv2'nin varsayılan ayarları ile mavi renk tonu (RGB yerine BGR) olarak okunmuştur. Bunu düzeltmek için `cv2.cvtColor(img, cv2.COLOR_BGR2RGB)` kullanılarak başarılı sonuçlar elde edilmiştir.
   - Görüntüler, `numpy.array` kullanılarak sayısal değerlere dönüştürülmüş ve `sklearn.model_selection.train_test_split` ile eğitim (%80) ve test (%20) verileri olarak ayrılmıştır.
   - Görüntüler, model giriş boyutlarına uygun olarak yeniden boyutlandırılmış (2224x224x3) ve normalize edilmiştir.

## 2. Veri Seti Artırma

Veri seti artırma yöntemi olarak **SMOTE** ve **ADASYN** sentetik veri artırma yöntemleri kullanılmıştır.

### 2.1 SMOTE (Synthetic Minority Over-Sampling Technique)
- SMOTE, sentetik veri üretilmesini sağlayan bir aşırı örnekleme sürecidir. Veri bilimi projelerinde en sık kullanılan yöntemlerden biridir.
- Yöntemin ana fikri, azınlık sınıfının örnekleri arasında belirli işlemler yaparak yeni azınlık sınıfı örnekleri yaratmaktır.

#### Sentetik örneklerin oluşturulma süreci:

1. İncelenen öznitelik vektörü (𝐸𝑖) ile en yakın komşusu arasındaki farkı alınır.
2. Bu fark, 0 ile 1 arasında rastgele bir sayı (𝛿) ile çarpılır.
3. Çıkan sonuç, incelenen öznitelik vektörüne eklenir ve yeni bir örnek oluşur.

- Gereken aşırı örnekleme miktarına bağlı olarak, en yakın k komşudan komşular rastgele seçilir. Bu işlem, aşırı öğrenme sorununun önüne geçer ve iyi bir sınıflandırma performansı sağlar.
         
[Veri Bilimi Okulu - Dengesiz Veri Setlerinde Modelleme](https://www.veribilimiokulu.com/dengesiz-veri-setlerinde-modelleme/#:~:text=SMOTE(Synthetic%20Minority%20Over%2DSampling,yeni%20az%C4%B1nl%C4%B1k%20s%C4%B1n%C4%B1f%C4%B1%20%C3%B6rnekleri%20yaratmakt%C4%B1r. )

  ### 2.2 Adaptive Synthetic Sampling Method (ADASYN)
  
  - SMOTE yönteminin geliştirilmiş bir versiyonudur. ADASYN hangi sayıda sentetik veri üreteceğine olasılık dağılım fonksiyonu kullanarak karar verir. [AYDIN, 2021](https://dergipark.org.tr/tr/download/article-file/1095950) Öğrenilmesi zor olan sınıflar için daha fazla sentetik veri üretilir. Böylece dengesiz sınıf dağılımdan dolayı oluşan eğilim azaltılmış olur. [Çürükoğlu, 2019](https://ieeexplore.ieee.org/document/8965444)


## 3. Model Seçimi ve Eğitim
   - AlexNet, VGG16, VGG19 ve ResNet50 modelleri ile çalışılmıştır.
   - **Transfer Öğrenme** yöntemi kullanılarak VGG16, VGG19 ve ResNet50 modelleri eğitilmiştir. Modellerin önceden eğitilmiş ağırlıkları `imagenet` veri setinden alınmıştır ve `include_top=False` kullanılarak kendi özel giriş ve çıkış katmanlarımız eklenmiştir. Ayrıca, `layer.trainable=False` parametresi ile modelin ağırlıklarının yeniden öğrenilmesi engellenmiştir.
   - Her modelin derlenmesinde loss='categorical_crossentropy',  metrics=['accuracy']) kullanılmış ve eğitim sırasında; batch_size=32, epochs= 20, validation_split=0.2 verilmiş olup optimizer da değişiklik yapılarak model eğitimi gerçekleştirilmiştir;
     - **VGG16**: Flatten ve dense çıkış katmanı eklendi ve çıkış katmanında sigmoid aktivasyon fonksiyonu kullanılmıştır. 
     - **VGG19**: Flatten ve dense çıkış katmanı eklendi ve çıkış katmanında sigmoid aktivasyon fonksiyonu kullanılmıştır. 
     - **ResNet50**: Flatten ve dense çıkış katmanı eklendi ve çıkış katmanında softmax aktivasyon fonksiyonu kullanılmıştır. 
     - **AlexNet**: Çıkış katmanında softmax aktivasyon fonksiyonu kullanılarak eğitim yapılmıştır.

## 4. Optimizer Kullanımı
- Bir makine öğrenmesi/derin öğrenme/yapay sinir ağı modeli tasarladığımızda da amacımız hatayı minimize etmektir. AlexNet, ResNet50, VGG16 ve VGG19 modelleri için aşağıdaki **optimize** ediciler kullanıldı.
   - **Stochastic Gradient Descent-SDG**
   - **RMSprop**
   - **Adagrad**
   - **Adadelta**
   - **Adam**

## 5. Fonksiyonlar:
- Tüm model eğitimleri için oluşturulan ve kullanılan fonksiyonlar;
   - Model eğitim geçmişi (`acc`, `loss`, `val_loss`, `val_accuracy`) CSV dosyası olarak kaydedilmiştir.
   - Eğitim geçmişinin her epoch'taki değerleri grafik olarak çizdirilmiştir (train ve validation için `loss` ve `accuracy` değerleri).
   - Eğitilen model `.h5` formatında kaydedilmiştir ve gerektiğinde tekrar yüklenebilir.
   - Modelin performansı `confusion matrix` ve `classification report` kullanılarak değerlendirilmiştir.


## Results
Gerçekleştirilen çalışmada en iyi sınıflandırma sonucu ADASYN sentetik veri artırma yöntemi kullanılarak oluşturulan veri seti VGG16 modeline ADAM optimizasyon yöntemi uygulanarak %86 başarı oranı elde edilmiştir. En yüksek başarı oranı gösteren modelin eğitim süreci Şekil 1 de gösterilmektedir. Test verisi için elde edilen Confusion matrix Şekil 2 de verilmiştir. 
 
### Şekil 1: Training Process: VGG16 with ADAM Optimizer on ADASYN Dataset

The following image shows the training process of the VGG16 model using the ADAM optimizer on the ADASYN-enhanced dataset.

![Training Process](https://github.com/user-attachments/assets/6d2cead1-7251-4799-b274-da75177a5167)

### Şekil 2: Confusion Matrix: Test Data

Below is the confusion matrix for the test data, which shows the model's performance in predicting different classes.

![Confusion Matrix](https://github.com/user-attachments/assets/89383e43-341e-4ecc-84e3-9e11ee14555d)

### 3. Test Data Class Distribution

- **Normal**: 264 samples  
- **Cataract**: 128 samples  
- **Diabetic Retinopathy**: 27 samples  
- **Glaucoma**: 115 samples

The confusion matrix provides insight into how well the model distinguishes between these different classes in the test dataset.


   
### Files and Code

Below are the links to the project files for different data augmentation methods used in the study:

- **ADASYN**: [Diabetes Eye Disease Detection with ADASYN](https://github.com/havva-nur-ezginci/Diabetes-EyeDisease-Detection-ML-DL/blob/main/Adasyn/Bitirme_2/2_adasyn_DiyabeteBagliGozHastaliklariTespiti.ipynb)
- **SMOTE**: [Diabetes Eye Disease Detection with SMOTE](https://github.com/havva-nur-ezginci/Diabetes-EyeDisease-Detection-ML-DL/blob/main/Smote/Bitirme_2/2_smote_DiyabeteBagliGozHastaliklariTespiti.ipynb)
- **Normal Dataset**: [Diabetes Eye Disease Detection without Data Augmentation](https://github.com/havva-nur-ezginci/Diabetes-EyeDisease-Detection-ML-DL/blob/main/Normal/Bitirme_2/2_normal_DiyabeteBagliGozHastaliklariTespiti.ipynb)

Each notebook demonstrates the application of different techniques in the detection of diabetic eye diseases.



# Publications and Presentations
Bu projeyle ilgili sunum 9. Uluslararası Bilimsel Çalışmalar Kongresi'nde (UBCAK) gerçekleştirilmiştir: [UBCAK9 pdf](https://www.ubcakcongress.org/ubcak9_tam_metin.pdf)
### Göz Fundus Görüntülerinden Diyabetin Sebep Olduğu Göz Hastalıklarının Tespiti
DEMİRCAN SEMİYE, Ezginci Havva Nur (03.08.2022-05.08.2022), Yayın Yeri: 9. Uluslararası Bilimsel Çalışmalar Kongresi (UBCAK)
<br>Yayın Türü: Ulusal Tam Metin Bildiri (Basılı + Elektronik)
