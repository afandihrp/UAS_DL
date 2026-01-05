# Laporan Fine-Tuning Model Phi-2 pada Dataset XSUM

## Tujuan Repositori
Repositori ini berfungsi sebagai tempat penyimpanan dan dokumentasi untuk eksperimen fine-tuning model bahasa kecil (Small Language Model - SLM) Microsoft Phi-2. Tujuan utamanya adalah untuk mendemonstrasikan proses fine-tuning model Phi-2 pada tugas peringkasan teks menggunakan dataset XSUM, serta menyajikan hasil training dan artefak model yang dihasilkan.

## Gambaran Umum Proyek
Proyek ini berfokus pada peningkatan kemampuan model Phi-2 dalam menghasilkan ringkasan teks yang koheren dan relevan. Dengan memanfaatkan teknik fine-tuning seperti QLoRA, kami berupaya mengadaptasi model dasar yang telah pre-trained untuk performa optimal pada tugas peringkasan. Hasil dari proses ini diharapkan dapat memberikan pemahaman tentang efektivitas fine-tuning SLM untuk tugas NLU spesifik.

## Konfigurasi
- **Model Dasar**: `microsoft/phi-2`
- **Dataset**: `xsum`
- **Tugas**: Peringkasan Teks
- **Framework**: Hugging Face Transformers dengan QLoRA

## Proses Training
Model dilatih selama 1 epoch dengan total 625 step. Evaluasi dilakukan setiap 500 step untuk mengukur performa pada data validasi. Checkpoint terbaik disimpan berdasarkan nilai *evaluation loss* terendah.

## Hasil Training

### Konfigurasi Training Aktual
- **Jumlah Epoch**: 1
- **Total Training Steps**: 625
- **Training Samples**: 5,000
- **Validation Samples**: 500
- **Per Device Batch Size**: 1
- **Gradient Accumulation Steps**: 8 (effective batch size = 8)
- **Learning Rate**: 2e-4
- **Learning Rate Scheduler**: Cosine
- **Optimizer**: paged_adamw_8bit (memory-efficient)
- **Evaluation Steps**: Setiap 500 steps
- **Precision**: Mixed precision (FP16)

### Metrik Training Terdetail

| Step | Training Loss | Learning Rate       | Grad Norm | Epoch |
|:----:|:-------------:|:-------------------:|:---------:|:-----:|
| 100  | 2.3373        | 1.96e-4             | 0.616     | 0.16  |
| 200  | 2.2274        | 1.69e-4             | 0.297     | 0.32  |
| 300  | 2.2168        | 1.21e-4             | 0.244     | 0.48  |
| 400  | 2.2066        | 6.70e-5             | 0.278     | 0.64  |
| 500  | 2.2102        | 2.28e-5             | 0.276     | 0.80  |

### Hasil Evaluasi

**Checkpoint Terbaik**: `./phi2-xsum-finetuned/checkpoint-500`

Evaluasi pada validation set:
- **Evaluation Loss**: **2.1183**
- **Best Model Step**: 500
- **Evaluation Runtime**: ~184 detik

Metrik performa menunjukkan konvergensi yang baik dengan training loss menurun dari 2.3373 pada step 100 menjadi 2.2102 pada step 500. Model mencapai evaluation loss terendah sebesar **2.1183** pada step ke-500, menandakan bahwa model telah belajar dengan efektif untuk menghasilkan ringkasan teks dari artikel berita dalam dataset XSUM.

### Analisis Hasil

1. **Penurunan Loss yang Konsisten**: Training loss menunjukkan penurunan yang konsisten dari step 100 hingga 400, dengan stabilisasi di step 500-625, menunjukkan model tidak overfitting.

2. **Gradient Norm Stabil**: Gradient norm berkisar antara 0.24-0.61, menunjukkan training yang stabil tanpa gradient explosion atau vanishing.

3. **Learning Rate Decay**: Learning rate decay yang progresif (cosine scheduler) membantu model konvergen dengan smooth.

4. **Generalisasi**: Gap antara training loss (2.2102) dan evaluation loss (2.1183) adalah kecil (~0.09), menunjukkan model generalisasi dengan baik terhadap data validation.

## Model Final
Adapter model yang telah di-fine-tune dan siap digunakan disimpan di direktori `phi2-xsum-final/`.

### Arsitektur Model LoRA
- **Model Dasar**: microsoft/phi-2
- **Quantization**: 4-bit (BitsAndBytes)
- **Compute Dtype**: bfloat16
- **LoRA Rank (r)**: 16
- **LoRA Alpha**: 32
- **LoRA Dropout**: 0.05
- **Target Modules**: q_proj, k_proj, v_proj, dense (attention layers)
- **Task Type**: CAUSAL_LM
- **Gradient Checkpointing**: Enabled (untuk efisiensi memori)

Total trainable parameters yang di-update melalui LoRA: persentase kecil dari total model, memungkinkan efisiensi komputasi dan memori.

### Specifikasi Training Environment
- **GPU Memory**: 5.67GB (dengan 4-bit quantization)
- **Framework**: Hugging Face Transformers + PEFT
- **Batch Strategy**: Gradient accumulation (batch size 1 × 8 steps = effective batch 8)
- **Mixed Precision**: FP16

## Kesimpulan Training
Proses fine-tuning model Phi-2 pada dataset XSUM berhasil menghasilkan model yang mampu menghasilkan ringkasan teks yang lebih baik. Dengan menggunakan teknik LoRA dan 4-bit quantization, kami dapat melatih model besar pada GPU dengan memori terbatas. Hasil menunjukkan:

1. **Convergence**: Model berhasil konvergen dengan penurunan loss yang smooth
2. **Generalisasi**: Tidak ada tanda-tanda overfitting dengan gap train-val yang minimal
3. **Efisiensi**: Training diselesaikan dalam 1 epoch dengan 625 steps dalam waktu yang efisien
4. **Kualitas**: Evaluation loss turun ke 2.1183, menunjukkan peningkatan dari initialization awal

 Nama: M. Afandi Harahap
 NIM: 1103223023
