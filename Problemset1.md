# 🎯 Birleşik Teknik Analiz: Problem Set 1 & LeetCode Dizileri

> Bu doküman, "Problem Set 1" (Karmaşıklık ve İspat) ve LeetCode (Dizi Manipülasyonu) alıştırmalarının problem tanımlarını, teknik analizlerini ve çözümlerini içerir.

---

## 📊 Problem 1: Asimptotik Çalışma Zamanı (Big O) Analizi

### ❓ Soru (Aufgabe 1)

**Görev:** Aşağıda verilen Java program parçalarının, **N değişkenine bağlı olarak** asimptotik çalışma zamanını (Big O Notasyonu) belirleyin.

---

### 🔵 a) Kod Parçası

```java
int sum = 0;
int X = 100000;
for (int i = 1; i <= 4 * N; i++) {
    for (int j = 1; j <= X + 2; j++) {
        sum++;
    }
    for (int j = 1; j <= X * 100; j++) {
        for (int k = 1; k <= X * X; k++) {
            sum++;
        }
    }
    sum++;
}
System.out.println(sum);
```

#### ✨ Çözüm Analizi

| Bileşen | Açıklama | Karmaşıklık |
|---------|----------|-------------|
| **Dış Döngü** | `4 * N` kez çalışır | O(N) |
| **X Değişkeni** | Sabit bir değer (100000) | O(1) |
| **İç Blok 1** | `X + 2` kez çalışır (N'ye bağlı değil) | O(1) |
| **İç Blok 2** | İç içe döngüler, ama X sabite bağlı | O(1) |

**Hesaplama:**
- Dış döngü: O(N) kez döner
- İçerideki tüm işlemler: O(1) + O(1) + O(1) = O(1)
- **Toplam:** O(N) × O(1) = **O(N)**

> ✅ **Sonuç: O(N)**

---

### 🔵 b) Kod Parçası

```java
int sum = 0;
for (int j = 0; j < 100 * N; j++) {
    for (int i = N; i > 0; i /= 2) {
        sum++;
    }
}
System.out.println(sum);
```

#### ✨ Çözüm Analizi

| Bileşen | Açıklama | Karmaşıklık |
|---------|----------|-------------|
| **Dış Döngü** | `100 * N` kez çalışır | O(N) |
| **İç Döngü** | Her adımda `i /= 2` (N → N/2 → N/4 → ... → 1) | O(log N) |

**Hesaplama:**
- İç içe döngüler (nested loops)
- **Toplam:** O(N) × O(log N) = **O(N log N)**

> ✅ **Sonuç: O(N log N)**

---

### 🔵 c) Kod Parçası

```java
int sum = 0;
for (int j = 0; j < 100 * N; j++) {
    for (int i = N; i > 0; i /= 2) {
        sum++;
    }
}
for (int j = 0; j < 100 * N; j++) {
    for (int i = N; i > 0; i /= 2) {
        sum++;
    }
}
System.out.println(sum);
```

#### ✨ Çözüm Analizi

Bu kod, **(b) şıkkındaki bloğun iki kez ardışık çalıştırılmasıdır.**

| Bileşen | Karmaşıklık |
|---------|-------------|
| **Blok 1** | O(N log N) |
| **Blok 2** | O(N log N) |

**Hesaplama:**
- Döngüler **ardışık** (sequential), iç içe değil
- O(N log N) + O(N log N) = O(2 · N log N)
- Big O'da sabit çarpanlar atılır

> ✅ **Sonuç: O(N log N)**

---

## 🧮 Problem 2: Tümevarım ile İspat

### ❓ Soru (Aufgabe 2)

**Görev:** Aşağıdaki matematiksel ifadenin **n ≥ 1** tüm pozitif tamsayıları için **matematiksel tümevarım** yöntemiyle doğru olduğunu ispatlayın.

$$\sum_{i=0}^{n} i^3 = \frac{n^2(n+1)^2}{4}$$

---

### ✨ İspat Adımları

#### 1️⃣ Temel Durum (n = 1)

| Taraf | Hesaplama | Sonuç |
|-------|-----------|-------|
| **Sol** | $\sum_{i=0}^{1} i^3 = 0^3 + 1^3$ | 1 |
| **Sağ** | $\frac{1^2(1+1)^2}{4} = \frac{1 \cdot 4}{4}$ | 1 |

> ✅ Sol = Sağ (1 = 1) → Temel durum doğrudur

---

#### 2️⃣ Tümevarım Hipotezi

Formülün **n = k** için doğru olduğunu varsayalım:

$$\sum_{i=0}^{k} i^3 = \frac{k^2(k+1)^2}{4}$$

---

#### 3️⃣ Tümevarım Adımı (n = k+1)

**Hedef:** Formülün n = k+1 için de doğru olduğunu göstermek:

$$\sum_{i=0}^{k+1} i^3 = \frac{(k+1)^2(k+2)^2}{4}$$

**İspat:**

```
Sol taraftan başlayalım:
∑(i=0 to k+1) i³ = [∑(i=0 to k) i³] + (k+1)³

Hipotezi kullanalım:
= [k²(k+1)²/4] + (k+1)³

Paydaları eşitleyelim:
= [k²(k+1)²/4] + [4(k+1)³/4]

Ortak çarpanı çıkaralım:
= [(k+1)² · (k² + 4(k+1))]/4

Parantez içini açalım:
= [(k+1)² · (k² + 4k + 4)]/4

(k² + 4k + 4) = (k+2)² olduğunu görelim:
= [(k+1)²(k+2)²]/4 ✓
```

> ✅ **Sonuç:** Formül tüm n ≥ 1 tamsayıları için doğrudur!

---

## 💻 Problem 3: Running Sum of 1d Array (LeetCode 1480)

### ❓ Problem Tanımı

**Görev:** `nums` dizisi verildiğinde, her indeksteki değerin o ana kadarki toplamını içeren bir dizi döndürün.

**Formül:** `runningSum[i] = sum(nums[0]…nums[i])`

#### 📝 Örnek

```
Girdi:  nums = [1, 2, 3, 4]
Çıktı:  [1, 3, 6, 10]

Açıklama:
[1,           → 1
 1+2,         → 3
 1+2+3,       → 6
 1+2+3+4]     → 10
```

---

### ✨ Çözüm Analizi

```cpp
vector<int> runningSum(vector<int>& nums) {
    vector<int> totals(nums.size());
    totals[0] = nums[0];
    for (int i = 1; i < nums.size(); i++) {
        totals[i] = totals[i - 1] + nums[i];
    }
    return totals;
}
```

#### 🔍 Algoritma Mantığı

| Adım | Açıklama |
|------|----------|
| **İlklendirme** | `nums` ile aynı boyutta `totals` vektörü oluştur |
| **Temel Durum** | `totals[0] = nums[0]` (ilk eleman aynı kalır) |
| **İterasyon** | Her eleman için: önceki toplam + mevcut eleman |

**💡 Kilit Nokta:** Ön Ek Toplamı (Prefix Sum) tekniği - Her adımda önceki toplamı kullanarak O(1) zamanda hesaplama yapar.

#### 📊 Karmaşıklık Analizi

| Tür | Değer | Açıklama |
|-----|-------|----------|
| ⏱️ **Zaman** | O(N) | Dizi üzerinde tek geçiş |
| 💾 **Alan** | O(N) | N boyutunda yeni vektör |

---

## 🍬 Problem 4: Kids With the Greatest Number of Candies (LeetCode 1431)

### ❓ Problem Tanımı

**Görev:** Her çocuğa `extraCandies` verilirse, o çocuğun en fazla şekere sahip çocuk olup olamayacağını belirleyin.

#### 📝 Örnek

```
Girdi:  candies = [2, 3, 5, 1, 3], extraCandies = 3
Çıktı:  [true, true, true, false, true]

Açıklama:
- Çocuk 1: 2+3 = 5 ≥ 5 (max) → ✓
- Çocuk 2: 3+3 = 6 ≥ 5 (max) → ✓
- Çocuk 3: 5+3 = 8 ≥ 5 (max) → ✓
- Çocuk 4: 1+3 = 4 < 5 (max) → ✗
- Çocuk 5: 3+3 = 6 ≥ 5 (max) → ✓
```

---

### ✨ Çözüm Analizi

```cpp
vector<bool> kidsWithCandies(vector<int>& candies, int extraCandies) {
    vector<bool> result(candies.size(), false);
    int top_candies = 0;
    
    // Geçiş 1: Maksimum şeker sayısını bul
    for(int i = 0; i < candies.size(); i++) {
        if(candies[i] >= top_candies) {
            top_candies = candies[i];
        }
    }
    
    // Geçiş 2: Her çocuk için kontrol et
    for(int i = 0; i < candies.size(); i++) {
        if((candies[i] + extraCandies) >= top_candies) {
            result[i] = true;
        }
    }
    
    return result;
}
```

#### 🔍 Algoritma Mantığı

Bu, verimli bir **iki geçişli (two-pass)** çözümdür:

| Geçiş | Amaç | Karmaşıklık |
|-------|------|-------------|
| **1️⃣ Birinci** | Maksimum şeker sayısını bul | O(N) |
| **2️⃣ İkinci** | Her çocuk için karşılaştırma yap | O(N) |

#### 📊 Karmaşıklık Analizi

| Tür | Değer | Açıklama |
|-----|-------|----------|
| ⏱️ **Zaman** | O(N) | İki bağımsız döngü: O(N) + O(N) = O(2N) ≈ O(N) |
| 💾 **Alan** | O(N) | N elemanlı boolean vektörü |

---

## 📚 Özet Karşılaştırma Tablosu

| Problem | Algoritma Türü | Zaman | Alan | Teknik |
|---------|----------------|-------|------|--------|
| **Running Sum** | Dizi İterasyonu | O(N) | O(N) | Prefix Sum |
| **Kids With Candies** | İki Geçişli Arama | O(N) | O(N) | Max Bulma + Karşılaştırma |
| **Big O Analizi (a)** | Döngü Analizi | O(N) | - | Sabit Faktör İhmal |
| **Big O Analizi (b)** | İç İçe Döngü | O(N log N) | - | Logaritmik İç Döngü |
| **Big O Analizi (c)** | Ardışık Döngüler | O(N log N) | - | Toplama Kuralı |

---

*Son güncelleme: 2025*