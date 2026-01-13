# 🔲 CNN Filter (Kernel) - সম্পূর্ণ গাইড

## 📖 Filter কী?

> **Filter (বা Kernel)** হলো CNN-এর হৃদপিণ্ড—একটি ছোট trainable matrix যা ছবির উপর স্লাইড করে গুরুত্বপূর্ণ features বের করে।

### 💡 সহজ ভাষায়
**Filter হলো একটি feature detector যা ছবি থেকে patterns, edges, textures খুঁজে বের করে**

---

## ❓ Filter কেন দরকার?

একটা ছবি মূলত শুধু pixel values এর সমষ্টি। CNN নিজে থেকে বুঝতে পারে না:

| সমস্যা | ব্যাখ্যা |
|--------|---------|
| 🔲 **Edge Detection** | কোথায় বস্তুর প্রান্ত আছে |
| 📐 **Corner Detection** | কোথায় কোণা আছে |
| 🎨 **Texture Recognition** | কোথায় কোন pattern আছে |
| 🎯 **Shape Understanding** | বস্তুর আকার কী |

💡 **Filter এই সব কাজই করে—ছবি থেকে meaningful information extract করে**

---

## 📐 Filter দেখতে কেমন?

### উদাহরণ: 3×3 Vertical Edge Detector

```
┌           ┐
│  1   0  -1 │
│  1   0  -1 │
│  1   0  -1 │
└           ┘
```

**🎯 কাজ:** এই filter vertical edges detect করে

### সাধারণ Filter Types

| Filter | Matrix Example | Detects |
|--------|----------------|---------|
| 🔲 **Vertical Edge** | `[1,0,-1]` | উল্লম্ব প্রান্ত |
| ↔️ **Horizontal Edge** | `[1,1,1],[0,0,0],[-1,-1,-1]` | অনুভূমিক প্রান্ত |
| 🔍 **Blur** | `[1,1,1],[1,1,1],[1,1,1]` / 9 | ছবি blur করে |
| ⚡ **Sharpen** | `[0,-1,0],[-1,5,-1],[0,-1,0]` | তীক্ষ্ণতা বাড়ায় |

---

## ⚙️ Filter কীভাবে কাজ করে?

### 🔄 Convolution Operation (Step-by-Step)

**Input Setup:**
- Input image: `7 × 7`
- Filter: `3 × 3`
- Stride: `1`

**Process:**

```
Step 1: Filter বাম-উপরের কোণায় বসে
    ┌───────┐
    │ ■ ■ ■ │ × Filter
    │ ■ ■ ■ │
    │ ■ ■ ■ │
    └───────┘

Step 2: Element-wise multiplication
    (Pixel × Filter weight) সব positions-এ

Step 3: সব গুণফল যোগ → Single output value

Step 4: Filter ডানে slide করে (stride অনুযায়ী)

Step 5: পুরো image জুড়ে repeat
```

**Result:** একটি **Feature Map** তৈরি হয়

---

## 🗺️ Filter → Feature Map সম্পর্ক

```
1 Filter  →  1 Feature Map
10 Filters → 10 Feature Maps
96 Filters → 96 Feature Maps
```

| Filters | Output | Use Case |
|---------|--------|----------|
| 1-10 | কম features | Simple tasks |
| 32-64 | Moderate | সাধারণ CNN |
| 96-256 | অনেক features | Deep CNN (AlexNet, VGG) |

---

## 🎯 Filter কী কী Feature ধরে?

### 📊 Layer Hierarchy

| Layer Level | Filter Type | Detects | Example |
|------------|-------------|---------|---------|
| 🔴 **Layer 1-2** | Low-level | Edges, colors, simple shapes | `/`, `\`, `─`, `│` |
| 🟠 **Layer 3-5** | Mid-level | Textures, patterns, corners | চোখের pattern, চাকার curve |
| 🟢 **Layer 6+** | High-level | Complex objects, parts | পুরো মুখ, গাড়ি, পশু |

### 🔄 Feature Learning Progression

```
Simple Edges → Textures → Shapes → Parts → Complete Objects
     ↓            ↓          ↓        ↓            ↓
   Layer 1     Layer 2    Layer 3  Layer 4    Layer 5+
```

---

## 🎨 Color Image-এ Filter কীভাবে কাজ করে?

### RGB Image Example

**Input:**
```
📐 Dimension: 227 × 227 × 3
            (Height × Width × Channels)
```

**Filter:**
```
📐 Dimension: 11 × 11 × 3
            (Height × Width × Channels)
```

### 🔑 গুরুত্বপূর্ণ Rule

> **Filter-এর depth (channel count) সবসময় input image-এর depth-এর সমান হয়**

| Input Channels | Filter Channels | Output |
|---------------|-----------------|---------|
| 3 (RGB) | 3 | ✅ Valid |
| 1 (Grayscale) | 1 | ✅ Valid |
| 3 (RGB) | 1 | ❌ Invalid |

### 🧮 Filter Size Formula

```
যদি Input = H × W × C
তাহলে Filter = f × f × C

যেখানে:
  f = filter height = filter width
  C = input channels
```

**Example:**
```python
Input:  (224, 224, 3)  # RGB image
Filter: (5, 5, 3)      # 5×5 filter for RGB
Output: (220, 220, 1)  # Single feature map (without padding)
```

---

## 📏 Filter Parameters

### 1️⃣ Stride (স্ট্রাইড)

Filter কত ঘর করে move করবে

| Stride | Movement | Output Size | Detail Level |
|--------|----------|-------------|--------------|
| s = 1 | ধীরে যায় | বড় output | বেশি detail |
| s = 2 | দ্রুত যায় | ছোট output | কম detail |
| s = 3+ | খুব দ্রুত | অনেক ছোট | কম তথ্য |

**Visual:**
```
Stride = 1:  ■ → ■ → ■ → ■
Stride = 2:  ■ → → ■ → → ■
```

---

### 2️⃣ Padding (প্যাডিং)

ছবির চারপাশে zeros যোগ করা

| Padding Type | Effect | Use Case |
|-------------|--------|----------|
| ✖️ **Valid** | কোন padding নেই | Output size কমে |
| ✅ **Same** | Output = Input size | Size maintain করা |
| 🔢 **Custom** | নির্দিষ্ট padding | বিশেষ প্রয়োজনে |

**Visual Example:**
```
Without Padding:        With Padding (p=1):
┌─────────┐            ┌───────────────┐
│ 5 × 5   │            │ 0 0 0 0 0 0 0 │
│  image  │    →       │ 0    5 × 5  0 │
│         │            │ 0   image   0 │
└─────────┘            │ 0 0 0 0 0 0 0 │
                       └───────────────┘
```

---

## 🧮 Output Size Calculation

### Formula

```
Output Size = ⌊(N − F + 2P) / S⌋ + 1
```

**যেখানে:**
- `N` = Input size (height বা width)
- `F` = Filter size
- `P` = Padding
- `S` = Stride
- `⌊ ⌋` = Floor function

### 📊 Calculation Examples

| Input (N) | Filter (F) | Padding (P) | Stride (S) | Output | Calculation |
|-----------|-----------|-------------|------------|--------|-------------|
| 7 | 3 | 0 | 1 | 5 | (7-3+0)/1 + 1 = 5 |
| 7 | 3 | 1 | 1 | 7 | (7-3+2)/1 + 1 = 7 |
| 32 | 5 | 0 | 2 | 14 | (32-5+0)/2 + 1 = 14 |
| 227 | 11 | 0 | 4 | 55 | (227-11+0)/4 + 1 = 55 |

---

## 🧠 Filter কীভাবে শেখে?

### ⚠️ গুরুত্বপূর্ণ তথ্য

```
❌ Filter manually বানানো হয় না
✅ Training-এর সময় automatically শেখে
```

### 🔄 Learning Process

```
1. Random Initialization
   ↓
2. Forward Pass (Prediction)
   ↓
3. Loss Calculation
   ↓
4. Backpropagation
   ↓
5. Filter Weights Update
   ↓
6. Repeat (until convergence)
```

**🎯 Goal:** Loss minimize করার জন্য optimal filter values খুঁজে বের করা

---

## 🔍 Real-World Example: AlexNet

### Layer 1 Configuration

| Parameter | Value | Description |
|-----------|-------|-------------|
| 📥 **Input** | 227 × 227 × 3 | RGB image |
| 🔲 **Filter Size** | 11 × 11 × 3 | Large filter |
| 📊 **Num Filters** | 96 | Multiple features |
| 👟 **Stride** | 4 | Fast movement |
| 📤 **Output** | 55 × 55 × 96 | 96 feature maps |

**Calculation:**
```
Output = (227 - 11 + 0) / 4 + 1
       = 216 / 4 + 1
       = 54 + 1
       = 55 ✓
```

**Result:** 96টি different features একসাথে detect হয়!

---

## 📊 Filter Size সম্পর্কে মজার তথ্য

### 🎯 Common Filter Sizes

| Size | Usage | Pros | Cons |
|------|-------|------|------|
| 1×1 | Channel mixing | খুব হালকা | কম spatial info |
| 3×3 | সবচেয়ে জনপ্রিয় | Balance ভালো | Standard |
| 5×5 | বড় features | বেশি context | বেশি computation |
| 7×7, 11×11 | First layers | Large receptive field | খুব ভারী |

### 💡 Modern Trend
**বেশিরভাগ modern CNN-এ 3×3 filter ব্যবহার হয় (VGG, ResNet)**

---

## 🎓 Exam-Friendly Definition

> ### 📝 পরীক্ষার জন্য মুখস্থ করুন
> **Filter (Kernel) হলো CNN-এর একটি trainable weight matrix, যা input image-এর উপর convolution operation করে বিভিন্ন গুরুত্বপূর্ণ features (edge, texture, shape, pattern) extract করে এবং feature maps তৈরি করে।**

---

## 🎯 মনে রাখার সহজ ট্রিক

### Flow Diagram
```
🖼️ Input Image
    ↓
🔲 Filter (Convolution)
    ↓
🗺️ Feature Maps
    ↓
🧠 Neural Network
    ↓
🎯 Decision/Classification
```

### 📌 Key Points

| Concept | Remember |
|---------|----------|
| 🔢 **Depth** | Filter depth = Input depth |
| 📊 **Multiple** | More filters = More features |
| 🎓 **Learning** | Filters শিখে, তৈরি করা হয় না |
| 📏 **Size** | 3×3 সবচেয়ে common |
| 🔄 **Hierarchy** | Shallow → Simple, Deep → Complex |

---

## 💡 Python Example (Keras)

```python
from tensorflow.keras.layers import Conv2D

# একটি Conv2D layer তৈরি
layer = Conv2D(
    filters=96,           # 96টি filters
    kernel_size=(11, 11), # 11×11 size
    strides=(4, 4),       # Stride = 4
    padding='valid',      # No padding
    activation='relu'     # ReLU activation
)

# Input shape: (227, 227, 3)
# Output shape: (55, 55, 96)
```


---

## 📚 সারাংশ

### ✅ মূল বিষয়
1. Filter হলো trainable weight matrix
2. Convolution করে feature extract করে
3. Multiple filters = Multiple feature maps
4. Backpropagation দিয়ে শেখে
5. Layer hierarchy: Simple → Complex features

### 🎯 Remember
> **"Filter is the eye of CNN—it sees and learns patterns!"**

---

*📅 Last Updated: January 2026*
