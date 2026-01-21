# Regularization in Deep Learning

## 1. Regularization কী?

**Regularization** হলো Deep Learning–এর এমন কিছু technique  
যার প্রধান উদ্দেশ্য হলো—

👉 **Overfitting কমানো**  
👉 **Model কে নতুন data-তে ভালো perform করাতে সাহায্য করা (Generalization)**

সহজভাবে:
> Model যেন training data মুখস্থ না করে  
> বরং pattern শিখে নতুন data-তেও ভালো কাজ করে

---

## 2. Overfitting কী এবং Regularization কেন দরকার?

### Overfitting সমস্যা
- Training accuracy অনেক বেশি
- Validation / Test accuracy কম
- Model শুধু training data-তেই ভালো কাজ করে

📌 কারণ:
- Model খুব complex
- Dataset ছোট
- Parameter অনেক বেশি

👉 এই সমস্যা সমাধানের জন্যই **Regularization** ব্যবহার করা হয়।

---

## 3. Regularization কীভাবে কাজ করে?

Regularization মূলত:
- Model-এর complexity কমায়
- Weight খুব বড় হতে দেয় না
- Model-কে simple solution শিখতে বাধ্য করে

---

## 4. Regularization-এর প্রকারভেদ (Types)

---

## 4.1 L1 Regularization (Lasso)

### কী করে?
- Weight-এর **absolute value** যোগ করে loss-এর সাথে

### Mathematical Form:
$$
Loss = Original\ Loss + \lambda \sum |w|
$$

### বৈশিষ্ট্য:
- কিছু weight একদম 0 হয়ে যায়
- Feature selection করে

### ব্যবহার:
- Feature বেশি হলে

---

## 4.2 L2 Regularization (Ridge / Weight Decay)

### কী করে?
- Weight-এর **square** যোগ করে loss-এর সাথে

### Mathematical Form:
$$
Loss = Original\ Loss + \lambda \sum w^2
$$

### বৈশিষ্ট্য:
- Weight ছোট রাখে
- Smooth model তৈরি করে

📌 Deep Learning–এ সবচেয়ে বেশি ব্যবহৃত regularization

---

## 4.3 Dropout Regularization

### কী করে?
- Training-এর সময় random neuron বন্ধ করে দেয়

### Dropout Rate:
- `0.2 – 0.5`

### উপকার:
- Neuron dependency কমে
- Overfitting কমে

📌 Dropout শুধু training-এর সময় কাজ করে

---

## 4.4 Data Augmentation

### কী করে?
- Dataset কৃত্রিমভাবে বড় করে

### Example:
- Image rotate
- Flip
- Zoom
- Crop

📌 Computer Vision–এ খুব জনপ্রিয়

---

## 4.5 Early Stopping

### কী করে?
- Validation loss বাড়তে শুরু করলে training বন্ধ করে দেয়

### উপকার:
- Over-training থেকে রক্ষা করে

---

## 4.6 Batch Normalization (Indirect Regularization)

### কী করে?
- Activation normalize করে
- Training stable করে

📌 Direct regularization না হলেও  
👉 Overfitting কমাতে সাহায্য করে

---

## 5. Regularization Parameter (λ / Lambda)

- Regularization-এর শক্তি নিয়ন্ত্রণ করে
- λ বেশি → model বেশি simple
- λ কম → model বেশি flexible

📌 সাধারণত:
- `0.0001 – 0.01`

---

## 6. Regularization ব্যবহার না করলে কী হয়?

❌ Overfitting  
❌ Poor generalization  
❌ Test accuracy কম  
❌ Real-world data-তে খারাপ result  

---

## 7. Regularization ব্যবহার করলে কী উপকার?

✅ Overfitting কমে  
✅ Stable training  
✅ Better generalization  
✅ Robust model  

---

## 8. Keras / TensorFlow Example

### L2 Regularization
```python
from tensorflow.keras import regularizers

Dense(
    128,
    activation='relu',
    kernel_regularizer=regularizers.l2(0.001)
)
```
