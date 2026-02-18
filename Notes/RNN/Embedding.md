# Embedding (NLP/RNN)

> শব্দ/টোকেনকে এমন সংখ্যার ভেক্টরে প্রকাশ করা, যা নিউরাল নেটওয়ার্ক বোঝে এবং যেখানে শব্দের অর্থ ও সম্পর্ক ধরা থাকে।

>Embedding মানে হলো শব্দ (word) বা টোকেনকে এমন সংখ্যার (vector) রূপে প্রকাশ করা, যেটা neural network বুঝতে পারে এবং যেখানে শব্দের অর্থ (meaning) ধরা থাকে।

---

## সূচিপত্র
- [কেন Embedding দরকার](#কেন-embedding-দরকার)
- [Embedding কীভাবে কাজ করে](#embedding-কিভাবে-কাজ-করে়)
- [One‑Hot বনাম Embedding](#onehot-encoding-বনাম-embedding)
- [RNN‑এ Embedding এর ভূমিকা](#rnnএ-embedding-এর-ভূমিকা)
- [Keras উদাহরণ](#keras-উদাহরণ-rnn--embedding)
- [Pretrained Embeddings](#pretrained-embeddings)
- [Real‑Life উদাহরণ](#reallife-উদাহরণ)
- [সংক্ষেপে](#সংক্ষেপে-মনে-রাখো)

---

## কেন Embedding দরকার
Neural Network সংখ্যা ছাড়া কিছুই বোঝে না, অথচ ভাষা তৈরি হয় শব্দ দিয়ে। তাই আমাদের দরকার:

```text
শব্দ  →  সংখ্যা (vector)
```

কিন্তু সাধারণ সংখ্যা নয়—এমন ভেক্টর চাই যেখানে অর্থ ও সম্পর্ক ধরা পড়ে। গাণিতিকভাবে, একটি শব্দের এম্বেডিংকে আমরা $\mathbf{x} \in \mathbb{R}^d$ হিসেবে ধরি; এখানে $d$ হলো embedding dimension।

---

## Embedding কীভাবে কাজ করে
ধরা যাক বাক্য: **"I love deep learning"**

**Step 1 — Tokenization**

```text
["I", "love", "deep", "learning"]
```

**Step 2 — Vocabulary তৈরি**

```text
I → 1,  love → 2,  deep → 3,  learning → 4
```

**Step 3 — Embedding Layer** (ধরা যাক dimension = 4)

```text
I        → [0.12,  0.45, -0.33,  0.89]
love     → [0.78, -0.11,  0.56,  0.22]
deep     → [-0.44, 0.91,  0.13, -0.67]
learning → [0.25,  0.66, -0.88,  0.41]
```

> এই ভেক্টরগুলোকেই বলা হয় word embeddings—নিকটবর্তী মান মানে সাধারণত কাছাকাছি অর্থ।

---

## One‑Hot Encoding বনাম Embedding

| তুলনা | One‑Hot | Embedding |
|---|---|---|
| আকার | খুব বড় (Vocabulary size) | ছোট নির্দিষ্ট dimension ($d$) |
| অর্থ | অর্থ/সম্পর্ক বোঝায় না | অর্থ ও সম্পর্ক ধরে |
| দূরত্ব | "love" ≠ "like" (সমান দূরে) | "love" ≈ "like" (কাছাকাছি) |
| শেখা | স্থির | ট্রেনিংয়ে শেখা যায় |

উদাহরণ:

```text
One‑Hot:  love → [0,1,0,0,0,0]
Embed:    love → [0.80, 0.70, 0.10]
          like → [0.79, 0.68, 0.12]
```

---

## RNN‑এ Embedding এর ভূমিকা

```text
Text → Embedding Layer → RNN/LSTM/GRU → Output
```

RNN সরাসরি শব্দ নিতে পারে না; তাই প্রথমে টোকেনগুলোকে এম্বেডিং ভেক্টরে রূপান্তর করা হয়, তারপর সিকোয়েন্স মডেল (RNN/LSTM/GRU) সেই ভেক্টর সিকোয়েন্স প্রক্রিয়া করে।

---

## Keras উদাহরণ (RNN + Embedding)

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, SimpleRNN, Dense

model = Sequential([
    Embedding(input_dim=5000, output_dim=128, input_length=100),
    SimpleRNN(64),
    Dense(1, activation='sigmoid')
])
```

ব্যাখ্যা:
- `input_dim=5000` → vocabulary size
- `output_dim=128` → embedding dimension
- Embedding layer ট্রেনিংয়ের সময় নিজে নিজেই শেখে

---

## Pretrained Embeddings
বড় ডেটাসেটে আগেই শেখানো এম্বেডিং:

| Embedding | উৎস/ধরন |
|---|---|
| Word2Vec | Google |
| GloVe | Stanford |
| FastText | Facebook |
| BERT Embedding | Context‑aware |

> "bank" শব্দটি প্রসঙ্গভেদে আলাদা অর্থ বহন করে—*river bank* বনাম *money bank*। **BERT** প্রসঙ্গ বুঝে আলাদা এম্বেডিং দেয়।

---

## Real‑Life উদাহরণ

**📱 YouTube Recommendation**
- “Python tutorial”, “Machine learning tutorial” → এম্বেডিং কাছাকাছি হলে সম্পর্কিত ভিডিও সাজেস্ট হয়।

**🛒 E‑commerce Search**
- “mobile”, “smartphone” → এম্বেডিং নিকট হলে প্রাসঙ্গিক রেজাল্ট আসে।

---

## সংক্ষেপে মনে রাখো

> **Embedding = শব্দকে অর্থবহ সংখ্যার ভেক্টরে রূপান্তর**

- ছোট dimension
- অর্থ ও সম্পর্ক ধরে
- RNN/Transformer–এর জন্য অপরিহার্য

---
