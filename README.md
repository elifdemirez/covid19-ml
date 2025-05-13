# 🦠 COVID-19 Severity Prediction using Logistic Regression & Hyperparameter Tuning

> Kaggle Notebook: [🔗 View on Kaggle](https://www.kaggle.com/code/YOUR_USERNAME/covid19-severity-logistic-regression)  
> Author: YOUR NAME  
> Date: May 2025

---

## 🎯 Problem Tanımı

Bu projede, COVID-19 veri kümesi kullanılarak ülkelerin son raporlanan değerlerine göre **“şiddetli salgın yaşayan”** ülkelerin sınıflandırılması amaçlanmıştır. 
Bir ülkenin COVID-19 durumunun şiddetli olup olmadığını, **"ölüm sayısının vaka sayısına oranının %5’ten büyük olması"** kriteriyle belirledik. Bu kriter üzerinden bir ikili sınıflandırma problemi kurulmuştur.

---

## 🔍 Neden Logistic Regression?

Bu projede birden fazla algoritma denemek yerine, doğrudan **Logistic Regression** algoritması üzerinde hiperparametre optimizasyonu uygulanarak en iyi sonuçlara ulaşılması hedeflenmiştir.  
Bu yaklaşımı tercih etme nedenlerimiz:

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
  [[26  1]
   [ 5  9]]
  ```
- **Classification Report:**
  ```
                precision    recall  f1-score   support

             0       0.84      0.96      0.90        27
             1       0.90      0.64      0.75        14

        accuracy                           0.84        41
       macro avg       0.87      0.80      0.82        41
    weighted avg       0.85      0.84      0.83        41
  ```

### 🔥 Korelasyon Matrisi

Girdi değişkenleri arasında yüksek korelasyon gözlenmemiştir. Bu, Logistic Regression için uygun bir ortam sağlar.

---

## 🌍 Gerçek Hayatta Uygulama Alanı

Bu tür bir sınıflandırıcı model:

- Hangi ülkelerin COVID-19 bakımından **riskli/severe** durumda olduğunu belirlemede
- Kaynak ve sağlık hizmetlerinin **önceliklendirilmesinde**
- Erken uyarı sistemleri geliştirmede
- Epidemiyolojik analiz ve sağlık politikası belirlemede

kullanılabilir.

---

## 🚀 Geliştirme Fikirleri

- 🌐 Ülke nüfusu, sağlık sistemi kapasitesi gibi ek demografik verilerle zenginleştirme
- 📈 Zaman serisi tahmin modelleri (LSTM, Prophet) ile vaka/ölüm sayılarının gelecekteki değerlerini öngörme
- 🧠 Ensemble modeller (Random Forest, XGBoost) ile daha güçlü modeller inşa etme
- 🌍 Coğrafi analizler ile vaka dağılımının harita üzerinde görselleştirilmesi

---

## 🛠️ Gereksinimler

- Python 3.7+
- pandas, numpy, matplotlib, seaborn
- scikit-learn

```bash
pip install -r requirements.txt
```

---

## 📌 Projeyi Çalıştırmak

1. Veriyi indirin: [Kaggle Dataset](https://www.kaggle.com/datasets/imdevskp/corona-virus-report)
2. Dosya yolunu güncelleyin.
3. `covid_severity_model.py` dosyasını çalıştırın.

---

## 📎 Lisans

Bu proje yalnızca eğitim ve araştırma amaçlıdır.