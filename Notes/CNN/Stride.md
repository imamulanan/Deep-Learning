# Stride কী? (Stride in CNN)

## 1️⃣ Stride কী?

**Stride** হলো
👉 **Convolution filter/kernel প্রতিবার কত ঘর (pixel) লাফ দিয়ে সামনে যাবে**, সেটার পরিমাণ।

সহজ ভাষায়:

> Filter কতটা দূরত্ব রেখে রেখে image-এর উপর slide করবে = **Stride**

---

## 2️⃣ Stride কীভাবে কাজ করে? (Visual Idea)

ধরা যাক:

* Input image: 7 × 7
* Filter: 3 × 3

### 🔹 Stride = 1

```
Filter moves 1 pixel at a time
```

➡️ বেশি output
➡️ বেশি detail capture

---

### 🔹 Stride = 2

```
Filter moves 2 pixels at a time
```

➡️ কম output
➡️ computation কম
➡️ কিছু detail বাদ পড়তে পারে

---

## 3️⃣ Output Size Formula (Stride সহ)

### 📐 General Formula:

$$
\text{Output Size} = \left\lfloor \frac{N - K + 2P}{S} \right\rfloor + 1
$$

### যেখানে:

* **N** = Input size
* **K** = Kernel / Filter size
* **P** = Padding
* **S** = Stride

---

### 🧮 Example 1 (Stride = 1)

Input = 7 × 7
Kernel = 3 × 3
Padding = 0
Stride = 1

$$
\text{Output} = \left\lfloor \frac{7 - 3 + 0}{1} \right\rfloor + 1 = 5
$$

👉 Output = **5 × 5**

---

### 🧮 Example 2 (Stride = 2)

Input = 7 × 7
Kernel = 3 × 3
Padding = 0
Stride = 2

$$
\text{Output} = \left\lfloor \frac{7 - 3}{2} \right\rfloor + 1 = 3
$$

👉 Output = **3 × 3**

---

## 4️⃣ Stride কেন প্রয়োজন?

### 🔹 1. Image Size কমানোর জন্য

Stride বাড়ালে:

* Feature map ছোট হয়
* Downsampling হয়

👉 Pooling ছাড়া size reduce করা যায়

---

### 🔹 2. Computation কমানোর জন্য

* বড় image হলে stride বাড়ালে
* কম convolution লাগে
* Training fast হয়

---

### 🔹 3. Receptive Field বাড়ানোর জন্য

Stride বাড়ালে:

* Filter বড় area cover করে
* Global feature ধরতে সুবিধা হয়

---

## 5️⃣ Stride না বাড়ালে কী সমস্যা?

| সমস্যা             | কারণ             |
| ------------------ | ---------------- |
| Feature map খুব বড় | Stride = 1       |
| Computation বেশি   | বেশি convolution |
| Memory বেশি লাগে   | GPU load         |

---

## 6️⃣ Stride বনাম Padding (Comparison)

| বিষয়        | Stride             | Padding             |
| ----------- | ------------------ | ------------------- |
| কাজ         | Filter কত দূর যাবে | Border-এ pixel যোগ  |
| Output size | Stride বাড়ালে কমে  | Padding বাড়ালে বাড়ে |
| Purpose     | Downsampling       | Edge preserve       |

---

## 7️⃣ Real-Life Example (সহজভাবে)

📷 ধরো তুমি একটা ছবি zoom করে দেখছো:

* **Stride = 1** → ধীরে ধীরে zoom → সব detail দেখা যায়
* **Stride = 2** → লাফ দিয়ে zoom → কিছু detail miss হয়

---

## 8️⃣ Common Stride Values

| Stride | ব্যবহার                    |
| ------ | -------------------------- |
| 1      | Detail feature extraction  |
| 2      | Downsampling               |
| ≥3     | Rare (information loss হয়) |

---

## 9️⃣ Exam-Friendly One-Liner

> Stride হলো CNN-এ filter/kernel প্রতিবার কত pixel দূরত্বে move করবে তা নির্ধারণ করার parameter।

---

## 🔥 Summary

* Stride = step size of convolution
* Stride ↑ → output ↓
* Stride ↓ → detail ↑
* Stride সাধারণত 1 বা 2 হয়

---

