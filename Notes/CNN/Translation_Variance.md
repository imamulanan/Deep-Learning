# Translation Variance কী?

## 1️⃣ Translation মানে কী?

**Translation** মানে হলো —
👉 কোনো object-কে **এক জায়গা থেকে আরেক জায়গায় সরানো**
(ডানে, বামে, উপরে, নিচে)

উদাহরণ:

* ছবির মাঝখানে থাকা একটি বিড়ালকে যদি বাম কোণায় সরানো হয় → এটাকে বলে **translation**

---

## 2️⃣ Translation Variance কী?

👉 **Input একটু সরালেই যদি model-এর output অনেক বদলে যায়**,
তাহলে সেটাকে বলে **Translation Variance**।

**Formal Definition:**

> A model is translation variant if a small shift in the input causes a significant change in the output.

---

## 3️⃣ সহজ উদাহরণ (Real-Life)

ধরা যাক:

* CNN model একটা ছবিতে **digit “5”** চিনতে শেখানো হয়েছে

### Case 1:

* “5” ছবির মাঝখানে → Model বলে **5**

### Case 2:

* একই “5” একটু ডান দিকে সরানো → Model বলে **3** 😐

👉 এই behaviour = **Translation Variance**

---

## 4️⃣ CNN কি পুরোপুরি Translation Invariant?

❌ না, CNN পুরোপুরি **translation invariant নয়**
✔️ কিন্তু **partially translation invariant**

---

## 5️⃣ কেন CNN-এ Translation Variance হয়?

### 🔹 1. Fully Connected Layer

* FC layer exact position sensitive
* Feature কোথায় আছে সেটার উপর depend করে

---

### 🔹 2. Stride > 1

* Filter লাফ দিয়ে move করে
* কিছু location skip হয়

---

### 🔹 3. Padding না থাকলে

* Border-এর feature হারিয়ে যায়

---

## 6️⃣ Pooling কীভাবে সাহায্য করে?

### Max Pooling:

* Feature **কোথায় আছে সেটা না দেখে**
* শুধু **আছে কিনা** সেটা দেখে

👉 তাই pooling **translation variance কমায়**

কিন্তু:

> Pooling পুরোপুরি invariant করে না

---

## 7️⃣ Translation Invariance বনাম Translation Variance

| বিষয়             | Translation Invariance | Translation Variance |
| ---------------- | ---------------------- | -------------------- |
| Input shift করলে | Output same থাকে       | Output বদলে যায়      |
| Robustness       | বেশি                   | কম                   |
| Ideal case       | Desired                | Undesired            |
| CNN বাস্তবে      | Partial                | Partial              |

---

## 8️⃣ Mathematical Intuition (সহজভাবে)

ধরা যাক:

* Input = x
* Shifted input = T(x)

যদি,
$$
f(x) \neq f(T(x))
$$

👉 Model **translation variant**

যদি,
$$
f(x) \approx f(T(x))
$$

👉 Model **translation invariant**

---

## 9️⃣ Translation Variance কমানোর উপায়

### ✅ 1. Data Augmentation

* Random shift
* Random crop

---

### ✅ 2. Pooling ব্যবহার

* Max pooling
* Average pooling

---

### ✅ 3. Stride = 1 রাখা

* Small stride = more stability

---

### ✅ 4. Global Average Pooling

* Position dependency কমায়

---

## 🔟 Exam One-Liner

> Translation variance হলো এমন একটি সমস্যা যেখানে input image সামান্য সরালেই model-এর output উল্লেখযোগ্যভাবে পরিবর্তিত হয়।

---

## 🔥 Summary

* Translation variance = position sensitive behavior
* CNN পুরোপুরি invariant নয়
* Pooling & augmentation দিয়ে কমানো যায়
* Object detection-এ variance দরকার
* Classification-এ invariance দরকার

---
