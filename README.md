# 🦠 COVID-19 Severity Prediction using Logistic Regression & Hyperparameter Tuning

> Kaggle Notebook: [🔗 View on Kaggle](https://www.kaggle.com/code/elifnurdemirezen/covid19-ml-project)

---

## 🎯 Problem Tanımı

Bu projede, COVID-19 veri kümesi kullanılarak ülkelerin son raporlanan değerlerine göre **“şiddetli salgın yaşayan”** ülkelerin sınıflandırılması amaçlanmıştır. 
Bir ülkenin COVID-19 durumunun şiddetli olup olmadığını, **"ölüm sayısının vaka sayısına oranının %5’ten büyük olması"** kriteriyle belirledik. Bu kriter üzerinden bir ikili sınıflandırma problemi kurulmuştur.

---

## 🔍 Neden Logistic Regression?

Bu projede birden fazla algoritma denemek yerine, doğrudan **Logistic Regression** algoritması üzerinde hiperparametre optimizasyonu uygulanarak en iyi sonuçlara ulaşılması hedeflenmiştir.  
Bu yaklaşımı tercih etme nedenlerim:

- Logistic Regression, küçük ve iyi tanımlanmış veri setleri için etkili, açıklanabilir ve yorumlanabilir bir modeldir.
- Modelin çıktısı, olasılık tabanlı olduğu için yorumlaması kolaydır.
- Basit ve hızlı bir algoritma olması, hiperparametre arama sürecini verimli hale getirir.
- Verimiz çok büyük ve kompleks olmadığından daha karmaşık modellere gerek duyulmamıştır.

---

## 🧪 Kullanılan Veri Kümesi

- **Adı:** COVID-19 Clean Complete Dataset  
- **Kaynak:** [Kaggle Dataset - COVID-19 Cleaned](https://www.kaggle.com/datasets/imdevskp/corona-virus-report)
- **İçerik:** Günlük bazda ülke/eyalet bazlı COVID-19 vaka, ölüm ve iyileşme sayıları.
- **Kullanılan Özellikler:** `Confirmed`, `Deaths`, `Recovered`
- **Hedef (Label):** `Severe` → (Deaths / Confirmed > 0.05) → 1, aksi takdirde 0

---

## 🧑‍💻 Model Geliştirme Süreci

1. **Veri Temizleme ve Dönüştürme**
   - `Province/State` sütunu kaldırıldı.
   - `Date` sütunu datetime formatına çevrildi.
   - Sadece en güncel tarihli veriler seçildi.

2. **Özellik Mühendisliği**
   - `Severe` isimli bir etiket sütunu oluşturuldu.
   - Girdi özellikleri: `Confirmed`, `Deaths`, `Recovered`

3. **Veri Seti Bölünmesi**
   - Eğitim ve test verileri `train_test_split()` ile ayrıldı (%80 / %20)

4. **Hiperparametre Optimizasyonu**
   - GridSearchCV ile aşağıdaki parametreler optimize edildi:
     - `C`: [0.01, 0.1, 1, 10, 100]
     - `penalty`: ['l1', 'l2']
     - `solver`: ['liblinear', 'saga']

5. **Nihai Model Eğitimi ve Değerlendirme**

---

## 🧠 Nihai Model Detayları

- **Model:** Logistic Regression
- **En iyi parametreler:**
  - `C=0.01`
  - `penalty='l2'`
  - `solver='liblinear'`

---

## ✅ Sonuçlar

### 🎯 Model Başarımı (Test Verisi Üzerinde)

- **Test Accuracy:** 0.84  
- **Confusion Matrix:**
  ```
 [46  0]
 [ 1  6]
 
  ```
- **Classification Report:**
  ```
                 precision    recall  f1-score   support

           0       0.98      1.00      0.99        46
           1       1.00      0.86      0.92         7

    accuracy                           0.98        53
   macro avg       0.99      0.93      0.96        53
weighted avg       0.98      0.98      0.98        53
  ```
-**

---

## 🌍 Gerçek Hayatta Uygulama Alanı

Bu tür bir sınıflandırıcı model:

- Hangi ülkelerin COVID-19 bakımından **riskli/severe** durumda olduğunu belirlemede
- Kaynak ve sağlık hizmetlerinin **önceliklendirilmesinde**
- Erken uyarı sistemleri geliştirmede
- Epidemiyolojik analiz ve sağlık politikası belirlemede

kullanılabilir.

---
