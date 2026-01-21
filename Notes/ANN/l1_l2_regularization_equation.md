# L1 and L2 Regularization Equation Explained (Deep Learning)

## 🔹 মূল Equation গুলো

### L1 Regularization
$$
Loss = Original\ Loss + \lambda \sum |w|
$$

### L2 Regularization
$$
Loss = Original\ Loss + \lambda \sum w^2
$$

এখন এগুলো একদম ভেঙে বুঝি 👇

---

## 1. Original Loss কী?

**Original Loss** হলো সেই loss যেটা model সাধারণভাবে minimize করতে চায়।

### উদাহরণ:
- **Regression** → Mean Squared Error (MSE)
- **Classification** → Cross Entropy Loss

### Example (MSE):
$$
Original\ Loss = \frac{1}{n} \sum (y - \hat{y})^2
$$

👉 এই loss শুধু prediction error দেখে  
👉 model-এর complexity বা weight কত বড় হচ্ছে তা দেখে না  

---

## 2. $w$ মানে কী?

- $w$ = model-এর **weights**
- Neural network–এর প্রতিটা connection-এর সাথে একটি weight থাকে

📌 **Overfitting হলে:**
- এই weight গুলো খুব বড় (large) হয়ে যায়  
- Model training data মুখস্থ করে ফেলে  

---

## 3. $\lambda$ (Lambda) কী?

$$
\lambda = \text{regularization strength}
$$

👉 Lambda ঠিক করে দেয়:
- model কতটা **simple** হবে  
- weight কতটা **penalty** পাবে  

### λ মান ও প্রভাব

| λ মান | প্রভাব |
|----|----|
| খুব ছোট | Regularization প্রায় নেই |
| মাঝারি | Balanced model |
| খুব বড় | Underfitting হতে পারে |

---

## 4. L1 Regularization Equation (Detail)

$$
Loss = Original\ Loss + \lambda \sum |w|
$$

### এখানে কী হচ্ছে?

- প্রতিটা weight-এর **absolute value** নেওয়া হচ্ছে  
- সব weight যোগ করা হচ্ছে  
- সেটাকে $\lambda$ দিয়ে multiply করা হচ্ছে  
- Original loss-এর সাথে যোগ করা হচ্ছে  

### কেন Absolute Value (|w|)?

কারণ:
- weight positive বা negative যাই হোক  
- weight বড় হলেই penalty বাড়বে  

### Gradient কী হয়?

$$
\frac{\partial |w|}{\partial w} =
\begin{cases}
+1 & w > 0 \\
-1 & w < 0
\end{cases}
$$

📌 **এর ফলাফল:**
- ছোট weight → আরও ছোট হয়  
- অনেক weight → একদম **0** হয়ে যায়  

👉 এজন্যই **L1 regularization feature selection করে**

---

## 5. L2 Regularization Equation (Detail)

$$
Loss = Original\ Loss + \lambda \sum w^2
$$

### এখানে কী হচ্ছে?

- প্রতিটা weight **square** করা হচ্ছে  
- বড় weight হলে penalty অনেক বেশি  
- ছোট weight হলে penalty কম  

### Gradient কী হয়?

$$
\frac{\partial w^2}{\partial w} = 2w
$$

📌 **এর ফলাফল:**
- weight ধীরে ধীরে ছোট হয়  
- কিন্তু সাধারণত **0 হয় না**

👉 এজন্য L2 weight **smoothly shrink** করে  

---

## 6. L1 vs L2 – Gradient Intuition

| বিষয় | L1 | L2 |
|----|----|----|
| Penalty | $|w|$ | $w^2$ |
| Gradient | Constant | w-এর proportional |
| Zero weight | হয় | সাধারণত হয় না |
| Feature selection | হ্যাঁ | না |
| Smoothness | কম | বেশি |

---

## 7. Geometric Intuition (Conceptual)

- **L1 Regularization**
  - Diamond-shaped constraint
  - Corner point-এ solution
  - অনেক weight = 0

- **L2 Regularization**
  - Circular constraint
  - Smooth solution
  - Weight ছোট কিন্তু non-zero

📌 এটি exam-এ খুব জনপ্রিয় explanation

---

## 8. Deep Learning–এ কেন L2 বেশি ব্যবহার হয়?

- Training বেশি stable  
- Gradient smooth থাকে  
- Optimization সহজ হয়  
- High-dimensional weight space-এ ভালো কাজ করে  

👉 এজন্য L2 regularization কে বলা হয়  
**Weight Decay**

---

## 9. Short Summary

- Regularization model-এর complexity কমায়  
- L1 weight zero করে → feature selection  
- L2 weight ছোট রাখে → smooth model  
- Deep Learning–এ L2 সবচেয়ে বেশি ব্যবহৃত  

---
