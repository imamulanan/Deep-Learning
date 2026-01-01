# Deep Learning-এ RMSprop

## 1. ভূমিকা (Introduction)
RMSprop (Root Mean Square Propagation) হলো Deep Learning-এ বহুল ব্যবহৃত একটি **adaptive learning rate optimization algorithm**।  
এটি **Geoff Hinton** প্রস্তাব করেন **AdaGrad-এর একটি বড় সমস্যা** সমাধানের জন্য, যেখানে training চলাকালীন learning rate ধীরে ধীরে খুব ছোট হয়ে যায়।

RMSprop প্রতিটি parameter-এর জন্য আলাদা ভাবে learning rate adjust করে,  
যেখানে **squared gradient-এর moving average** ব্যবহার করা হয়।

---

## 2. RMSprop কেন দরকার?

### SGD-এর সমস্যা
- Fixed learning rate ব্যবহার করে  
- Steep বা narrow region-এ oscillation করে  
- Convergence ধীর হয়  

---

### AdaGrad-এর সমস্যা
- Squared gradient চিরদিন জমা করে  
- Learning rate সব সময় কমতেই থাকে  
- Training আগেই থেমে যেতে পারে  

👉 **RMSprop পুরনো gradient ধীরে ধীরে ভুলে যায়**, তাই এই সমস্যাগুলো সমাধান হয়।

---

## 3. RMSprop-এর মূল ধারণা (Core Idea)
AdaGrad-এর মতো squared gradient-এর **simple sum** ব্যবহার না করে,  
RMSprop ব্যবহার করে:

> **Squared gradient-এর Exponential Weighted Moving Average**

এর ফলে:
- Learning rate decay নিয়ন্ত্রণে থাকে  
- Long training-এও model শেখা চালিয়ে যেতে পারে  

---

## 4. Mathematical Formulation

### ধাপ–১: Squared Gradient-এর Exponential Moving Average
$$
s_t = \beta s_{t-1} + (1 - \beta)(\nabla L(w_t))^2
$$

---

### ধাপ–২: Weight Update
$$
w_{t+1} = w_t - \frac{\eta}{\sqrt{s_t} + \epsilon} \cdot \nabla L(w_t)
$$

---

## 5. Term গুলোর ব্যাখ্যা
- $w_t$ = সময় *t*-এ weight  
- $\eta$ = learning rate  
- $\beta$ = decay rate (সাধারণত 0.9)  
- $s_t$ = squared gradient-এর moving average  
- $\epsilon$ = division by zero এড়ানোর জন্য ছোট মান

---

## 6. Intuition (সহজভাবে বোঝা)
- Gradient বড় → $s_t$ বড় → learning rate ছোট  
- Gradient ছোট → $s_t$ ছোট → learning rate বড়  

👉 এতে update গুলো হয় **balanced এবং stable**।

---

## 7. Exponential Weighted Average-এর সাথে সম্পর্ক
RMSprop **Exponential Weighted Average (EWA)** ব্যবহার করে:
- সাম্প্রতিক gradient-কে বেশি গুরুত্ব দেয়  
- পুরনো gradient-এর প্রভাব কমায়  

👉 এটাই **AdaGrad এবং RMSprop-এর মূল পার্থক্য**।

---

## 8. RMSprop-এর সুবিধা (Advantages)
- Adaptive learning rate ব্যবহার করে  
- Learning rate শূন্যের কাছাকাছি চলে যাওয়া রোধ করে  
- দ্রুত convergence করে  
- Non-stationary objective-এ ভালো কাজ করে  
- RNN ও deep network-এর জন্য খুব কার্যকর  

---

## 9. RMSprop-এর অসুবিধা (Disadvantages)
- Decay rate $\beta$ ঠিকভাবে tune করতে হয়  
- Adam optimizer-এর মতো সব ক্ষেত্রে robust না  
- Bias correction নেই  

---

## 10. RMSprop বনাম AdaGrad

| বৈশিষ্ট্য | AdaGrad | RMSprop |
|---------|--------|--------|
| Gradient accumulation | Sum | Exponential moving average |
| Learning rate decay | সবসময় কমে | নিয়ন্ত্রিত |
| Long training | দুর্বল | ভালো |
| Deep learning | সীমিত | খুব ভালো |

---

## 11. Implementation Examples

### TensorFlow / Keras
```python
import tensorflow as tf

optimizer = tf.keras.optimizers.RMSprop(
    learning_rate=0.001,
    rho=0.9
)
```
### PyTorch
```python 
import torch

optimizer = torch.optim.RMSprop(
    model.parameters(),
    lr=0.001,
    alpha=0.9
)
```