# Fine-tuning T5 for Question Answering on SQuAD

## Tujuan Repositori (Repository Objective)
Repositori ini bertujuan untuk mendemonstrasikan proses fine-tuning model T5 (Text-To-Text Transfer Transformer) untuk tugas Question Answering (QA) menggunakan dataset SQuAD (Stanford Question Answering Dataset). Model yang telah di-fine-tune dapat menjawab pertanyaan berdasarkan konteks yang diberikan.

## Gambaran Umum Proyek (Project Overview)
Proyek ini melibatkan langkah-langkah berikut:
1.  Pemuatan dan eksplorasi dataset SQuAD.
2.  Tokenisasi data menggunakan T5 tokenizer.
3.  Konfigurasi model `T5ForConditionalGeneration` dari Hugging Face Transformers library.
4.  Fine-tuning model menggunakan `Seq2SeqTrainer` dari library Transformers.
5.  Evaluasi kinerja model dengan metrik standar QA.
6.  Melakukan inferensi untuk menghasilkan jawaban dari pertanyaan baru.

## Deskripsi Model dan Metrik (Model Description and Metrics)

### Model
Model yang digunakan adalah **`T5ForConditionalGeneration`** dengan arsitektur **`t5-base`** dari Hugging Face Transformers library. T5 adalah model encoder-decoder yang dilatih untuk berbagai tugas teks-ke-teks, menjadikannya pilihan yang sangat baik untuk tugas Question Answering.

### Metrik Evaluasi
Kinerja model dievaluasi menggunakan dua metrik utama yang umum digunakan dalam tugas Question Answering:

*   **Exact Match (EM)**: Mengukur persentase prediksi yang secara harfiah cocok dengan salah satu jawaban referensi. Nilai 1 menunjukkan kecocokan sempurna, dan 0 jika tidak ada kecocokan sama sekali.
*   **F1 Score (Token-level)**: Metrik ini mengukur tumpang tindih antara prediksi dan jawaban referensi. Ini dihitung sebagai rata-rata harmonik dari Precision dan Recall pada tingkat token, dengan memperhitungkan kata-kata yang relevan yang ditemukan dan kata-kata yang salah prediksi.

## Cara Menavigasi GitHub/Notebooks (How to Navigate GitHub/Notebooks)

Repositori ini berisi file Jupyter Notebook utama:
*   `test.ipynb`: Notebook ini adalah panduan langkah demi langkah yang lengkap untuk seluruh alur kerja proyek, mulai dari pemuatan data, preprocessing, fine-tuning model, hingga evaluasi dan inferensi. Disarankan untuk menjalankan notebook ini secara berurutan untuk memahami setiap langkah.

## Hasil Training Model (Model Training Results)

Model ini dikonfigurasi untuk fine-tuning pada dataset SQuAD dengan tujuan mencapai kinerja tinggi dalam tugas Question Answering. Setelah proses training (`trainer.train()` dieksekusi), metrik Exact Match dan F1 Score akan dihitung selama fase evaluasi.

*   **Epochs**: 1
*   **Batch Size per device (Train)**: 8 (jika menggunakan GPU), 4 (jika menggunakan CPU)
*   **Batch Size per device (Eval)**: 16 (jika menggunakan GPU), 8 (jika menggunakan CPU)

## Analisa Hasil Training dan Kesimpulan

Berdasarkan sampel kecil dari hasil inferensi yang ditampilkan di notebook `test.ipynb`, performa model ini **cukup bagus dan menjanjikan**.

### Kelebihan:
*   Model ini berhasil menjawab sebagian besar pertanyaan dengan benar dan akurat. Contohnya, pada pertanyaan "Which NFL team represented the AFC at Super Bowl 50?", model dengan tepat menjawab "Denver Broncos".
*   Model juga dapat mengekstrak informasi yang lebih panjang dan detail seperti pada pertanyaan "Where did Super Bowl 50 take place?", di mana jawabannya adalah "Levi's Stadium in the San Francisco Bay Area at Santa Clara, California". Meskipun jawaban referensinya lebih singkat ("Santa Clara, California"), jawaban model secara teknis benar dan lebih informatif. Ini adalah contoh di mana metrik *Exact Match* akan gagal, tetapi *F1 Score* akan memberikan nilai yang tinggi.

### Kekurangan:
*   Model ini tidak sempurna. Ada contoh di mana model gagal menangkap jawaban yang tepat. Misalnya, untuk pertanyaan "What was the theme of Super Bowl 50?", model menjawab "gold", padahal jawaban yang benar adalah `"golden anniversary"`. Model sepertinya hanya menangkap kata kunci tanpa memahami konteks sepenuhnya.

### Kesimpulan:
Secara keseluruhan, untuk model yang baru di-fine-tune, hasil ini sangat menjanjikan. Namun, untuk penilaian yang lebih komprehensif, sangat disarankan untuk menjalankan evaluasi pada seluruh set validasi menggunakan fungsi `compute_metrics` yang telah disiapkan di dalam notebook. Ini akan memberikan gambaran yang lebih akurat tentang seberapa baik kinerja model secara umum melalui metrik F1 dan Exact Match.

NAMA: M. Afandi Harahap
NIM: 1103223023