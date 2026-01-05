# Fine-tuning BERT untuk Klasifikasi Emosi Multi-Label (GoEmotions)

Proyek ini menunjukkan proses fine-tuning model BERT (`bert-base-uncased`) untuk tugas klasifikasi emosi multi-label menggunakan dataset GoEmotions. Notebook `testing.ipynb` berisi implementasi lengkap dari pipeline, mulai dari pemuatan data hingga inferensi.

## Ringkasan Proyek

Tujuan dari proyek ini adalah untuk melatih sebuah model yang dapat mengenali dan memberikan beberapa label emosi yang relevan untuk sebuah teks. Dataset GoEmotions digunakan, yang berisi teks dari komentar Reddit yang telah dilabeli dengan 27 emosi + 1 label 'netral'.

## Pipeline

Proses yang diimplementasikan dalam `testing.ipynb` adalah sebagai berikut:

1.  **Instalasi Dependensi**: Menginstal `transformers`, `datasets`, `evaluate`, `accelerate`, dan `scikit-learn`.
2.  **Pemuatan Dataset**: Memuat dataset `google-research-datasets/go_emotions` dari Hugging Face Hub.
3.  **Preprocessing**:
    *   **Tokenisasi**: Teks diubah menjadi token menggunakan `AutoTokenizer` dari `bert-base-uncased`.
    *   **Encoding Label**: Label emosi dikonversi menjadi format *multi-hot vector* agar sesuai untuk training klasifikasi multi-label.
4.  **Setup Model**:
    *   Model `AutoModelForSequenceClassification` dimuat dengan `problem_type='multi_label_classification'`.
    *   Konfigurasi model disesuaikan untuk memiliki 28 label keluaran.
5.  **Training**:
    *   Model dilatih menggunakan `Trainer` dari Hugging Face.
    *   Hyperparameter yang digunakan:
        *   **Epochs**: 3
        *   **Batch Size**: 16 (training), 32 (evaluasi)
        *   **Learning Rate**: 2e-5
6.  **Evaluasi**:
    *   Metrik yang digunakan adalah **F1-score (micro & macro)**, yang umum untuk tugas klasifikasi multi-label.
    *   Evaluasi dilakukan di setiap akhir epoch pada set validasi.

## Hasil Training

Model terbaik didapatkan pada epoch ke-3 dengan hasil evaluasi pada set validasi sebagai berikut:

| Metrik       | Skor        |
|--------------|-------------|
| `eval_loss`    | `0.0853`    |
| `eval_f1_micro`| `0.5733`    |
| `eval_f1_macro`| `0.3944`    |

Berikut adalah log training dari `Trainer`:

```
Epoch | Training Loss | Validation Loss | F1 Micro | F1 Macro
:---: | :---: | :---: | :---: | :---:
1     | 0.093400      | 0.093321        | 0.509136 | 0.248086
2     | 0.083200      | 0.085575        | 0.556098 | 0.367664
3     | 0.074100      | 0.085382        | 0.573374 | 0.394483
```

Checkpoint model disimpan di direktori `goemotions-bert/`. Checkpoint terbaik (`checkpoint-8142`) digunakan untuk inferensi.

## Contoh Inferensi

Berikut adalah contoh cara menggunakan model yang telah di-fine-tune untuk memprediksi emosi dari sebuah teks baru.

**Teks Input**:
```
'I feel joyful and excited today!'
```

**Hasil Prediksi**:
Model ini akan menghasilkan probabilitas untuk setiap emosi. Dengan menggunakan *threshold* 0.5 (probabilitas > 50%), kita mendapatkan label yang paling relevan.

*   **Label yang Diprediksi**: `['joy']`

*   **Probabilitas Tertinggi**:
    ```
    joy 0.635
    excitement 0.473
    gratitude 0.052
    neutral 0.039
    admiration 0.035
    ```
    Seperti yang terlihat, `excitement` memiliki probabilitas tinggi tetapi sedikit di bawah threshold 0.5, sehingga tidak termasuk dalam label yang diprediksi.
