# 📊 Data Augmentation (ডেটা অগমেন্টেশন)

> **Definition:** মেশিন লার্নিং / ডিপ লার্নিং-এ ট্রেনিং ডেটাকে কৃত্রিমভাবে বাড়ানোর একটি কৌশল, যেখানে মূল ডেটা পরিবর্তন করে নতুন ভ্যারিয়েশন তৈরি করা হয়—কিন্তু ডেটার আসল অর্থ (label) একই থাকে।

### 💡 সহজ ভাষায়
**কম ডেটা দিয়ে বেশি ডেটার মতো করে মডেলকে ট্রেন করা**

---

## ❓ কেন Data Augmentation দরকার?

ডিপ লার্নিং মডেল (বিশেষ করে CNN) ভালো কাজ করতে **অনেক ডেটা** চায়।

| সমস্যা | বর্ণনা |
|--------|---------|
| 📉 **কম ডেটা** | ডেটা সংগ্রহ করা কঠিন |
| 🏷️ **লেবেল খরচ** | ডেটা লেবেল করা সময়সাপেক্ষ |
| 🔄 **Overfitting** | কম ডেটা হলে মডেল মুখস্থ করে ফেলে |

👉 **Data Augmentation এই সমস্যাগুলো সমাধান করে**

---

## ⚙️ Data Augmentation কীভাবে কাজ করে?

একই ডেটার উপর **ছোট ছোট পরিবর্তন** করা হয়, যেমন:

```
একটি বিড়ালের ছবি 🐱
        ↓
   (ঘোরানো, উল্টানো, জুম, আলো)
        ↓
   নতুন নতুন ছবি তৈরি
        ↓
   label থাকে "Cat" ✓
```

---

## 🖼️ Image Data Augmentation (সবচেয়ে বেশি ব্যবহৃত)

### 📋 সাধারণ Techniques

| # | Technique | বর্ণনা | উদাহরণ |
|---|-----------|--------|--------|
| 1 | 🔄 **Rotation** | ছবি ঘোরানো | 10°, 20°, 90° |
| 2 | ↔️ **Flipping** | ছবি উল্টানো | Horizontal, Vertical |
| 3 | 🔍 **Zoom/Scale** | ছবি বড় বা ছোট | 0.8x থেকে 1.5x |
| 4 | ⬌ **Translation** | ছবি শিফট করা | ডানে-বামে, ওপরে-নিচে |
| 5 | ☀️ **Brightness** | আলো সামঞ্জস্য | বাড়ানো বা কমানো |
| 6 | 📐 **Shear** | ছবি বাঁকা করা | Skew transformation |
| 7 | 🌪️ **Noise** | Random noise যোগ | Gaussian, Salt & Pepper |

---

## 💬 Text Data Augmentation (NLP)

টেক্সট ডেটার ক্ষেত্রে বিভিন্ন পদ্ধতি রয়েছে:

| Technique | উদাহরণ |
|-----------|--------|
| 🔄 **Synonym Replacement** | "good" → "excellent", "bad" → "poor" |
| ➕ **Random Insertion** | বাক্যে র্যান্ডম শব্দ যোগ করা |
| ➖ **Random Deletion** | বাক্য থেকে র্যান্ডম শব্দ মুছা |
| 🔁 **Back Translation** | English → Bangla → English |

---

## 🎵 Audio Data Augmentation

- 🔊 Background noise যোগ করা
- 🎼 Speed বাড়ানো/কমানো
- 🎹 Pitch পরিবর্তন করা
- 🎧 Time shifting

---

## 💪 Data Augmentation এর সুবিধা ও সীমাবদ্ধতা

### ✅ প্রধান সুবিধা

| সুবিধা | বর্ণনা |
|--------|--------|
| 📉 **Overfitting কমায়** | মডেল একই ডেটা মুখস্থ করতে পারে না |
| 🎯 **Generalization বাড়ায়** | নতুন ডেটায় ভালো পারফরম্যান্স |
| 💾 **কম ডেটা প্রয়োজন** | সীমিত ডেটা দিয়ে ভালো ফলাফল |
| 🌍 **Real-world variations** | বাস্তব পরিস্থিতির বৈচিত্র্য শেখায় |

### ⚠️ সীমাবদ্ধতা

| সীমাবদ্ধতা | সমাধান |
|-----------|--------|
| ❌ **অযথা augmentation** | সঠিক technique নির্বাচন করুন |
| 📊 **সব সমস্যার জন্য নয়** | ডোমেন অনুযায়ী কাস্টমাইজ করুন |
| 🐌 **কম্পিউটেশনাল খরচ** | প্রাক-augmented ডেটা সংরক্ষণ করুন |

---

## 🔍 Deep Learning-এ বাস্তব প্রয়োগ

| ক্ষেত্র | প্রয়োগ |
|--------|--------|
| 📸 **Image Classification** | ছবি শ্রেণীবিভাজন |
| 😊 **Face Recognition** | মুখ সনাক্তকরণ |
| 🏥 **Medical Imaging** | স্কিন ক্যান্সার, এক্স-রে ডায়াগনসিস |
| 🚗 **Autonomous Driving** | স্বয়ংক্রিয় গাড়ি চালনা |
| 🔢 **Handwriting Recognition** | হাতের লেখা সনাক্তকরণ |

> **তোমার CNN + Skin Disease প্রজেক্টে এটা অত্যন্ত গুরুত্বপূর্ণ!** 🎯

---

## 🔗 Overfitting এর সাথে সম্পর্ক

```
Data Augmentation ↓
├── Training data বাড়ায় ✅
├── Model একই ডেটা মুখস্থ করতে পারে না ✅
└── নতুন নতুন পরিস্থিতি দেখে শেখে ✅
         ↓
     Overfitting কমে ✅
```

---

## 🎁 সংক্ষিপ্ত সারাংশ

> ### 📌 **এক লাইনে**
> **Data Augmentation হলো মূল ডেটা পরিবর্তন করে নতুন ডেটা তৈরি করার কৌশল, যা মডেলকে বেশি robust এবং general করে তোলে।**

---

## 🚀 Python Example (Keras)

```python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

# Data Augmentation সেটআপ
datagen = ImageDataGenerator(
    rotation_range=30,        # 30° পর্যন্ত ঘোরান
    zoom_range=0.2,           # 0.2x জুম
    horizontal_flip=True,      # অনুভূমিক ফ্লিপ
    width_shift_range=0.2,    # 20% প্রস্থ শিফট
    height_shift_range=0.2    # 20% উচ্চতা শিফট
)

# প্রশিক্ষণের সময় প্রয়োগ করুন
# model.fit(datagen.flow(train_data, train_labels, batch_size=32))
```

---

*শেষ আপডেট: 2026* 📅
