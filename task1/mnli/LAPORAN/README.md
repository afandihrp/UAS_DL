# Laporan Eksperimen: Fine-Tuning BERT pada Dataset MNLI

Proyek ini bertujuan untuk melakukan fine-tuning pada model `bert-base-uncased` menggunakan dataset **MNLI (Multi-Genre Natural Language Inference)** dari benchmark GLUE. Tugas utama model adalah mengklasifikasikan pasangan kalimat (*premise* dan *hypothesis*) ke dalam tiga label: *Entailment*, *Neutral*, atau *Contradiction*.

## 1. Lingkungan Eksperimen
Training dijalankan pada lingkungan lokal dengan spesifikasi perangkat keras sebagai berikut:

* **GPU:** NVIDIA GeForce RTX 3060 Laptop GPU (1 Unit)
* **Platform:** Linux
* **Framework:** PyTorch, Hugging Face Transformers, Datasets, Evaluate

## 2. Metodologi & Konfigurasi
Model dilatih menggunakan pendekatan *End-to-End Fine-Tuning* dengan konfigurasi hyperparameter berikut:

| Parameter | Nilai |
| :--- | :--- |
| **Base Model** | `bert-base-uncased` |
| **Batch Size (Train)** | 8 |
| **Batch Size (Eval)** | 16 |
| **Learning Rate** | 2e-5 |
| **Weight Decay** | 0.01 |
| **Epochs** | 1 |
| **Optimizer** | AdamW (Default Trainer) |

**Catatan:** Training dilakukan hanya selama 1 epoch karena keterbatasan resource atau untuk membuktikan konsep (*proof of concept*), namun hasil yang didapat sudah menunjukkan konvergensi yang baik.

## 3. Hasil Training dan Evaluasi
Berikut adalah ringkasan performa model setelah proses training selesai:

### Metrik Performa (Validation Matched)
| Metrik | Nilai | Deskripsi |
| :--- | :--- | :--- |
| **Validation Loss** | 0.4564 | Tingkat kesalahan pada data validasi. |
| **Accuracy** | **83.23%** | Persentase prediksi yang tepat. |
| **F1 Macro** | 83.17% | Rata-rata harmonik precision/recall (seimbang antar kelas). |

### Statistik Training
* **Training Loss Akhir:** 0.5281
* **Durasi Training:** ~54 menit (3249 detik)
* **Kecepatan:** ~15 langkah/detik (steps per second)

## 4. Analisis Hasil
Meskipun hanya dilatih selama **1 epoch**, model `bert-base` mampu mencapai akurasi **83.23%**. Sebagai perbandingan, state-of-the-art untuk BERT-base pada MNLI biasanya berkisar di angka 84-85% dengan training 3 epoch. Hal ini menunjukkan bahwa:
1.  Model berhasil mempelajari pola inferensi bahasa dengan sangat cepat.
2.  Learning rate `2e-5` sangat efektif untuk dataset ini.
3.  Tidak terjadi *overfitting* yang signifikan (Loss validasi 0.45 vs Training loss 0.43-0.52 masih dalam rentang wajar).

## 5. Contoh Inferensi (Qualitative Analysis)
Model diuji dengan input kalimat baru untuk memverifikasi kemampuan generalisasi:

**Kasus 1 (Entailment):**
> *Premise:* "Two men in polo shirts standing in a bar."
> *Hypothesis:* "They are in a pub."
> **Prediksi:** **Entailment** (Score: 0.7811) ✅
> *Analisis:* Model memahami bahwa "bar" dan "pub" memiliki konteks lokasi yang serupa/berhubungan.

**Kasus 2 (Contradiction):**
> *Premise:* "A man inspects the uniform of a figure in some East Asian country."
> *Hypothesis:* "A man is sleeping."
> **Prediksi:** **Contradiction** (Score: 0.9696) ✅
> *Analisis:* Model dengan tegas mendeteksi pertentangan antara aktivitas "inspects" (aktif) dan "sleeping" (pasif).

## 6. Kesimpulan & Rekomendasi
Model ini siap digunakan untuk tugas inferensi bahasa alami tingkat dasar. Untuk meningkatkan performa mendekati batas maksimal kemampuan BERT:
* Disarankan menambah jumlah epoch menjadi 3.
* Menggunakan *Gradient Accumulation* jika ingin memperbesar *batch size* efektif tanpa membebani VRAM GPU Laptop.