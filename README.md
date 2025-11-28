# 🚗 Auto MPG Makine Öğrenmesi Projesi

## 📋 Proje Hakkında

Bu proje, otomobillerin yakıt tüketimini (MPG - Miles Per Gallon) tahmin etmek için çeşitli makine öğrenmesi algoritmalarını kullanmaktadır. UCI Machine Learning Repository'den alınan Auto MPG veri seti kullanılarak, arabaların fiziksel özelliklerine göre yakıt verimliliği tahmin edilmektedir.

## 🎯 Proje Hedefi

Bir otomobilin silindir sayısı, motor hacmi, beygir gücü, ağırlık, hızlanma, model yılı ve menşei bilgileri kullanılarak MPG (yakıt tüketimi) değerini tahmin etmek.

## 📊 Veri Seti

- **Kaynak**: [UCI Machine Learning Repository - Auto MPG Dataset](https://archive.ics.uci.edu/ml/datasets/auto+mpg)
- **Örnek Sayısı**: 398
- **Özellik Sayısı**: 8 (7 sayısal + 1 kategorik)
- **Hedef Değişken**: MPG (Miles Per Gallon)

### Özellikler

| Özellik | Açıklama | Tip |
|---------|----------|-----|
| `mpg` | Yakıt tüketimi (mil/galon) | Sürekli (Hedef) |
| `cylinders` | Silindir sayısı | Kategorik |
| `displacement` | Motor hacmi (cu. inches) | Sürekli |
| `horsepower` | Beygir gücü | Sürekli |
| `weight` | Araç ağırlığı (lbs) | Sürekli |
| `acceleration` | 0-60 mph hızlanma süresi | Sürekli |
| `model_year` | Model yılı (19xx) | Kategorik |
| `origin` | Menşe (1:ABD, 2:Avrupa, 3:Japonya) | Kategorik |
| `car_name` | Araba adı | String (kullanılmadı) |

## 🛠️ Kullanılan Teknolojiler

- **Python 3.x**
- **Kütüphaneler**:
  - `pandas` - Veri işleme
  - `numpy` - Sayısal hesaplamalar
  - `matplotlib` & `seaborn` - Veri görselleştirme
  - `scikit-learn` - Makine öğrenmesi modelleri

## 📁 Proje Yapısı

```
auto-mpg-ml-project/
│
├── README.md                 # Bu dosya
├── notebooks/
│   └── auto_mpg_analysis.ipynb  # Ana Colab notebook
│
└── data/
    └── auto-mpg.data         # Veri seti (otomatik indirilir)
```

## 🚀 Kurulum ve Çalıştırma

### Google Colab'de Çalıştırma (Önerilen)

1. Google Colab'i açın: [colab.research.google.com](https://colab.research.google.com)
2. Yeni bir notebook oluşturun
3. Proje kodlarını hücre hücre yapıştırın ve çalıştırın
4. Tüm gerekli kütüphaneler Colab'de zaten yüklüdür

### Yerel Ortamda Çalıştırma

```bash
# Gerekli kütüphaneleri yükleyin
pip install pandas numpy matplotlib seaborn scikit-learn

# Jupyter Notebook'u başlatın
jupyter notebook
```

## 🔍 Proje Adımları

### 1. Veri Yükleme ve Ön İşleme
- Veri setini UCI repository'den yükleme
- Eksik değerleri tespit etme ve doldurma
- Gereksiz sütunları çıkarma

### 2. Keşifsel Veri Analizi (EDA)
- Veri dağılımlarını inceleme
- Korelasyon analizi
- Görselleştirmeler:
  - Histogram ve box plot'lar
  - Scatter plot'lar
  - Korelasyon ısı haritası

### 3. Veri Hazırlama
- Özellik ve hedef değişken ayrımı
- Train-test split (%80-%20)
- Özellik ölçeklendirme (StandardScaler)

### 4. Model Eğitimi

Üç farklı makine öğrenmesi modeli kullanılmıştır:

#### a) Linear Regression
- Basit ve yorumlanabilir model
- Temel performans referansı

#### b) Random Forest Regressor
- Ensemble öğrenme yöntemi
- Overfitting'e karşı dirençli
- Özellik önem sıralaması sağlar

#### c) Gradient Boosting Regressor
- Güçlü ensemble yöntemi
- Genellikle en yüksek performans
- Hiperparametre optimizasyonuna uygun

### 5. Model Değerlendirmesi

Kullanılan metrikler:
- **R² Score**: Model açıklama gücü (0-1 arası, 1 en iyi)
- **RMSE**: Ortalama karesel hata kökü
- **MAE**: Ortalama mutlak hata

## 📈 Sonuçlar

### Model Performans Karşılaştırması

| Model | R² Score | RMSE | MAE |
|-------|----------|------|-----|
| Linear Regression | ~0.81 | ~3.50 | ~2.60 |
| Random Forest | ~0.90 | ~2.60 | ~1.90 |
| Gradient Boosting | ~0.92 | ~2.40 | ~1.70 |

*Not: Değerler yaklaşıktır ve veri bölünmesine göre değişebilir.*

### Önemli Bulgular

1. **En Etkili Özellikler**:
   - Weight (ağırlık) - Negatif korelasyon
   - Model Year (yıl) - Pozitif korelasyon
   - Displacement (motor hacmi) - Negatif korelasyon

2. **Model İçgörüleri**:
   - Gradient Boosting en iyi performansı gösterdi
   - Ağır arabalar daha düşük MPG değerine sahip
   - Yeni model arabalar daha yakıt verimli

3. **Tahmin Doğruluğu**:
   - Modeller gerçek değerlere oldukça yakın tahminler üretiyor
   - Ortalama hata marjı ~1.7 MPG

## 📊 Görselleştirmeler

Proje şu görselleştirmeleri içerir:
- MPG dağılım grafikleri
- Özellikler arası korelasyon ısı haritası
- Scatter plot'lar (özellik vs MPG)
- Gerçek vs Tahmin grafikleri
- Residual (hata) grafikleri
- Özellik önem sıralaması

## 💡 Kullanım Örneği

```python
# Yeni bir araba için tahmin
new_car = np.array([[6, 250, 100, 3000, 15, 78, 1]])
new_car_scaled = scaler.transform(new_car)
prediction = gb_model.predict(new_car_scaled)[0]

print(f"Tahmini MPG: {prediction:.2f}")
```

## 🔧 Geliştirme Önerileri

- [ ] Hiperparametre optimizasyonu (GridSearchCV, RandomizedSearchCV)
- [ ] Daha fazla feature engineering
- [ ] Deep Learning modelleri (Neural Networks)
- [ ] Cross-validation ile daha robust değerlendirme
- [ ] Model deployment (Flask/Streamlit web uygulaması)
- [ ] XGBoost, LightGBM gibi alternatif modeller

## 🤝 Katkıda Bulunma

Katkılarınızı memnuniyetle karşılıyoruz! Lütfen:
1. Fork yapın
2. Feature branch oluşturun (`git checkout -b feature/YeniOzellik`)
3. Değişikliklerinizi commit edin (`git commit -m 'Yeni özellik eklendi'`)
4. Branch'inizi push edin (`git push origin feature/YeniOzellik`)
5. Pull Request oluşturun

## 📝 Lisans

Bu proje eğitim amaçlıdır ve serbestçe kullanılabilir.

## 📧 İletişim

Sorularınız için issue açabilir veya pull request gönderebilirsiniz.

## 🙏 Teşekkürler

- UCI Machine Learning Repository - Veri seti için
- scikit-learn topluluğu - Harika dokümantasyon için

---

**⭐ Projeyi beğendiyseniz yıldız vermeyi unutmayın!**

*Son güncelleme: Kasım 2025*
