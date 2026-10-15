# Network Routing Optimization

Bu proje, Bilgisayar Ağları dersi kapsamında ekip çalışması olarak geliştirilmiş bir **ağ yönlendirme ve rota optimizasyonu uygulamasıdır**.

Amaç, bir ağ üzerindeki kaynak ve hedef düğümler arasında yalnızca en kısa yolu bulmak yerine; **gecikme (delay), güvenilirlik (reliability) ve bant genişliği (bandwidth)** gibi farklı ağ kriterlerini birlikte değerlendirerek uygun bir rota belirlemektir.

Projede rota optimizasyonu için iki farklı sezgisel optimizasyon algoritması kullanılmıştır:

- Genetic Algorithm (GA)
- Ant Colony Optimization (ACO)

Uygulama hem rastgele oluşturulan ağ topolojileri üzerinde hem de CSV dosyalarından okunan ağ verileri üzerinde çalışabilmektedir.

---

## Benim Katkım

Bu projede ağırlıklı olarak **algoritma geliştirme ve optimizasyon kısmında** çalıştım.

Özellikle;

- Genetic Algorithm yapısının geliştirilmesi ve düzenlenmesi
- Ant Colony Optimization algoritmasının uygulanması
- Rotaların değerlendirilmesi için fitness / maliyet hesaplamalarının oluşturulması
- Gecikme, güvenilirlik ve bant genişlığı değerlerinin algoritmalara dahil edilmesi
- Algoritmaların farklı ağ yapıları üzerinde test edilmesi
- Elde edilen rotaların karşılaştırılması ve algoritma davranışlarının iyileştirilmesi

konularında çalıştım.

Bu bölüm sayesinde teorik olarak öğrendiğimiz ağ yönlendirme problemlerinin optimizasyon algoritmalarıyla nasıl çözülebileceğini uygulamalı olarak inceleme fırsatı buldum.

---

## Projenin Çalışma Mantığı

Kullanıcı öncelikle bir ağ topolojisi oluşturur veya mevcut CSV verilerini sisteme yükler.

Daha sonra:

1. Kaynak düğüm seçilir.
2. Hedef düğüm seçilir.
3. Kullanılacak optimizasyon algoritması belirlenir.
4. Delay, reliability ve bandwidth kriterleri için ağırlık değerleri girilir.
5. Algoritma olası rotaları değerlendirir.
6. Uygun bulunan rota ağ üzerinde görselleştirilir.

Rota değerlendirilirken yalnızca düğümler arasındaki mesafe değil, ağ bağlantılarının sahip olduğu farklı özellikler de hesaba katılır.

---

## Genetic Algorithm

Genetic Algorithm bölümünde farklı rotalar birer çözüm adayı olarak değerlendirilir.

Algoritmada temel olarak:

- Başlangıç popülasyonu oluşturma
- Fitness hesaplama
- Selection
- Crossover
- Mutation
- Elitism

adımları uygulanmaktadır.

Her rotanın uygunluk değeri gecikme, güvenilirlik ve bant genişlığı değerlerine göre hesaplanır. Daha düşük maliyet üreten rotaların sonraki nesillere aktarılma ihtimali artırılır.

---

## Ant Colony Optimization

Ant Colony Optimization algoritmasında ağ üzerindeki bağlantılar feromon değerleri kullanılarak değerlendirilir.

Karıncalar kaynak düğümden hedef düğüme farklı rotalar oluşturur. Daha uygun sonuç veren bağlantılardaki feromon miktarı artırılırken zaman içerisinde mevcut feromon değerleri azaltılır.

Bu sayede algoritma iterasyonlar ilerledikçe daha uygun rotalara yönelmeye çalışır.

---

## Değerlendirilen Ağ Metrikleri

### Delay

Bir rota üzerindeki bağlantıların gecikme değerleri ve ara düğümlerin işlem süreleri dikkate alınır.

### Reliability

Bağlantıların ve düğümlerin güvenilirlik değerleri rota değerlendirmesine dahil edilir.

### Bandwidth

Bir rota üzerindeki bağlantıların bant genişlığı değerleri değerlendirilerek düşük kapasiteli bağlantıların oluşturduğu maliyet hesaba katılır.

Bu üç kriter kullanıcı tarafından verilen ağırlıklarla birlikte değerlendirilerek rota için toplam bir maliyet değeri oluşturulur.

---

## Ağ Topolojisi

Uygulama iki farklı veri kaynağını desteklemektedir.

### Rastgele Topoloji

NetworkX kullanılarak rastgele ağ topolojileri oluşturulabilir.

Varsayılan olarak 250 düğümlü ağlar üzerinde çalışma yapılabilmektedir.

### CSV Verileri

Projeyle birlikte verilen CSV dosyalarındaki:

- Node
- Edge
- Demand

bilgileri kullanılarak hazır ağ topolojileri de sisteme yüklenebilmektedir.

---

## Görselleştirme

Bulunan rota ağ grafiği üzerinde gösterilmektedir.

Kaynak ve hedef düğümler ile algoritmanın seçtiği ara düğümler görsel olarak ayırt edilebilmektedir.

Projede iki farklı arayüz bulunmaktadır:

- Tkinter tabanlı masaüstü arayüz
- Flask tabanlı web arayüzü

---

## Kullanılan Teknolojiler

- Python
- NetworkX
- NumPy
- Matplotlib
- Flask
- Tkinter
- HTML / JavaScript

---

## Proje Yapısı

```text
network-routing-optimization/
│
├── algorithm/
│   ├── ACOAlgorithm.py
│   ├── GeneticAlgorithm.py
│   └── AlgorithmUtils.py
│
├── generate/
│   ├── ReadData.py
│   └── TopologyGenerator.py
│
├── model/
│   ├── Node.py
│   ├── Link.py
│   └── NetworkGraph.py
│
├── documents/
│   └── Ağ topolojisi ve talep verileri
│
├── templates/
│   └── index.html
│
├── app.py
├── main.py
└── requirements.txt
