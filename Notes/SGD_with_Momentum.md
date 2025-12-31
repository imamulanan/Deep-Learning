# Deep Learning-এ SGD with Momentum

## 1. ভূমিকা (Introduction)
Deep Learning-এ একটি neural network train করার মূল লক্ষ্য হলো **loss function কমানো**, অর্থাৎ model-এর parameter (weight) গুলো ধাপে ধাপে update করা।  
এই কাজের জন্য সবচেয়ে বেশি ব্যবহৃত optimization algorithm হলো **Stochastic Gradient Descent (SGD)**।  

তবে সাধারণ SGD-তে কিছু সমস্যা থাকে, যেমন:
- ধীরে convergence করা  
- update-এর সময় instability দেখা দেওয়া  

এই সমস্যাগুলো সমাধান করার জন্য **SGD with Momentum** ব্যবহার করা হয়।

---

## 2. Stochastic Gradient Descent (SGD)

### 2.1 SGD কী?
Stochastic Gradient Descent এমন একটি optimization method যেখানে:
- সম্পূর্ণ dataset ব্যবহার না করে
- ছোট ছোট **mini-batch** থেকে gradient হিসাব করে
- model-এর weight আপডেট করা হয়

---

### 2.2 Mathematical Formulation
SGD-এর সাধারণ weight update formula হলো:

$$
w_{t+1} = w_t - \eta \cdot \nabla L(w_t)
$$

যেখানে,
- $w_t$ = সময় *t*-এ weight  
- $\eta$ = learning rate  
- $\nabla L(w_t)$ = loss function-এর gradient

---

### 2.3 SGD-এর সীমাবদ্ধতা (Limitations)
- Narrow valley-তে বেশি oscillation করে  
- Convergence ধীর হয়  
- Learning rate-এর প্রতি খুব sensitive  
- Saddle point-এর আশেপাশে আটকে যেতে পারে  

---

## 3. Momentum ব্যবহারের প্রয়োজনীয়তা
বাস্তব জীবনের optimization problem-এ loss surface সাধারণত **non-convex** হয়।  
এক্ষেত্রে সাধারণ SGD বারবার direction পরিবর্তন করে, কারণ gradient সব সময় stable থাকে না।

**Momentum** এই সমস্যাগুলো কমাতে সাহায্য করে:
- আগের gradient গুলো জমা রাখে  
- Update-এর direction মসৃণ করে  
- একই দিকে gradient থাকলে speed বাড়ায়  

---

## 4. SGD with Momentum

### 4.1 মূল ধারণা (Concept)
SGD with Momentum-এর ধারণাটি **physics** থেকে নেওয়া।  
এখানে একটি **velocity** term ব্যবহার করা হয়, যা আগের gradient-এর প্রভাব ধরে রাখে।

এটি অনেকটা এমন:
> পাহাড় থেকে একটি বল গড়ালে, একবার গতি পেলে সেটি সহজে থামে না।

---

### 4.2 Mathematical Formulation

#### ধাপ–১: Velocity Update
$$
v_t = \gamma v_{t-1} + \eta \nabla L(w_t)
$$

#### ধাপ–২: Weight Update
$$
w_{t+1} = w_t - v_t
$$

যেখানে,
- $v_t$ = সময় *t*-এ velocity  
- $\gamma$ = momentum coefficient (সাধারণত 0.9)  
- $\eta$ = learning rate

---

## 5. Momentum-এর Intuition (সহজ বোঝাপড়া)
- একই direction-এ থাকা gradient গুলো **জোরালো হয়**
- বিপরীত direction-এর gradient গুলো **noise কমিয়ে দেয়**
- Zig-zag movement কমে যায়
- Training আরও দ্রুত এবং smooth হয়

---

## 6. Visual Understanding
- **SGD:** আঁকাবাঁকা পথে হাঁটার মতো  
- **SGD with Momentum:** পাহাড় থেকে গড়ানো বলের মতো  

Momentum optimizer-কে ছোটখাটো fluctuation ignore করতে সাহায্য করে এবং দ্রুত global minimum-এর দিকে এগিয়ে যায়।

---

## 7. SGD with Momentum-এর সুবিধা (Advantages)
- দ্রুত convergence  
- Oscillation কম হয়  
- Training বেশি stable হয়  
- Deep neural network-এ ভালো কাজ করে  
- Saddle point থেকে বের হতে সাহায্য করে  

---

## 8. অসুবিধা (Disadvantages)
- Momentum coefficient ঠিকভাবে tune করতে হয়  
- Momentum বেশি হলে minimum overshoot করতে পারে  

---

## 9. Implementation Examples

### 9.1 TensorFlow / Keras
```python
import tensorflow as tf

optimizer = tf.keras.optimizers.SGD(
    learning_rate=0.01,
    momentum=0.9
)
```

# Exponential Weighted Average (EWA)

## 1. ভূমিকা (Introduction)
Exponential Weighted Average (EWA) হলো এমন একটি পদ্ধতি যেখানে:
- সাম্প্রতিক মানগুলোর গুরুত্ব বেশি
- পুরনো মানগুলোর গুরুত্ব ধীরে ধীরে কমে যায়

Deep Learning-এ এটি মূলত ব্যবহার করা হয়:
- Gradient smooth করার জন্য
- Noise কমানোর জন্য
- Optimization দ্রুত ও stable করার জন্য

---

## 2. সাধারণ Average vs Exponential Weighted Average

### 2.1 Simple Average
Simple average-এ সব মানকে সমান গুরুত্ব দেওয়া হয়।

$$
Avg = \frac{1}{n} \sum_{i=1}^{n} x_i
$$

👉 সমস্যা: পুরনো এবং নতুন মানের মধ্যে পার্থক্য করা যায় না।

---

### 2.2 Exponential Weighted Average
EWA-তে সাম্প্রতিক মানগুলোকে **বেশি weight** দেওয়া হয় এবং আগের মানগুলোর প্রভাব **exponentially কমে যায়**।

---

## 3. Mathematical Formula

$$
v_t = \beta v_{t-1} + (1 - \beta) x_t
$$

যেখানে,
- $v_t$ = সময় *t*-এ Exponential weighted average  
- $x_t$ = বর্তমান মান  
- $\beta$ = smoothing factor (সাধারণত 0.9 বা 0.99)

---

## 4. β (Beta) এর ভূমিকা
- **β বড় (0.9 – 0.99)** → বেশি smoothing, slow response  
- **β ছোট (0.5 – 0.7)** → কম smoothing, fast response  

📌 সাধারণভাবে,
- β = 0.9 → last ~10 step মনে রাখে  
- β = 0.99 → last ~100 step মনে রাখে  

---

## 5. Intuition (সহজ ব্যাখ্যা)
EWA অনেকটা এমন:

> গতকালের কথা আজও মনে আছে,  
> কিন্তু এক মাস আগের কথা কম মনে আছে।

অর্থাৎ,
- নতুন তথ্য বেশি গুরুত্বপূর্ণ
- পুরনো তথ্য ধীরে ধীরে ভুলে যায়

---

## 6. Deep Learning-এ ব্যবহার

### 6.1 Momentum
Momentum optimizer-এ:
- Gradient-এর exponential weighted average নেওয়া হয়
- Update smooth হয়

$$
v_t = \beta v_{t-1} + (1-\beta)\nabla L(w_t)
$$

---

### 6.2 RMSProp
RMSProp-এ:
- Gradient² এর EWA নেওয়া হয়
- Learning rate adaptive হয়

$$
s_t = \beta s_{t-1} + (1-\beta)(\nabla L(w_t))^2
$$

---

### 6.3 Adam Optimizer
Adam optimizer-এ:
- Gradient-এর EWA (momentum)
- Gradient² এর EWA (RMSProp)
দুটোই ব্যবহার হয়

---

## 7. কেন Exponential Weighted Average দরকার?
- Noise কমায়  
- Sudden fluctuation smooth করে  
- Faster convergence নিশ্চিত করে  
- Training আরও stable করে  

---

## 8. বাস্তব উদাহরণ
ধরো প্রতিদিনের temperature record:
- আজকের তাপমাত্রার প্রভাব বেশি
- এক সপ্তাহ আগের তাপমাত্রার প্রভাব কম

এই ধারণাটাই EWA।

---

## 9. এক লাইনের সংজ্ঞা (Exam Ready)
**Exponential Weighted Average হলো এমন একটি averaging technique যেখানে সাম্প্রতিক মানগুলোকে বেশি গুরুত্ব দিয়ে পুরনো মানগুলোর প্রভাব ধীরে ধীরে কমানো হয়।**

---

## 10. উপসংহার (Conclusion)
Exponential Weighted Average হলো আধুনিক Deep Learning optimization techniques-এর মূল ভিত্তি।  
Momentum, RMSProp এবং Adam optimizer বোঝার জন্য EWA জানা অত্যন্ত জরুরি।

