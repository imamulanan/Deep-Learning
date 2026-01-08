# Padding কী? (Padding in Deep Learning)

## 1️⃣ Padding কী?

**Padding** হলো একটি technique যেখানে **input image বা feature map–এর চারপাশে অতিরিক্ত পিক্সেল যোগ করা হয়** (সাধারণত 0 দিয়ে)।

👉 এটি মূলত **Convolutional Neural Network (CNN)**-এ ব্যবহার করা হয়।

উদাহরণ:

```
Original Image (3×3):
1 2 3
4 5 6
7 8 9

Padding (p = 1):
0 0 0 0 0
0 1 2 3 0
0 4 5 6 0
0 7 8 9 0
0 0 0 0 0
```

---

## 2️⃣ Padding কেন প্রয়োজন?

Padding ছাড়া CNN-এ কিছু বড় সমস্যা দেখা দেয়।

---

### 🔹 Problem 1: Feature map ছোট হয়ে যায়

Convolution করলে image size ধীরে ধীরে **কমে যায়**।

📉 Example:

* Input: 32 × 32
* Filter: 3 × 3
* Stride: 1
  👉 Output: 30 × 30

বারবার convolution করলে:

```
32 → 30 → 28 → 26 → ...
```

❌ এতে **important information হারিয়ে যায়**

---

### 🔹 Problem 2: Edge information হারানো

Padding ছাড়া:

* Filter image-এর **edge বা corner-এ ঠিকমতো কাজ করতে পারে না**
* Middle pixels বেশি গুরুত্ব পায়

Padding দিলে:

* Edge pixels-ও equal importance পায়

---

### 🔹 Problem 3: Deep Network-এ dimension control করা যায় না

Padding ছাড়া:

* Deep CNN বানানো কঠিন
* Feature map খুব দ্রুত shrink হয়ে যায়

Padding দিয়ে:

* Network stable থাকে
* Architecture design সহজ হয়

---

## 3️⃣ Padding না থাকলে কী হয়?

| বিষয়         | Padding ছাড়া  |
| ------------ | ------------- |
| Output size  | দ্রুত ছোট হয়  |
| Edge feature | হারিয়ে যায়    |
| Deep CNN     | বানানো কঠিন   |
| Accuracy     | কমে যেতে পারে |

---

## 4️⃣ Padding এর প্রকারভেদ

### 🔹 1. Valid Padding

* **কোন padding ব্যবহার করা হয় না**
* Default convolution

📌 Formula:

```
Padding = 0
```

📉 Output size কমে যায়

---

### 🔹 2. Same Padding

* Output size ≈ Input size
* সবচেয়ে বেশি ব্যবহৃত

📌 সাধারণ formula:

```
p = (k - 1) / 2   (stride = 1 হলে)
```

Example:

* Kernel size = 3 × 3
* Padding = 1

---

### 🔹 3. Full Padding

* Output size input থেকে বড় হয়
* খুব কম ব্যবহৃত

---

## 5️⃣ Convolution Output Size Formula (সবচেয়ে গুরুত্বপূর্ণ)

### 📐 General Formula:

$$
	ext{Output Size} = \left\lfloor \frac{N - K + 2P}{S} \right\rfloor + 1
$$

### যেখানে,

* **N** = Input size
* **K** = Kernel / Filter size
* **P** = Padding
* **S** = Stride

---

### 🧮 Example:

Input = 7 × 7
Kernel = 3 × 3
Padding = 1
Stride = 1

$$
	ext{Output} = \frac{7 - 3 + 2\times 1}{1} + 1 = 7
$$

👉 Output size = **7 × 7 (Same as input)**

---

## 6️⃣ Same Padding বের করার Formula

Stride = 1 এবং **odd kernel size** হলে:

$$
P = \frac{K - 1}{2}
$$

নোট:
- **Even kernel** হলে `(K - 1)/2` ভগ্নাংশ হয় — বাস্তবে ফ্রেমওয়ার্কগুলো সাধারণত **asymmetric padding** ব্যবহার করে (এক পাশে $\lfloor K/2 \rfloor$, অন্য পাশে $\lceil K/2 \rceil$) যাতে output size input-এর সমান থাকে।
- 2D ক্ষেত্রে height/width-এর জন্য আলাদা padding নেয়া যায়: `P_h`, `P_w`।

Example:

* K = 5 → P = 2
* K = 3 → P = 1

---

## 6.1️⃣ 2D Output Size (Height/Width)

Height/Width আলাদাভাবে হিসাব করা হয়:

$$
	ext{Out}_h = \left\lfloor \frac{N_h - K_h + 2P_h}{S_h} \right\rfloor + 1,\quad
	ext{Out}_w = \left\lfloor \frac{N_w - K_w + 2P_w}{S_w} \right\rfloor + 1
$$

`same` padding (stride = 1) লক্ষ্য: `Out_h = N_h`, `Out_w = N_w`।

---

## 6.2️⃣ Framework Examples

- PyTorch:
  - `Conv2d(..., kernel_size=3, stride=1, padding=1)` → প্রায় `same`
  - নতুন ভার্সনে: `Conv2d(..., kernel_size=3, stride=1, padding='same')`
- TensorFlow/Keras:
  - `Conv2D(filters, kernel_size=3, strides=1, padding='same')`

Even kernel-এর ক্ষেত্রে উভয়েই প্রয়োজনমতো asymmetric padding দেয়।

---

## 7️⃣ Padding বাস্তব জীবনের উদাহরণ (Real-Life Analogy)

🖼️ ধরো তুমি একটি ছবি crop করছো:

* Padding ছাড়া → ছবির চারপাশ কেটে যায়
* Padding সহ → চারপাশে white border দিয়ে মূল ছবি safe রাখা

👉 CNN-এ padding ঠিক এই কাজটাই করে

---

## 8️⃣ Summary (সংক্ষেপে)

| বিষয়           | Padding                               |
| -------------- | ------------------------------------- |
| কাজ            | Input-এর চারপাশে extra pixels যোগ করা |
| উদ্দেশ্য       | Size control + edge feature preserve  |
| সবচেয়ে জনপ্রিয় | Same Padding                          |
| Formula        | (N − K + 2P)/S + 1                    |

---

## 🔥 One-Line Exam Answer

> Padding হলো CNN-এ input image-এর চারপাশে অতিরিক্ত পিক্সেল যোগ করার technique, যার মাধ্যমে output size control করা যায় এবং edge information সংরক্ষণ করা যায়।

---

