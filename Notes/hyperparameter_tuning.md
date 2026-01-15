# Hyperparameter Tuning in Deep Learning

## 1. Hyperparameter কী?

**Hyperparameter** হলো এমন parameter যেগুলো:
- 👉 **training শুরু হওয়ার আগে নির্ধারণ করতে হয়**
- 👉 **model নিজে শিখতে পারে না**

### উদাহরণ:
| | |
|---|---|
| Learning Rate | Batch Size |
| Number of Epochs | Optimizer (SGD, Adam, RMSprop) |
| Number of Hidden Layers | Number of Neurons |
| Dropout Rate | Regularization (L1, L2) |

---

## 2. Parameter vs Hyperparameter

| বিষয়            | Parameter     | Hyperparameter         |
| --------------- | ------------- | ---------------------- |
| কে শেখে         | Model নিজে    | Developer নির্ধারণ করে |
| উদাহরণ          | Weights, Bias | Learning rate          |
| Training-এর সময় | Update হয়     | Fixed থাকে             |

---

## 3. Hyperparameter Tuning কী?

**Hyperparameter Tuning** হলো বিভিন্ন hyperparameter-এর মান পরিবর্তন করে সবচেয়ে ভালো performance (low loss, high accuracy) পাওয়া।

### 🎯 লক্ষ্য:
- Overfitting কমানো
- Faster convergence
- Better generalization

---

## 4. কেন Hyperparameter Tuning গুরুত্বপূর্ণ?

| সমস্যা | ফলাফল |
|--------|--------|
| ❌ ভুল learning rate | Training fail করতে পারে |
| ❌ বেশি epoch | Overfitting |
| ❌ কম epoch | Underfitting |
| ❌ ভুল batch size | Unstable gradient |

> 💡 **একটা ভালো model ≠ শুধু ভালো architecture**  
> **Hyperparameter equally important**

---

## 5. গুরুত্বপূর্ণ Hyperparameters (Deep Learning)

### 5.1 Learning Rate (সবচেয়ে গুরুত্বপূর্ণ)

| স্থিতি | প্রভাব |
|--------|--------|
| 📈 খুব বেশি | Loss explode করে |
| 📉 খুব কম | Training খুব slow |

**📌 সাধারণ মান:**
- Adam: `0.001`
- SGD: `0.01`

---

### 5.2 Batch Size

| ধরন | প্রভাব |
|-----|--------|
| 🔹 Small | Better generalization |
| 🔹 Large | Fast training |

**📌 Common Values:** `16, 32, 64, 128`

---

### 5.3 Number of Epochs

| স্থিতি | সমস্যা |
|--------|--------|
| 📈 বেশি | Overfitting |
| 📉 কম | Underfitting |

💡 **সমাধান:** Early Stopping ব্যবহার করো

---

### 5.4 Optimizer

| নাম | বৈশিষ্ট্য |
|-----|----------|
| SGD | Basic gradient descent |
| Momentum | Fast convergence |
| RMSprop | Adaptive learning rate |
| **Adam** ⭐ | সবচেয়ে জনপ্রিয় |

---

### 5.5 Network Depth & Width

- 📊 **Deep Networks**: Powerful কিন্তু gradient control গুরুত্বপূর্ণ
- 🧠 **Wide Networks**: Higher capacity কিন্তু overfitting রিস্ক

---

### 5.6 Dropout Rate

- 🛡️ **কাজ**: Overfitting কমায়
- 📌 **সাধারণ মান**: `0.2 – 0.5`

---

## 6. Hyperparameter Tuning করার পদ্ধতি

---

## 6.1 Manual Search (সবচেয়ে সহজ)

| বৈশিষ্ট্য | মূল্যায়ন |
|----------|----------|
| পদ্ধতি | নিজে নিজে parameter change করা |
| সুবিধা | Beginner-friendly |
| অসুবিধা | ❌ Time consuming, Large model-এ অকার্যকর |

---

## 6.2 Grid Search

**সব possible combination try করা**

```text
Learning rate: [0.1, 0.01, 0.001]
Batch size: [32, 64]
Total runs = 3 × 2 = 6
```

| ✅ সুবিধা | ❌ অসুবিধা |
|----------|-----------|
| Accurate results | Computationally expensive |
| Systematic search | অনেক সময় লাগে |

---

## 6.3 Random Search (সবচেয়ে ব্যবহারিক)

**Randomly hyperparameter pick করে tuning করা**

| বৈশিষ্ট্য | মূল্যায়ন |
|----------|----------|
| গতি | ✅ Grid search থেকে দ্রুত |
| ফলাফল | প্রায়ই Grid search থেকে ভালো |
| Space explore | ✅ Large space খুব ভালো explore করে |

---

## 6.4 Bayesian Optimization (Advanced) 🧠

**আগের result দেখে পরবর্তী parameter smartly নির্বাচন করা**

| বৈশিষ্ট্য | বর্ণনা |
|----------|--------|
| পদ্ধতি | Intelligent tuning |
| সুবিধা | ✅ অত্যন্ত efficient |
| ব্যবহার | AutoML, Hyperopt, Optuna |

---

## 7. Learning Rate Scheduling (Advanced Tuning) 📊

**Training-এর সময় learning rate smartly পরিবর্তন করা**

### কৌশলগুলো:
- 📉 **Step Decay**: নির্দিষ্ট epoch-এ rate কমানো
- 📉 **Exponential Decay**: exponentially rate কমানো
- 📉 **Reduce on Plateau**: validation loss স্থির হলে কমানো

```python
tf.keras.callbacks.ReduceLROnPlateau()
```

---

## 8. Early Stopping (Smart Tuning) 🛑

**Validation loss বাড়তে শুরু করলে training বন্ধ করা**

```python
tf.keras.callbacks.EarlyStopping(patience=3)
```

**লাভ**: 
- 🎯 Overfitting আটকায়
- ⏱️ Training সময় বাঁচায়
- 💾 সেরা model আপনা save করে

---

## 9. Hyperparameter Tuning Workflow 🔄

1. 📊 **Dataset split**: Train / Validation set তৈরি করো
2. ⚙️ **Initial hyperparameters** সেট করো
3. 🚀 **Train model** করো
4. ✅ **Evaluate** validation set-এ
5. 🔧 **Change hyperparameter** একটি করে
6. 🔁 **Repeat** যতক্ষণ না ভালো result পাও
7. 🏆 **Select best model** সংরক্ষণ করো

---

## 10. Common Mistakes ⚠️

| ভুল | ফলাফল |
|-----|--------|
| ❌ সব hyperparameter একসাথে change করা | Confused results |
| ❌ Validation set না রাখা | Overfitting detect করতে পারবে না |
| ❌ খুব বড় learning rate | Training crash |
| ❌ Overfitting ignore করা | Poor generalization |

---

## 11. Best Practices ✅

| টিপস | সুবিধা |
|------|--------|
| 🔹 One hyperparameter at a time tune করো | Clear impact দেখতে পারবে |
| 🔹 Learning rate আগে tune করো | সবচেয়ে গুরুত্বপূর্ণ |
| 🔹 Validation loss monitor করো | Overfitting catch করতে পারবে |
| 🔹 Early stopping ব্যবহার করো | Time এবং resource বাঁচায় |
| 🔹 Adam optimizer দিয়ে শুরু করো | বেশিরভাগ সময় সেরা |

---

## 12. Real-Life Analogy 🎯

### 📖 **Exam Preparation**

| Machine Learning | পড়াশোনার পরিকল্পনা |
|-----------------|------------------|
| Study hours | Epochs |
| Reading speed | Learning rate |
| Break time | Regularization / Dropout |
| Revision strategy | Optimizer |

> **সব balance না হলে result ভালো হয় না!**

---

## 13. Summary 📝

✅ **Hyperparameter tuning** Deep Learning-এর মেরুদণ্ড  
✅ **Model performance** অনেকাংশে এর উপর নির্ভর করে  
✅ **Proper tuning** = Faster + Accurate model  
✅ **Smart approach** = Time এবং resource optimize করে

---

