# Adam Optimizer (Adaptive Moment Estimation) – Deep Learning

## 1. ভূমিকা (Introduction)
Adam Optimizer এর পূর্ণরূপ হলো **Adaptive Moment Estimation**।  
এটি Deep Learning-এ সবচেয়ে জনপ্রিয় ও শক্তিশালী optimization algorithm গুলোর একটি।

Adam মূলত **Momentum** এবং **RMSprop** — এই দুইটি ধারণাকে একসাথে ব্যবহার করে:
- Gradient-এর গতি (Momentum)
- Gradient-এর আকার অনুযায়ী adaptive learning rate (RMSprop)

ফলে Adam খুব দ্রুত, stable এবং efficient training নিশ্চিত করে।

---

## 2. Adam কেন দরকার?

### SGD-এর সমস্যা
- Fixed learning rate
- Slow convergence
- Oscillation বেশি

### AdaGrad-এর সমস্যা
- Learning rate খুব দ্রুত ছোট হয়ে যায়
- Long training-এ model শেখা বন্ধ করে দেয়

### RMSprop-এর সীমাবদ্ধতা
- Momentum পুরোপুরি ব্যবহার করে না
- Bias correction নেই

👉 **Adam এই সব সমস্যার সমাধান করে।**

---

## 3. Adam-এর মূল ধারণা (Core Idea)
Adam একই সাথে দুটি জিনিস হিসাব করে:

1. **First Moment (Mean)** → Gradient-এর Exponential Weighted Average  
2. **Second Moment (Variance)** → Gradient² এর Exponential Weighted Average  

এজন্যই নাম:
> **Adaptive Moment Estimation**

---

## 4. Adam-এর ধাপে ধাপে কাজ (Algorithm Steps)

ধরা যাক:
- Gradient = \( g_t = \nabla L(w_t) \)

---

### ধাপ–১: First Moment (Momentum) হিসাব
\[
m_t = \beta_1 m_{t-1} + (1 - \beta_1) g_t
\]

এটি gradient-এর **moving average**।

---

### ধাপ–২: Second Moment (RMSprop) হিসাব
\[
v_t = \beta_2 v_{t-1} + (1 - \beta_2) g_t^2
\]

এটি squared gradient-এর **moving average**।

---

## 5. Bias Correction (খুব গুরুত্বপূর্ণ)
শুরুর দিকে \( m_t \) ও \( v_t \) এর মান ছোট হয় (biased থাকে)।  
এটা ঠিক করার জন্য **bias correction** করা হয়।

### Bias-corrected first moment:
\[
\hat{m}_t = \frac{m_t}{1 - \beta_1^t}
\]

### Bias-corrected second moment:
\[
\hat{v}_t = \frac{v_t}{1 - \beta_2^t}
\]

---

## 6. Final Weight Update Equation
\[
w_{t+1} = w_t - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \cdot \hat{m}_t
\]

---

## 7. Parameter গুলোর ব্যাখ্যা
- \( \eta \) = learning rate (সাধারণত 0.001)
- \( \beta_1 \) = momentum decay (সাধারণত 0.9)
- \( \beta_2 \) = RMSprop decay (সাধারণত 0.999)
- \( \epsilon \) = numerical stability (যেমন: \(10^{-8}\))

---

## 8. Intuition (সহজ ভাষায়)
Adam এমনভাবে কাজ করে যেন:
- কোন direction-এ বেশি যেতে হবে → Momentum দেখে
- কত বড় step নেওয়া যাবে → Gradient² দেখে

👉 তাই update হয়:
- দ্রুত
- smart
- stable

---

## 9. Adam বনাম অন্যান্য Optimizer

| Optimizer | Momentum | Adaptive LR | Bias Correction |
|---------|---------|------------|----------------|
| SGD | ❌ | ❌ | ❌ |
| Momentum | ✅ | ❌ | ❌ |
| AdaGrad | ❌ | ✅ | ❌ |
| RMSprop | ❌ | ✅ | ❌ |
| **Adam** | ✅ | ✅ | ✅ |

---

## 10. Adam-এর সুবিধা (Advantages)
- খুব দ্রুত convergence
- Sparse data-তে ভালো কাজ করে
- Learning rate tuning কম লাগে
- Deep network ও CNN/RNN-এ কার্যকর
- Industry standard optimizer

---

## 11. Adam-এর অসুবিধা (Disadvantages)
- কিছু ক্ষেত্রে generalization কম হতে পারে
- Simple SGD কখনো কখনো better result দেয়
- Memory usage একটু বেশি

---

## 12. Implementation Examples

### TensorFlow / Keras
```python
import tensorflow as tf

optimizer = tf.keras.optimizers.Adam(
    learning_rate=0.001,
    beta_1=0.9,
    beta_2=0.999,
    epsilon=1e-8
)
```

