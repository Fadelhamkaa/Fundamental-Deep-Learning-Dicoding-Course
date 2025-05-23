# Fundamental-Deep-Learning-Dicoding-Course

## Garbage Classification (3-Class)

Proyek ini membangun end-to-end pipeline klasifikasi sampah, mulai dari pemilihan 3 kelas terbaik hingga konversi model untuk deployment di berbagai platform.


## 📂 Struktur Repo


submission/
├── saved\_model/           # TensorFlow SavedModel (server/cloud)
│   ├── saved\_model.pb
│   └── variables/
│       ├── variables.data-00000-of-00001
│       └── variables.index
├── tflite/                # TensorFlow Lite (mobile/embedded)
│   ├── model.tflite
│   └── label.txt
├── tfjs\_model/            # TensorFlow\.js (browser/JavaScript)
│   ├── model.json
│   └── group1-shard\*.bin
├── garbage\_3cls/          # Data split (train/val/test per class)
│   ├── train/
│   ├── val/
│   └── test/
├── notebook.ipynb         # Semua langkah di Colab
├── requirements.txt       # Dependencies
└── README.md              # (file ini)



---

## 🎯 Ringkasan Pipeline

1. **Pemilihan 3 Kelas Terbaik**  
   Berdasarkan _f1-score_ pada 6-kelas awal, dipilih:  
   `cardboard`, `paper`, `plastic`
2. **Stratified Split** (70 / 15 / 15)  
   Langsung dari folder dataset asli, membagi ke  
   `garbage_3cls/{train,val,test}/{kelas}/`
3. **Data Augmentasi & Generator**  
   Augmentasi kaya (rotasi, shift, zoom, brightness, flip)
4. **Training**  
   - Optimizer: Adam (LR=1e-4)  
   - Callbacks: `EarlyStopping` + `ReduceLROnPlateau`  
   - **Class weights** untuk handle imbalance  
   - **Fine-tuning**: buka top-10 layer, lanjut training LR=1e-5  
5. **Evaluasi**  
   - **Test accuracy:** 87.84%  
   - Classification report per kelas  
6. **Konversi Model**  
   - **SavedModel** untuk server/cloud  
   - **TFLite** untuk mobile/embedded  
   - **TFJS** untuk web/browser  
7. **Inferensi Contoh**  
   - Satu-baris kode Python (SavedModel / TFLite)  
   - Snippet JS untuk TensorFlow.js

---

## 🗂️ Dataset & Split Detail

- **Asal**: `/content/drive/MyDrive/.../Garbage classification/`
- **Kelas**: `cardboard`, `paper`, `plastic`
- **Jumlah gambar** (top3):  
  cardboard: 393
  paper:     584
  plastic:   472
  Total:    1449


* **Split**:

  * Train: \~1014 (70%)
  * Val:    \~217 (15%)
  * Test:   \~217 (15%)

---

## 🛠️ Instalasi & Jalankan

1. Clone repo:


   git clone [https://github.com/username/garbage-3cls](https://github.com/Fadelhamkaa/Fundamental-Deep-Learning-Dicoding-Course/).git
   cd submission


2. Install dependencies:


   pip install -r requirements.txt


3. Buka `notebook.ipynb` di Colab, jalankan dari atas sampai akhir.

---

---

## 📋 Requirements


tensorflow>=2.11
tensorflowjs
numpy
Pillow
matplotlib
scikit-learn


---

## 📖 License

MIT © 2025 ― Muhammad Fadel Hamka
Feel free to adapt & reuse!
