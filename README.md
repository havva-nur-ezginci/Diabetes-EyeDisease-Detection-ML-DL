# Diyabet ve Diyabete Bağlı Göz Hastalıkları Tespiti: Makine ve Derin Öğrenme Yöntemleri
Gerçekleştirilen çalışmada en iyi sınıflandırma sonucu ADASYN sentetik veri artırma yöntemi kullanılarak oluşturulan veri seti VGG16 modeline ADAM optimizasyon yöntemi uygulanarak %86 başarı oranı elde edilmiştir.

Bu proje, diyabetin ve diyabete bağlı göz hastalıklarının tespitini gerçekleştirmek için makine öğrenmesi ve derin öğrenme yöntemlerinin uygulanmasını içermektedir. Çalışma iki ana başlık altında toplanmıştır: diyabet tespiti ve göz hastalığı tespiti.

## 1. Diyabet Tespiti
[Diyabet Tespiti](https://github.com/havva-nur-ezginci/DiyabetTespiti-ve-DiyabeteBagliOlusanGozHastaliklarininTespiti-MakineOgrenmesi-DerinOgrenme/blob/main/Diyabet_Tespiti/DiyabetTahminModelleri.ipynb)

Bu bölümde, Kaggle'dan alınan kan değerleri veri seti kullanılarak çeşitli makine öğrenmesi modelleri ile diyabet tespiti yapılmıştır. Kullanılan modeller ve yöntemler aşağıda listelenmiştir:

Kullanılan Modeller:
- Perceptron
- MLPClassifier
- Karar Ağacı (Decision Tree) (overfitting'i önlemek için max_depth parametresi kullanılmıştır)
- Logistic Regression
- KNeighbors
- Support Vector Classification (SVC)
- Gaussian Naive Bayes
- Random Forest Classifier

Test setinde en yüksek doğruluk oranı %81 ile **Logistic Regression** modelinden elde edilmiştir.

## 2. Göz Hastalığı Tespiti
[Göz Hastalığı Tespiti](https://github.com/havva-nur-ezginci/DiyabetTespiti-ve-DiyabeteBagliOlusanGozHastaliklarininTespiti-MakineOgrenmesi-DerinOgrenme)

Bu bölümde, diyabete bağlı olarak gelişen göz hastalıklarının tespitine odaklanılmıştır. Kaggle'dan alınan [Ocular Disease Recognition](https://www.kaggle.com/datasets/andrewmvd/ocular-disease-recognition-odir5k) veri seti kullanılarak göz hastalıkları tespit edilmiştir.
Tespit Edilen Sınıflar:
- Normal
- Diyabetik Retinopati
- Katarakt
- Glokom

Kullanılan Yöntemler:
- Veri seti, SMOTE ve ADASYN yöntemleriyle artırılmıştır.
- VGG16 ve VGG19 derin öğrenme modelleri, SGD, Adagrad ve Adam optimizerları ile eğitilmiştir.
- Eğitim için Google Colab GPU kullanılmıştır.

# Yayınlar ve Sunumlar
Bu projeyle ilgili sunum 9. Uluslararası Bilimsel Çalışmalar Kongresi'nde (UBCAK) gerçekleştirilmiştir: [UBCAK9 pdf](https://www.ubcakcongress.org/ubcak9_tam_metin.pdf)
### Göz Fundus Görüntülerinden Diyabetin Sebep Olduğu Göz Hastalıklarının Tespiti
DEMİRCAN SEMİYE, Ezginci Havva Nur (03.08.2022-05.08.2022), Yayın Yeri: 9. Uluslararası Bilimsel Çalışmalar Kongresi (UBCAK)
<br>Yayın Türü: Ulusal Tam Metin Bildiri (Basılı + Elektronik)
