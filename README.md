# Medical Appointment No-Show Prediction

Bu projede, bir hastanın daha önce planlanmış bir randevuya gelip gelmeyeceğini tahmin etmek amaçlanmıştır. Bu amaçla hem **gözetimli öğrenme** (sınıflandırma algoritmaları) denenmiştir.
---

## 🔍 Problem Tanımı

Bir kişinin randevuya gelip gelmeyeceği, yani `No-show` değişkeni hedef alınarak sınıflandırma yapılması istenmektedir.

### Kullanılabilecek Modeller

**Gözetimli Öğrenme (Sınıflandırma):**
- Logistic Regression
- Decision Tree
- Random Forest
- Naive Bayes
- SVM (Support Vector Machine)
- XGBClassifier

**Gözetimsiz Öğrenme (Kümeleme):**
- K-Means Clustering
- DBSCAN (Density-Based Spatial Clustering of Applications with Noise)

---

## 📑 Veri Seti Özellikleri

Veri seti aşağıdaki değişkenleri içermektedir:

- `PatientId`
- `AppointmentID`
- `Gender`
- `ScheduledDay`
- `AppointmentDay`
- `Age`
- `Neighbourhood`
- `Scholarship`
- `Hipertension`
- `Diabetes`
- `Alcoholism`
- `Handcap`
- `SMS_received`
- `No-show` (Target)

Toplamda hedef değişken ile birlikte **14 öznitelik** yer almaktadır.

### Notlar:
- `Age` nümerik bir değişkendir.
- Diğer sayısal görünümlü değişkenler aslında kategoriktir.
- `ScheduledDay` ve `AppointmentDay` object tipinde olsalar da **tarih** tipine çevrilmelidir.

---

## 🧹 Veri Ön İşleme

Modelin doğru çalışabilmesi için aşağıdaki işlemler gerçekleştirilmiştir:

- `PatientId` ve `AppointmentID` gibi anlamlı bilgi taşımayan değişkenler çıkarıldı.
- `ScheduledDay` ve `AppointmentDay` sütunları `pd.to_datetime()` ile tarih formatına çevrildi.
- Tarih değişkenlerinden **yıl, ay, gün** gibi özellikler türetildi.
- **One-Hot Encoding** ve **Rare Encoding** uygulandı.
- Dengesiz veri problemi tespit edildi (`No-show=1` oranı %20).

---

## ⚙️ Modelleme ve Değerlendirme

Model seçiminde aşağıdaki noktalar dikkate alınmıştır:

- **Random Forest** modeli tercih edilmiştir (ensemle yöntem ve dengesiz verilerde daha dayanıklı).
- **SVC** modeli veri büyüklüğü nedeniyle tercih edilmemiştir.
- Modelin genelleme başarısını ölçmek için:
  - **K-Fold Cross Validation**
  - **GridSearchCV** ve **RandomizedSearchCV** uygulanmıştır.
- Değerlendirme metrikleri olarak:
  - **F1 Score**
  - **ROC-AUC** skorları dikkate alınmıştır.

### Kullanılan Değerlendirme Araçları:
- `classification_report`
- `confusion_matrix`

---

## ⚠️ Dengesiz Veri Problemi

Veri seti ciddi bir dengesizlik içermektedir:
- `No-show = 0`: %80
- `No-show = 1`: %20

Bu dengesizlik modellerin yanlı sonuçlar üretmesine neden olabilir.

### Örnek:
> 1000 köpek, 10 kedi resmiyle eğitilen bir model, yeni bir resme “köpek” deme eğiliminde olur. Çünkü veri dengesizdir.

### Çözüm Önerileri:
- **Undersampling** (baskın sınıftan veri silmek)
- **Oversampling** (azınlık sınıfına sentetik örnekler eklemek - SMOTE vb.)

---

## 📌 Sonuç ve Gelecek Çalışmalar

- Veri seti dengesiz olduğu için modeller istenilen başarıyı göstermemiştir.
- Aşağıdaki geliştirmeler yapılabilir:
  - Daha dengeli veri dağılımı için **SMOTE**, **ADASYN**, **RandomUnderSampler** gibi yöntemler denenebilir.
  - `Appointment_Year`, `Appointment_Minute` gibi yeni değişkenler türetilebilir.
  - `Neighbourhood` gibi **rare** (az tekrar eden) kategoriler sadeleştirilebilir veya yeniden encoding yapılabilir.
  - Dengeleme sonrası modeller yeniden eğitilerek karşılaştırılabilir.

---

## 🔗 Bağlantılar

- Kaggle Notebook: [Medical Appointment No-Show - Kaggle](https://www.kaggle.com/code/emreustubec/medical-appointment-no-show/notebook)

---

## 👨‍💻 Geliştirici

**Emre Üstübeç**  
📧 emresb1999@gmail.com  
📌 GitHub: [@UstubecEmre](https://github.com/UstubecEmre)

---
