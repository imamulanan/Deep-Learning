# 🧠 Weight Initialization Techniques (Deep Learning)

## 📌 Weight Initialization কী?

**Weight Initialization** হলো Neural Network ট্রেনিং শুরু করার সময়
প্রতিটি নিউরনের **weight-এর প্রাথমিক মান সেট করা**।

👉 ভুল initialization হলে:

* Gradient Vanishing 🔻
* Gradient Exploding 🔺
* Training খুব ধীরে বা একদমই শেখে না

👉 ভালো initialization হলে:

* দ্রুত Convergence
* Stable Training
* ভালো Accuracy

---

## 🔴 কেন Weight Initialization এত গুরুত্বপূর্ণ?

1. **Symmetry Breaking**

   * সব weight যদি একই হয় → সব neuron একই কাজ করবে
2. **Gradient Flow ঠিক রাখা**

   * খুব বড় weight → exploding gradient
   * খুব ছোট weight → vanishing gradient
3. **Training Speed বাড়ানো**

---

## 🧪 Weight Initialization Techniques

---

## 1️⃣ Zero Initialization

```text
W = 0
```

### ❌ সমস্যা:

* সব neuron একই output দেয়
* **Symmetry Problem**

### ❌ ব্যবহার করা উচিত নয় (Hidden Layer)

✔️ শুধুমাত্র bias = 0 রাখা যায়

---

## 2️⃣ Random Initialization

```text
W ~ Random(-0.01, 0.01)
```

### ✅ সুবিধা:

* Symmetry ভাঙে

### ❌ সমস্যা:

* খুব ছোট → Vanishing Gradient
* খুব বড় → Exploding Gradient

---

## 3️⃣ Xavier Initialization (Glorot)

### 📐 Formula:

```text
W ~ N(0, 1 / n)
```

অথবা

```text
W ~ Uniform( -√(1/n), +√(1/n) )
```

যেখানে
`n = number of input neurons`

### 🎯 কোথায় ব্যবহার হয়?

* **Sigmoid**
* **Tanh**

### 🧠 ধারণা:

Input ও Output variance সমান রাখে

---

## 4️⃣ He Initialization (Kaiming)

### 📐 Formula:

```text
W ~ N(0, 2 / n)
```

### 🎯 কোথায় ব্যবহার হয়?

* **ReLU**
* **Leaky ReLU**

### 🧠 কেন ReLU-এর জন্য ভালো?

* ReLU অনেক neuron deactivate করে
* তাই variance একটু বেশি রাখা লাগে

---

## 5️⃣ LeCun Initialization

### 📐 Formula:

```text
W ~ N(0, 1 / n)
```

### 🎯 কোথায় ব্যবহার হয়?

* **SELU Activation**

### 🧠 Self-normalizing network তৈরি করে

---

## 6️⃣ Orthogonal Initialization

### ধারণা:

* Weight matrix কে **orthogonal matrix** হিসেবে initialize করা

### 🎯 সুবিধা:

* Gradient stable থাকে
* Deep RNN / CNN এ ভালো কাজ করে

---

## 7️⃣ Constant Initialization

```text
W = c (যেমন 0.1)
```

### ❌ সমস্যা:

* Symmetry problem
* Deep network এ ব্যবহার অনুপযুক্ত

---

## 🔁 Activation অনুযায়ী Best Initialization

| Activation Function | Best Initialization |
| ------------------- | ------------------- |
| Sigmoid             | Xavier              |
| Tanh                | Xavier              |
| ReLU                | He                  |
| Leaky ReLU          | He                  |
| SELU                | LeCun               |

---

## 🧩 Keras / TensorFlow উদাহরণ

```python
from tensorflow.keras.initializers import HeNormal, GlorotNormal

# He Initialization (ReLU)
Dense(128, activation='relu', kernel_initializer=HeNormal())

# Xavier Initialization
Dense(128, activation='tanh', kernel_initializer=GlorotNormal())
```

---