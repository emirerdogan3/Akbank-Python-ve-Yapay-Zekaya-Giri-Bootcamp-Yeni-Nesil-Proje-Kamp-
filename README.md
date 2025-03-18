# Akbank-Python-ve-Yapay-Zekaya-Giri-Bootcamp-Yeni-Nesil-Proje-Kamp-
"Akbank Python ve Yapay Zekaya Giriş Bootcamp: Yeni Nesil Proje Kampı" Projesi

# Sürücüsüz Metro Simülasyonu (Rota Optimizasyonu)

Bu proje, bir metro ağında iki istasyon arasındaki en hızlı ve en az aktarmalı rotaları bulan bir simülasyon uygulamasıdır. Proje, graf veri yapıları ve çeşitli graf algoritmaları kullanılarak geliştirilmiştir.

## Proje Hakkında

Metro Simülasyonu, gerçek dünya problemlerini algoritmik düşünce ile çözmeyi amaçlayan bir projedir. Bu sistem, metro ağını bir graf olarak modelleyerek, yolcuların seyahat planlaması için optimal rotalar sunar.

### Temel Özellikler

- Graf veri yapısı ile metro ağı modellemesi
- BFS (Breadth-First Search) algoritması ile en az aktarmalı rota hesaplama
- A* algoritması ile en hızlı rota hesaplama
- Farklı metro hatları arasında aktarma optimizasyonu
- Çeşitli başlangıç ve hedef noktaları için test senaryoları

## Kullanılan Teknolojiler ve Kütüphaneler

- **Python 3.x**: Temel programlama dili
- **collections.deque**: BFS algoritması için kuyruk veri yapısı sağlar
- **heapq**: A* algoritması için öncelik kuyruğu (priority queue) implementasyonu
- **defaultdict**: Hat-istasyon ilişkilerini yönetmek için varsayılan değerli sözlük yapısı
- **typing**: Kodun okunabilirliğini artırmak için tip belirteçleri (type hints)

## Algoritmaların Çalışma Mantığı

### BFS (Breadth-First Search) Algoritması

BFS algoritması, bir grafta başlangıç noktasından itibaren tüm düğümleri seviye seviye dolaşır. Bu algoritma metro ağında kullanıldığında:

1. Başlangıç istasyonundan başlayarak, komşu istasyonları bir kuyruğa ekler
2. Kuyruktaki istasyonları sırayla ziyaret ederek, ziyaret edilmemiş komşuları keşfeder
3. Her istasyon için o istasyona ulaşmak için gereken rotayı takip eder
4. Hedef istasyona ulaştığında, en az kenar sayısına sahip yolu bulmuş olur

BFS algoritması, en az aktarmalı rotayı bulmak için idealdir çünkü en az kenar (istasyon bağlantısı) sayısına sahip yolu garanti eder.

### A* Algoritması

A* algoritması, başlangıç düğümünden hedef düğüme giden en kısa (veya en düşük maliyetli) yolu bulmak için kullanılan bilgili bir arama algoritmasıdır. Metro ağında:

1. Her istasyon için iki değer hesaplanır:
   - g(n): Başlangıç istasyonundan mevcut istasyona olan maliyet (süre)
   - h(n): Mevcut istasyondan hedef istasyona olan tahmini maliyet
2. f(n) = g(n) + h(n) değeri en düşük olan istasyonu seçer
3. Öncelik kuyruğu kullanarak, her zaman en düşük toplam maliyete sahip istasyonu ziyaret eder
4. Farklı hatlar arasında aktarma durumunda ek maliyet (aktarma cezası) ekler

A* algoritması, en hızlı rotayı bulabilmek için hem kat edilen mesafeyi hem de hedefe olan tahmini mesafeyi göz önünde bulundurur.

### Neden Bu Algoritmaları Kullandık?

- **BFS**: En az aktarmalı rotayı bulmak için BFS en uygun algoritmadır çünkü her bir kenar aynı ağırlığa sahipmiş gibi davranır ve en az kenar sayısıyla hedefine ulaşır.
- **A***: En hızlı rotayı bulmak için A* algoritması, hem şimdiye kadar kat edilen süreyi hem de hedefe olan tahmini süreyi hesaba katarak, en optimal rotayı bulabilir. Ayrıca, hat değişimlerinde ekstra zaman maliyeti ekleyerek daha gerçekçi bir simülasyon sağlar.

## Örnek Kullanım ve Test Sonuçları

Kod, önceden tanımlanmış bir metro ağı ile test senaryoları içerir:

```python
# Metro ağı oluşturma
metro = MetroAgi()

# İstasyon ekleme
metro.istasyon_ekle("K1", "Kızılay", "Kırmızı Hat")
# ...diğer istasyonlar...

# Bağlantı ekleme
metro.baglanti_ekle("K1", "K2", 4)  # Kızılay -> Ulus, 4 dakika
# ...diğer bağlantılar...

# Rota hesaplama
rota = metro.en_az_aktarma_bul("M1", "K4")  # AŞTİ'den OSB'ye
sonuc = metro.en_hizli_rota_bul("M1", "K4")
```

### Test Senaryoları ve Sonuçları

Proje, üç ana test senaryosu içerir:

1. **AŞTİ'den OSB'ye**:
   - En az aktarmalı rota hesaplanır
   - En hızlı rota ve toplam süre hesaplanır

2. **Batıkent'ten Keçiören'e**:
   - Aynı hat üzerindeki istasyonlar arası en kısa rota bulunur

3. **Keçiören'den AŞTİ'ye**:
   - Farklı hatlar üzerinden optimum rota belirlenir
