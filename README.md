# Kalabalık Analizi – CSRNet + VGG16

Bu proje, görüntüler içerisindeki insan yoğunluğunu tahmin etmek amacıyla **CSRNet (Congested Scene Recognition Network)** mimarisinin **VGG16** ile güçlendirilmiş bir versiyonunu kullanarak geliştirilmiştir.

Projenin temel amacı, özellikle kalabalık ve yoğun insan gruplarının bulunduğu görüntülerde kişi sayısını ve insan yoğunluğunu daha doğru şekilde tahmin edebilen bir derin öğrenme modeli geliştirmektir.

## Proje Hakkında

Kalabalık sahnelerde tek tek insanları tespit etmek, insanların birbirini kapatması, farklı ölçeklerde görünmeleri ve görüntü içerisindeki yoğunluk nedeniyle oldukça zorlaşabilmektedir.

Bu projede klasik nesne tespit yöntemleri yerine **density map (yoğunluk haritası)** tabanlı bir yaklaşım kullanılmıştır.

Model, görüntü içerisindeki insanların oluşturduğu yoğunluk dağılımını öğrenerek tahmini kişi sayısını elde etmektedir.

Kullanılan temel mimari:

**VGG16 → CSRNet → Density Map → Estimated Crowd Count**

## Kullanılan Teknolojiler

* Python
* PyTorch
* OpenCV
* NumPy
* Matplotlib
* VGG16
* CSRNet
* Deep Learning
* Computer Vision

## Kullanılan Veri Setleri

Projede iki farklı veri seti üzerinde çalışmalar gerçekleştirilmiştir:

* **MALL Dataset**
* **CROWD-UIT Dataset**

Bu veri setleri farklı yoğunluk seviyelerine sahip kalabalık görüntüler içermektedir.

> Veri setlerinin tamamı bu repository içerisinde paylaşılmamıştır.

## Model Mimarisi

Projede CSRNet mimarisinin özellik çıkarma kısmında **VGG16** kullanılmıştır.

Model iki temel bölümden oluşmaktadır:

### 1. Frontend – VGG16

VGG16, görüntülerden temel ve yüksek seviyeli görsel özellikleri çıkarmak için kullanılmıştır.

Bu aşamada model;

* Kenarları
* Şekilleri
* İnsanlara ait görsel özellikleri
* Daha karmaşık görüntü özelliklerini

öğrenmektedir.

### 2. Backend – CSRNet

CSRNet'in dilated convolution yapısı kullanılarak görüntü içerisindeki geniş alanlardan bilgi alınması amaçlanmıştır.

Modelin çıktısı bir **density map** şeklindedir.

Bu yoğunluk haritasının toplamı alınarak görüntü içerisindeki tahmini insan sayısı elde edilmektedir.

## Eğitim

Model PyTorch kullanılarak eğitilmiştir.

Eğitim sürecinde:

* Görüntüler modele uygun şekilde işlenmiştir.
* Density map'ler kullanılmıştır.
* Modelin tahminleri ground truth değerleriyle karşılaştırılmıştır.
* Eğitim performansı MSE ve MAE metrikleri üzerinden değerlendirilmiştir.

Modelin eğitimi sırasında GPU kullanılmıştır.

Kullanılan donanım:

**NVIDIA RTX 3050 – 4 GB VRAM**

## Sonuçlar

Model, farklı kalabalık yoğunluklarına sahip görüntüler üzerinde değerlendirilmiştir.

Elde edilen sonuçlardan bazıları:

| Dataset   |  MSE |  MAE |
| --------- | ---: | ---: |
| MALL      | 0.08 | 0.10 |
| CROWD-UIT | 0.05 | 0.15 |

Bu metrikler, modelin tahmin ettiği yoğunluk haritaları üzerinden hesaplanmıştır.

## Örnek Çıktı

Modelin çalışma süreci genel olarak şu şekildedir:

```text
Input Image
     ↓
VGG16 Feature Extraction
     ↓
CSRNet Backend
     ↓
Density Map
     ↓
Sum of Density Map
     ↓
Estimated Crowd Count
```

## Projenin Öğrenme Çıktıları

Bu proje kapsamında;

* Derin öğrenme modellerinin görüntü işleme problemlerinde kullanılması,
* CNN tabanlı mimarilerin incelenmesi,
* VGG16 mimarisinin özellik çıkarımında kullanılması,
* CSRNet ile crowd counting yaklaşımının uygulanması,
* Density map oluşturma ve yorumlama,
* PyTorch ile model eğitimi,
* GPU üzerinde model çalıştırma,
* Model performansının MSE ve MAE ile değerlendirilmesi

konularında deneyim kazanılmıştır.

## Nasıl Çalıştırılır?

Projeyi bilgisayarınıza klonladıktan sonra gerekli Python paketlerini yükleyebilirsiniz.

```bash
git clone https://github.com/KULLANICI_ADINIZ/kalabalik-analizi.git

cd kalabalik-analizi

pip install -r requirements.txt
```

Daha sonra eğitim veya tahmin dosyası çalıştırılabilir:

```bash
python train.py
```

veya

```bash
python test.py
```

> Dosya isimleri projenin son repository yapısına göre güncellenmelidir.

## Proje Yapısı

```text
kalabalik-analizi/
│
├── README.md
├── requirements.txt
├── train.py
├── test.py
├── model.py
│
├── notebooks/
│
├── results/
│
└── images/
```

## Geliştirici

**Damla Tatlıcan**

İlgi alanları:

* Artificial Intelligence
* Deep Learning
* Computer Vision
* Machine Learning
* Cybersecurity

Bu proje, görüntü işleme ve yapay zeka alanında geliştirdiğim çalışmalar kapsamında hazırlanmıştır.
