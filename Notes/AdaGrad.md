# AdaGrad (Adaptive Gradient Algorithm)

## 1. ভূমিকা (Introduction)
AdaGrad (Adaptive Gradient Algorithm) হলো Deep Learning ও Machine Learning-এ ব্যবহৃত একটি **optimization algorithm**।  
এর মূল বৈশিষ্ট্য হলো—  
👉 **প্রতিটি parameter-এর জন্য আলাদা learning rate ব্যবহার করা**।

AdaGrad বিশেষভাবে উপযোগী:
- Sparse data (যেমন NLP, text data)
- যেখানে কিছু feature খুব কম update হয়

---

## 2. কেন AdaGrad দরকার?
সাধারণ SGD-তে:
- সব parameter-এর জন্য একই learning rate ব্যবহার করা হয়
- Rare feature এবং frequent feature আলাদা করে handle করা যায় না

👉 AdaGrad এই সমস্যার সমাধান করে।

---

## 3. মূল ধারণা (Core Idea)
AdaGrad:
- যেসব parameter **বারবার update হয়**, তাদের learning rate **কমিয়ে দেয়**
- যেসব parameter **কম update হয়**, তাদের learning rate **বেশি রাখে**

ফলে training আরও balanced হয়।

---

## 4. Mathematical Formulation

### Step–1: Gradient Accumulation
$$
G_t = G_{t-1} + (\nabla L(w_t))^2
$$

এখানে,
- $G_t$ = past squared gradients-এর যোগফল

---

### Step–2: Weight Update
$$
w_{t+1} = w_t - \frac{\eta}{\sqrt{G_t} + \epsilon} \cdot \nabla L(w_t)
$$

যেখানে,
- $\eta$ = initial learning rate  
- $\epsilon$ = small constant (numerical stability-এর জন্য)  
- $G_t$ = accumulated squared gradients  

---

## 5. Intuition (সহজভাবে বোঝা)
- Gradient বড় হলে → learning rate ছোট  
- Gradient ছোট হলে → learning rate বড়  

অর্থাৎ,
> যেটা বেশি শেখা হয়ে গেছে, সেটাকে ধীরে শেখাও  
> যেটা কম শেখা হয়েছে, সেটাকে দ্রুত শেখাও

---

## 6. Exponential Weighted Average এর সাথে পার্থক্য
AdaGrad-এ:
- **Simple sum** of squared gradients ব্যবহার হয়  
- Exponential decay নেই  

এ কারণেই learning rate ধীরে ধীরে খুব ছোট হয়ে যায়।

---

## 7. সুবিধা (Advantages)
- Adaptive learning rate  
- Sparse data-তে খুব ভালো কাজ করে  
- Hyperparameter tuning কম লাগে  
- NLP ও recommendation system-এ কার্যকর  

---

## 8. অসুবিধা (Disadvantages)
- Learning rate দ্রুত খুব ছোট হয়ে যায়  
- Long training-এ model শেখা বন্ধ করে দিতে পারে  
- Deep neural network-এ সব সময় ভালো কাজ করে না  

👉 এই সমস্যার কারণেই RMSProp ও Adam এসেছে।

---

## 9. ব্যবহার ক্ষেত্র (Use Cases)
- Natural Language Processing (NLP)
- Text classification
- Sparse feature problems
- Recommendation systems

---

## 10. Implementation Example

### TensorFlow / Keras
```python
import tensorflow as tf

optimizer = tf.keras.optimizers.Adagrad(
    learning_rate=0.01
)
```

