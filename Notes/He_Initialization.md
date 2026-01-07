# 🧠 He Initialization (Kaiming Initialization)

---

## 🔹 He Initialization কী?

**He Initialization** হলো একটি **weight initialization technique**,  
যা Neural Network–এর training শুরু করার সময় weight এমনভাবে initialize করে যাতে:

- ReLU-based activation ব্যবহার করলে signal vanish বা explode না করে  
- Backpropagation–এ gradient stable থাকে  
- Deep network দ্রুত converge করে  

📌 এটি **2015 সালে Kaiming He** প্রস্তাব করেন, তাই একে  
**Kaiming Initialization**ও বলা হয়।

---

## 🔹 কেন He Initialization দরকার?

ধরা যাক আমরা **ReLU activation** ব্যবহার করছি।

### ReLU Function:

```text
f(x) = max(0, x)
```

### ❌ সমস্যা (Xavier ব্যবহার করলে):

- ReLU প্রায় **৫০% neuron deactivate** করে দেয়  
- ফলে variance কমে যায়  
- Gradient ধীরে ধীরে vanish করে  

### ✅ He কী করে?

> ReLU–এর কারণে যে variance কমে যায়, সেটাকে compensate করে

---

## 🔹 Mathematical Intuition (সহজভাবে)

একটি neuron ধরি:

```
z = w1x1 + w2x2 + ... + wnxn
```

ধরি:
- Mean(x) = 0
- Var(x) = σ²

Forward pass–এ:

```
Var(z) = n × Var(w) × Var(x)
```

ReLU ব্যবহারের পরে (প্রায় 50% neuron deactivate হয়):

```
Var(a) ≈ 0.5 × Var(z)
```

👉 Xavier–এ:

```
Var(w) = 1/n 
→ Var কমে যায় (কারণ 0.5 × 1/n = 0.5/n)
```

👉 He বলে:

```
Var(w) = 2/n
σ = √(2/n)
→ 0.5 × 2/n = 1/n (যা original input–এর Var–এর সমান)
```

📌 এভাবে ReLU–এর পরেও variance stable থাকে

---

## 🔹 He Initialization Formula

### 🔸 Normal Distribution (He Normal)

```text
W ~ N(0, σ²)
যেখানে σ² = 2/n
বা σ = √(2/n)
```

### 🔸 Uniform Distribution (He Uniform)

```text
W ~ U(-limit, +limit)
যেখানে limit = √(2/n)
```

যেখানে:
- `n = number of input neurons (fan_in)`
- `n_in = number of input neurons`
- `n_out = number of output neurons`

---

## 🔹 He Initialization কখন ব্যবহার করা হয়?

### ✅ Best for:

- **ReLU**
- **Leaky ReLU**
- **ELU**
- **PReLU**
- **GELU** (কখনো কখনো)

### ❌ Not ideal for:

- Sigmoid  
- Tanh  

(এইগুলোর জন্য Xavier ভালো)

---

## 🔹 He vs Xavier (Quick Comparison)

| Feature | Xavier | He |
|---------|--------|-----|
| Designed for | Sigmoid/Tanh | ReLU family |
| Variance formula | 1/n | 2/n |
| Standard deviation | √(1/n) | √(2/n) |
| Handles dead neurons | ❌ | ✅ |
| Deep ReLU networks | ❌ | ✅ |
| Good for Sigmoid | ✅ | ❌ |

---

## 🔹 Practical Code Example

### 🔸 TensorFlow / Keras

```python
from tensorflow.keras.layers import Dense, Conv2D
from tensorflow.keras.initializers import HeNormal, HeUniform

# He Normal (recommended)
model.add(Dense(256, activation='relu',
                kernel_initializer=HeNormal()))

# He Uniform (alternative)
model.add(Dense(128, activation='relu',
                kernel_initializer=HeUniform()))

# Convolutional layer with He initialization
model.add(Conv2D(64, (3, 3), activation='relu',
                 kernel_initializer=HeNormal()))
```

### 🔸 PyTorch

```python
import torch.nn as nn

# He Normal (Kaiming Normal)
layer = nn.Linear(256, 128)
nn.init.kaiming_normal_(layer.weight, nonlinearity='relu')

# He Uniform (Kaiming Uniform)
layer2 = nn.Linear(128, 64)
nn.init.kaiming_uniform_(layer2.weight, nonlinearity='relu')

# For Convolutional layer
conv_layer = nn.Conv2d(3, 64, (3, 3))
nn.init.kaiming_normal_(conv_layer.weight, nonlinearity='relu')
```

### 🔸 NumPy (Manual Implementation)

```python
import numpy as np

n_in = 256
n_out = 128

# He Normal
std = np.sqrt(2.0 / n_in)
weights = np.random.randn(n_in, n_out) * std

# He Uniform
limit = np.sqrt(6.0 / n_in)
weights = np.random.uniform(-limit, limit, (n_in, n_out))

# Using both fan_in and fan_out (more accurate)
std_both = np.sqrt(2.0 / (n_in + n_out))
weights_both = np.random.randn(n_in, n_out) * std_both
```

---

## 🔹 Bias Initialization

সাধারণভাবে bias initialize করা হয়:

```text
bias = 0
```

কখনো কখনো ReLU networks–এ:

```text
bias = 0.01 বা 0.1
```

👉 এটি **dead neuron** এড়াতে সাহায্য করে

---

## 🔹 Comparison: He Normal vs He Uniform

| Aspect | He Normal | He Uniform |
|--------|-----------|-----------|
| Distribution type | Gaussian (normal) | Uniform |
| Computation | Slower (randn) | Faster (uniform) |
| Theoretical backing | Stronger | Good |
| Commonly used | ✅ (recommended) | ⚠️ |
| Default in frameworks | Usually ✅ | Sometimes |

---

## 🔹 Exam / Viva Ready Answer

**He Initialization** হলো এমন একটি weight initialization technique যা **ReLU activation** function–এর জন্য বিশেষভাবে ডিজাইন করা। এটি weight–এর variance `2/n` রাখে যাতে ReLU–এর কারণে যে variance কমে যায় (প্রায় 50%), তা compensate হয়। এর ফলে deep neural network–এ **vanishing বা exploding gradient** সমস্যা কমে যায় এবং network দ্রুত converge করে।

---

## 🔹 One-Line Intuition

> **"He keeps the signal strength stable AFTER ReLU deactivates neurons."**

---

## 🔹 Key Takeaway

| Activation | Best Initialization |
|------------|-------------------|
| Sigmoid | Xavier (1/n) |
| Tanh | Xavier (1/n) |
| ReLU | He (2/n) ✅ |
| Leaky ReLU | He (2/n) |
| ELU | He (2/n) |

---
