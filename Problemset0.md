# 📚 INF203 Problem Set 0: Analiz ve Çözüm Yöntemleri

> Bu doküman, INF203 Algoritmalar ve Veri Yapıları "Problemset 0" içerisinde yer alan problemlerin sözde kod (pseudo-code) analizlerini ve çözüm yaklaşımlarını içermektedir.

---

## 🔄 Problem 1: Basit Döngü Analizi

Problem, bir döngü içindeki iki değişkenin değerlerini takip etmeyi amaçlar.

### 📝 Sözde Kod

```plaintext
1: Variable Loop sei 0 und Variable Multiple sei 0
2: Addiere 1 zu Loop
3: Addiere 3 zu Multiple
4: Falls Loop < 100 gehe zu Zeile 2
5: Ende
```

### 🔍 Analiz

1. Kod, `Loop` ve `Multiple` adında iki değişkeni 0 olarak başlatır.
2. Döngüye girilir. Her döngü adımında `Loop` 1, `Multiple` 3 artar.
3. Bu, `Multiple` değişkeninin her zaman `Loop * 3` değerine eşit olacağı bir ilişki kurar.
4. Koşul `Loop < 100` olarak belirlenmiştir.
5. Döngünün son adımları kritiktir:
   - `Loop = 99` olduğunda, `Multiple = 297` olur. `99 < 100` koşulu **Doğru**'dur. 2. satıra gidilir.
   - `Loop` 100 olur.
   - `Multiple` 300 olur.
   - `Loop < 100` (yani `100 < 100`) koşulu kontrol edilir.
   - Koşul **Yanlış** olduğu için 2. satıra gidilmez ve kod 5. satıra (Ende) geçer.

### ✅ Sonuç

Kod 5. satıra ulaştığında `Multiple` değişkeninin değeri **300**'dür.

---

## 🔤 Problem 2: Metin (String) Manipülasyonu ve Sınır Koşulu

Problem, bir metin değişkeni üzerinde indis (index) kullanarak harf değiştirme işlemi yapan bir döngünün sonucunu analiz etmeyi amaçlar.

### 📝 Sözde Kod

```plaintext
1: Variable Loop sei 0 und Variable Text sei = "ABCDEFG"
2: Addiere 1 zu Loop
3: Tausche Buchstabe auf Position Loop mit Buchstabe auf Position Loop + 2
4: Falls Loop < 4 gehe zu Schritt 2
5: Ende
```

### 🔍 Analiz

1. Döngü koşulu `Loop < 4`'tür. Bu, 3. satırdaki `Tausche` (Değiştir) işleminin `Loop = 1`, `Loop = 2` ve `Loop = 3` için çalışacağı, ancak `Loop = 4` olduğunda çalışmayacağı anlamına gelir.

2. **Adım adım değişken takibi** (Pozisyonların 1'den başladığı varsayılmıştır):

| Adım | Loop | İşlem | Sonuç |
|------|------|-------|-------|
| Başlangıç | 0 | - | `ABCDEFG` |
| 1 | 1 | Text[1] ↔ Text[3] (A ↔ C) | `CBADEFG` |
| 2 | 2 | Text[2] ↔ Text[4] (B ↔ D) | `CDABEFG` |
| 3 | 3 | Text[3] ↔ Text[5] (A ↔ E) | `CDEBAFG` |
| 4 | 4 | Koşul yanlış, döngü biter | `CDEBAFG` |

### ✅ Sonuç

Kod sonlandığında `Text` değişkeninin son hali **"CDEBAFG"** olmalıdır.

> ⚠️ **Not:** "CDEFABG" sonucu, muhtemelen `Loop < 4` koşulunun `Loop <= 4` olarak yorumlanmasından veya `Loop = 3` adımındaki indis takibinden kaynaklanan bir fark olabilir. Bu tür "off-by-one" (bir eksik/fazla) hataları, algoritma takibinde en dikkat edilmesi gereken noktalardır.

---

## 🔢 Problem 3: Fibonacci Serisi - İteratif vs. Rekürsif Çözümler

Problem, Fibonacci serisi için iki farklı algoritmik yaklaşımın (iteratif ve rekürsif) yazılmasını ve bu yaklaşımların verimlilik açısından karşılaştırılmasını istemektedir.

### 🔁 3.a) İteratif (Döngüsel) Çözüm

```pseudo
Algorithmus Fibonacci_Iterativ(n)
  wenn n == 0 dann
    gib 0 zurück
  sonst wenn n == 1 dann
    gib 1 zurück
  sonst
    f0 ← 0
    f1 ← 1
    für i von 2 bis n wiederhole
      f2 ← f0 + f1
      f0 ← f1
      f1 ← f2
    ende für
    gib f1 zurück
```

**💡 Analiz:** Bu algoritma, F(0) ve F(1) değerlerini kullanarak seriyi "aşağıdan yukarıya" (bottom-up) inşa eder. Bir döngü kullanarak `n`'inci değere kadar tüm değerleri sırayla hesaplar.

### 🔄 3.b) Rekürsif (Özyineli) Çözüm

```pseudo
Algorithmus Fibonacci_Rekursiv(n)
  wenn n == 0 dann
    gib 0 zurück
  sonst wenn n == 1 dann
    gib 1 zurück
  sonst
    gib Fibonacci_Rekursiv(n-1) + Fibonacci_Rekursiv(n-2) zurück
```

**💡 Analiz:** Bu algoritma, F(n) = F(n-1) + F(n-2) matematiksel tanımının doğrudan koda dökülmüş halidir. "Yukarıdan aşağıya" (top-down) bir yaklaşım sergiler ve F(0) ile F(1) temel durumlarına ulaşana kadar kendini çağırır.

### ⚡ 3.c) Hız Karşılaştırması

#### 🚀 İteratif: Daha Hızlı
- **Zaman Karmaşıklığı:** O(n) (Doğrusal)
- Algoritma `n`'e kadar bir döngüde çalışır ve her Fibonacci sayısını *yalnızca bir kez* hesaplar.

#### 🐌 Rekürsif: Daha Yavaş
- **Zaman Karmaşıklığı:** O(2^n) (Üssel)
- F(n)'i hesaplamak için F(n-1) ve F(n-2) çağrılır. Bu iki çağrı da kendi alt çağrılarını yapar.
- Örneğin, F(5)'i hesaplarken F(3) değeri birden çok kez hesaplanır. Bu durum, `n` büyüdükçe verimliliği hızla düşürür.

### 💾 3.d) Bellek Kullanımı Karşılaştırması

| Yaklaşım | Alan Karmaşıklığı | Açıklama |
|----------|-------------------|----------|
| **İteratif** | O(1) - Sabit | `n`'in değeri ne olursa olsun, algoritma yalnızca sabit sayıda değişken (`f0`, `f1`, `f2`) kullanır. |
| **Rekürsif** | O(n) - Doğrusal | Her özyineli çağrı, fonksiyon yığınına (call stack) yeni bir çerçeve (frame) ekler. F(n) hesaplaması için `n` derinliğine kadar bir yığın oluşabilir. |

---

## 📊 Özet Karşılaştırma

| Kriter | İteratif | Rekürsif |
|--------|----------|----------|
| Hız | ⚡ Hızlı (O(n)) | 🐌 Yavaş (O(2^n)) |
| Bellek | 💚 Az (O(1)) | 💛 Fazla (O(n)) |
| Okunabilirlik | Orta | Yüksek |
| Uygulama | Pratik kullanım için tercih edilir | Matematiksel tanıma daha yakın |

---

*Son güncelleme: 2025*