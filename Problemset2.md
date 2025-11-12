# 🚀 Birleşik Teknik Analiz: Problem Set 2 & LeetCode (Medium)

> Bu doküman, "AlgoDat 1 - Problemset 2" (Karmaşıklık Analizi) ve LeetCode platformundaki "Medium" seviye iki problemin (Bitwise Aritmetik ve Dinamik Programlama) teknik analizlerini içerir.

---

## 📐 Problem 1: AlgoDat 1 - Problemset 2 Analizleri

### 🔵 Soru 1.a: Ardışık Döngüler Analizi

#### 📝 Problem Tanımı

**Görev:** Aşağıdaki sözde kod parçasının N'ye bağlı olarak asimptotik çalışma zamanını (Big O Notasyonu) belirleyin.

```pseudo
a <- N
b <- 1
i <- 1
while i < N {
    a <- a * N
    b <- b + i
    i <- i + 1
}
for j = 1 bis b {
    i <- [i/j]  // (O(1) bir işlem)
}
```

---

#### ✨ Çözüm Analizi

Bu kod, **birbirini takip eden (sequential)** iki ana bloktan oluşur.

##### 1️⃣ Birinci Blok: While Döngüsü

| Özellik | Değer |
|---------|-------|
| **Başlangıç** | `i = 1` |
| **Bitiş** | `i = N-1` |
| **İterasyon Sayısı** | N-1 kez |
| **İşlem Karmaşıklığı** | O(1) (çarpma, toplama, artırma) |
| **Blok Karmaşıklığı** | **O(N)** |

##### 2️⃣ `b` Değişkeni Analizi

```
b başlangıç değeri = 1
Her adımda b'ye eklenen: 1, 2, 3, ..., (N-1)

b = 1 + (1 + 2 + 3 + ... + (N-1))
b = 1 + Σ(i=1 to N-1) i
b = 1 + [(N-1)·N]/2    (Gauss Toplam Formülü)
b ≈ N²/2               (Asimptotik olarak)
```

> 💡 **Sonuç:** `b` değişkeninin nihai değeri **O(N²)** mertebesindedir.

##### 3️⃣ İkinci Blok: For Döngüsü

| Özellik | Değer |
|---------|-------|
| **Başlangıç** | `j = 1` |
| **Bitiş** | `j = b` (b ≈ O(N²)) |
| **İterasyon Sayısı** | O(N²) kez |
| **İşlem Karmaşıklığı** | O(1) |
| **Blok Karmaşıklığı** | **O(N²)** |

##### 🎯 Toplam Karmaşıklık

```
T(N) = O(Blok 1) + O(Blok 2)
T(N) = O(N) + O(N²)
T(N) = O(N²)  ← Baskın terim
```

> ✅ **Sonuç: O(N²)**

---

### 🔵 Soru 1.b: Sabit Zamanlı Algoritma

#### 📝 Problem Tanımı

**Görev:** Aşağıdaki sözde kod parçasının N'ye bağlı olarak asimptotik çalışma zamanını belirleyin.

```pseudo
a <- N^2
c <- N
while c > 1 {
    a <- a + c
    c <- c - N/4
}
while a > N^2 {
    a <- sqrt(a)
}
```

---

#### ✨ Çözüm Analizi

##### 1️⃣ Birinci Blok: While `c > 1`

**Döngü İterasyonları:**

| İterasyon | c Değeri | Durum |
|-----------|----------|-------|
| 0 | N | Başlangıç |
| 1 | N - N/4 = 3N/4 | c > 1 ✓ |
| 2 | 3N/4 - N/4 = 2N/4 | c > 1 ✓ |
| 3 | 2N/4 - N/4 = N/4 | c > 1 ✓ |
| 4 | N/4 - N/4 = 0 | c ≤ 1 ✗ |

> 💡 **Sonuç:** Döngü **sabit 4 kez** çalışır → **O(1)**

##### 2️⃣ `a` Değişkeni Analizi

```
a başlangıç = N²

Birinci döngüde a'ya eklenenler:
N + 3N/4 + 2N/4 + N/4 = N + (3N + 2N + N)/4 = N + 6N/4 = 2.5N

Döngü sonunda:
a = N² + 2.5N
```

##### 3️⃣ İkinci Blok: While `a > N²`

**Kontrol:**
- Giriş: `a = N² + 2.5N`
- Koşul: `N² + 2.5N > N²` → **DOĞRU** (ilk iterasyon çalışır)

**İlk İterasyon:**
```
a = √(N² + 2.5N)

N ≥ 2 için:
√(N² + 2.5N) < N²

Örnek (N=2): √(4+5) = 3, ama N²=4
3 > 4? → YANLIŞ
```

> 💡 **Sonuç:** İkinci döngü **tam 1 kez** çalışır → **O(1)**

##### 🎯 Toplam Karmaşıklık

```
T(N) = O(Blok 1) + O(Blok 2)
T(N) = O(1) + O(1)
T(N) = O(1)
```

> ✅ **Sonuç: O(1)** - N'ye bağlı olmayan sabit zamanlı algoritma!

---

### 🔵 Soru 1.c: Fibonacci Rekürsif - Yerine Koyma Yöntemi

#### 📝 Problem Tanımı

**Görev:** Fibonacci serisindeki bir sayıyı bulan rekürsif fonksiyonun çalışma zamanını **Yerine Koyma Yöntemi** (Substitution Method) ile belirleyin.

**Rekürsif Fonksiyon:**
$$T(n) = T(n-1) + T(n-2) + c$$

*(c = O(1), temel işlemler için sabit zaman)*

---

#### ✨ Çözüm Analizi

##### 1️⃣ Tahmin (Hypothesis)

> 🎯 **Tahmin:** T(n) = O(2ⁿ)
> 
> **İspat Hedefi:** T(n) ≤ k·2ⁿ (k bir sabit)

##### 2️⃣ Yerine Koyma Adımları

**Başlangıç:**
```
T(n) = T(n-1) + T(n-2) + c
```

**Hipotezi Uygula:**
```
T(n) ≤ [k·2^(n-1)] + [k·2^(n-2)] + c
```

**Düzenleme:**
```
T(n) ≤ k·(2^(n-1) + 2^(n-2)) + c
T(n) ≤ k·(2·2^(n-2) + 1·2^(n-2)) + c
T(n) ≤ k·(3·2^(n-2)) + c
```

**2ⁿ Cinsinden Yazalım:**
```
T(n) ≤ k·(3/4)·4·2^(n-2) + c
T(n) ≤ k·(3/4)·2²·2^(n-2) + c
T(n) ≤ (3/4)k·2ⁿ + c
```

##### 3️⃣ Doğrulama

**Hedef:** T(n) ≤ k·2ⁿ

**Kontrol:**
```
(3/4)k·2ⁿ + c ≤ k·2ⁿ
c ≤ k·2ⁿ - (3/4)k·2ⁿ
c ≤ (1/4)k·2ⁿ
```

> ✅ **Sonuç:** k ≥ 4c seçildiğinde, n ≥ 1 için her zaman doğrudur.

##### 📊 Özet

| Metod | Sonuç |
|-------|-------|
| **Yerine Koyma** | T(n) = O(2ⁿ) |
| **İspat Durumu** | ✓ Doğrulandı |
| **k Sabiti** | k ≥ 4c |

---

## 💻 Problem 2: Sum of Two Integers (LeetCode 371)

### ❓ Problem Tanımı

**Görev:** İki tamsayı `a` ve `b` verildiğinde, **`+` ve `-` operatörlerini kullanmadan** toplamlarını döndürün.

#### 📝 Örnek

```
Girdi:  a = 2, b = 3
Çıktı:  5

Girdi:  a = 1, b = 1
Çıktı:  2
```

---

### ✨ Çözüm Analizi

```cpp
int getSum(int a, int b) {
    while (b != 0) {
        // sum: Taşıma (carry) olmadan toplama
        int sum = a ^ b; 
        
        // carry: Sadece taşıma bitlerini hesapla
        int carry = (unsigned int)(a & b) << 1; 
        
        // Bir sonraki iterasyon için değerleri güncelle
        a = sum;
        b = carry;
    }
    return a;
}
```

#### 🔍 Algoritma Mantığı

Bu kod, **Full Adder** (Tam Toplayıcı) devre mantığını simüle eder.

##### 1️⃣ XOR İşlemi: `sum = a ^ b`

**Taşımasız Toplama**

| a | b | a ^ b | Açıklama |
|---|---|-------|----------|
| 0 | 0 | 0 | 0 + 0 = 0 |
| 0 | 1 | 1 | 0 + 1 = 1 |
| 1 | 0 | 1 | 1 + 0 = 1 |
| 1 | 1 | 0 | 1 + 1 = 10 (0 yaz, 1 taşı) |

> 💡 XOR sadece "toplam" bitini verir, taşımayı göz ardı eder.

##### 2️⃣ AND + Shift: `carry = (unsigned int)(a & b) << 1`

**Taşıma Hesaplama**

```
a & b  → Her iki biti 1 olan pozisyonlar (taşıma oluşur)
<< 1   → Taşıma bir sonraki basamağa gider
```

| a | b | a & b | (a & b) << 1 |
|---|---|-------|--------------|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 1 | 1 | 10 (2 desimal) |

> 💡 `(unsigned int)` cast'i negatif sayılar ve overflow için güvenlik sağlar.

##### 3️⃣ Döngü Mantığı

```
while (b != 0) {
    // b = 0 olana kadar (taşıma kalmayana kadar)
    a = eldesiz toplam
    b = taşıma bitleri
}
```

#### 📊 Örnek Çalıştırma

**a = 5 (101), b = 3 (011)**

| İterasyon | a (binary) | b (binary) | a ^ b | a & b | (a&b)<<1 |
|-----------|------------|------------|-------|-------|----------|
| 0 | 101 (5) | 011 (3) | 110 | 001 | 010 |
| 1 | 110 (6) | 010 (2) | 100 | 010 | 100 |
| 2 | 100 (4) | 100 (4) | 000 | 100 | 1000 |
| 3 | 000 (0) | 1000 (8) | 1000 | 000 | 0 |
| Sonuç | **1000 (8)** | 0 | - | - | - |

> ✅ Sonuç: 5 + 3 = **8** ✓

#### 📊 Karmaşıklık Analizi

| Tür | Değer | Açıklama |
|-----|-------|----------|
| ⏱️ **Zaman** | O(1) | En fazla 32 bit (int) veya 64 bit (long) için sabit |
| 💾 **Alan** | O(1) | Sadece `sum` ve `carry` değişkenleri |

> 💡 **Not:** Bit sayısı sabit olduğundan (32/64), N'ye bağlı değil!

---

## 🎯 Problem 3: Maximum Subarray (LeetCode 53)

### ❓ Problem Tanımı

**Görev:** `nums` tamsayı dizisi verildiğinde, toplamı en büyük olan **bitişik** (contiguous) alt diziyi bulun ve bu toplamı döndürün.

#### 📝 Örnek

```
Girdi:  nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Çıktı:  6

Açıklama:
Alt dizi [4, -1, 2, 1] toplamı = 6 (maksimum)

İndeksler:  0   1   2   3   4   5  6   7   8
Değerler:  -2   1  -3  [4  -1   2  1] -5   4
                       └────────┘
                       Toplam = 6
```

---

### ✨ Çözüm Analizi: Kadane Algoritması

```cpp
int maxSubArray(vector<int>& nums) {
    int maxSum = nums[0];
    int currentSum = nums[0];

    for (int i = 1; i < nums.size(); i++) {
        // 1. O anki elemanla devam eden en iyi toplamı güncelle
        currentSum = max(nums[i], currentSum + nums[i]);
        
        // 2. Global olarak bulunan en iyi toplamı güncelle
        maxSum = max(maxSum, currentSum);
    }

    return maxSum;
}
```

#### 🔍 Algoritma Mantığı

##### 📌 Değişkenler

| Değişken | Anlamı |
|----------|--------|
| `maxSum` | Şimdiye kadar bulunan en büyük toplam (global) |
| `currentSum` | Bu indekste **biten** en büyük alt dizi toplamı |

##### 🎯 Kritik Karar: `currentSum = max(nums[i], currentSum + nums[i])`

**İki Seçenek:**

1. **`nums[i]`** → Yeni bir alt dizi başlat
   - Önceki toplam çok kötüyse (negatif/küçük)
   - Mevcut eleman tek başına daha iyi

2. **`currentSum + nums[i]`** → Mevcut alt diziye devam et
   - Önceki toplam pozitif/faydalıysa
   - Eklemeye devam etmek daha karlı

#### 📊 Örnek Çalıştırma

**nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]**

| i | nums[i] | currentSum Öncesi | Karar | currentSum | maxSum |
|---|---------|-------------------|-------|------------|--------|
| 0 | -2 | - | Başlangıç | -2 | -2 |
| 1 | 1 | -2 | max(1, -2+1=-1) | **1** | 1 |
| 2 | -3 | 1 | max(-3, 1-3=-2) | **-2** | 1 |
| 3 | 4 | -2 | max(4, -2+4=2) | **4** | 4 |
| 4 | -1 | 4 | max(-1, 4-1=3) | **3** | 4 |
| 5 | 2 | 3 | max(2, 3+2=5) | **5** | 5 |
| 6 | 1 | 5 | max(1, 5+1=6) | **6** | **6** |
| 7 | -5 | 6 | max(-5, 6-5=1) | **1** | 6 |
| 8 | 4 | 1 | max(4, 1+4=5) | **5** | 6 |

> ✅ **Sonuç: 6** (Alt dizi: [4, -1, 2, 1])

#### 📊 Karmaşıklık Analizi

| Tür | Değer | Açıklama |
|-----|-------|----------|
| ⏱️ **Zaman** | O(N) | Dizi üzerinde tek geçiş (single pass) |
| 💾 **Alan** | O(1) | Sadece iki değişken (maxSum, currentSum) |

---

## 📚 Karşılaştırma Tablosu

| Problem | Kategori | Teknik | Zaman | Alan |
|---------|----------|--------|-------|------|
| **AlgoDat 1.a** | Karmaşıklık Analizi | Ardışık Döngüler | O(N²) | - |
| **AlgoDat 1.b** | Karmaşıklık Analizi | Sabit İterasyon | O(1) | - |
| **AlgoDat 1.c** | Rekürsif İspat | Yerine Koyma | O(2ⁿ) | - |
| **Sum of Two Integers** | Bit Manipulation | XOR + AND | O(1) | O(1) |
| **Maximum Subarray** | Dynamic Programming | Kadane Algoritması | O(N) | O(1) |

---

## 🎓 Önemli Kavramlar

### 🔹 Big O Analizi
- **Ardışık Bloklar:** Karmaşıklıklar toplanır, baskın terim alınır
- **İç İçe Döngüler:** Karmaşıklıklar çarpılır
- **Sabit İterasyon:** N'ye bağlı olmayan → O(1)

### 🔹 Bitwise Operatörler
- **XOR (^):** Taşımasız toplama
- **AND (&):** Taşıma tespiti
- **Left Shift (<<):** Taşımayı kaydırma

### 🔹 Dinamik Programlama
- **Kadane:** Optimal alt yapı + memoization
- **Greedy seçim:** Her adımda en iyi karar

---

*Son güncelleme: 2025*