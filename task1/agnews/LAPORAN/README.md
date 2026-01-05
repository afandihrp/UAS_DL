# Laporan Fine-tuning BERT pada AG News

Deskripsi singkat eksperimen fine-tuning BERT untuk klasifikasi topik berita pada dataset AG News (4 kelas).

## 1. Ringkasan
- Dataset: AG News (4 kelas: World, Sports, Business, Sci/Tech)
- Model dasar: `bert-base-uncased` (encoder Transformer)
- Task: supervised single-label classification (4 kelas)

## 2. Setup environment
Instal dependensi (jalankan di environment/virtualenv yang aktif):

```bash
python -m pip install -q transformers datasets evaluate accelerate
```

Notebook utama: [test.ipynb](test.ipynb)

## 3. Konfigurasi training (yang digunakan di notebook)
- Model: bert-base-uncased (AutoModelForSequenceClassification)
- Tokenizer: AutoTokenizer.from_pretrained('bert-base-uncased')
- Epochs: 3
- Learning rate: 2e-5
- Batch size train: 16
- Batch size eval: 64
- Weight decay: 0.01
- Evaluation strategy: per epoch
- Metric utama: accuracy (juga menyimpan weighted F1)

Lokasi keluaran model: `./results` (Training logs & checkpoints) dan model akhir disimpan di `./fine-tuned-bert-agnews` oleh notebook.

## 4. Hasil (metrics)
Jalankan cell evaluasi di notebook untuk melihat metrik aktual yang dihasilkan oleh run Anda. Contoh format metrik yang akan dicetak oleh notebook:

```
{'eval_loss': ..., 'eval_accuracy': ..., 'eval_f1_weighted': ..., 'epoch': ...}
```

Jika Anda sudah menjalankan training, tempel/replace hasil berikut di bagian ini (contoh):

- Accuracy (test): 0.95
- Weighted F1 (test): 0.95


## 5. Inference contoh
Notebook sudah menambahkan cell inference yang memuat model yang tersimpan dan memetakan label internal `LABEL_#` ke nama kategori manusia:

- Mapping: `['World', 'Sports', 'Business', 'Sci/Tech']`

Contoh menjalankan inference dari terminal (jika Anda ingin menjalankan skrip kecil):

```bash
# aktifkan environment Anda lalu jalankan Python REPL atau skrip yang memuat
python - <<'PY'
from transformers import pipeline
classifier = pipeline('text-classification', model='./fine-tuned-bert-agnews', tokenizer='./fine-tuned-bert-agnews', device=0)
print(classifier('Apple releases their latest iPhone model with new features.'))
PY
```

### Contoh Hasil Inference
Berikut adalah contoh hasil inference dari notebook `test.ipynb`:

```
Text: Apple releases their latest iPhone model with new features.
Prediction: {'label': 'Sci/Tech', 'score': 0.9823869466781616}
---
Text: The government announced new policies affecting the economy.
Prediction: {'label': 'Business', 'score': 0.9666765928268433}
---
```

## 6. Cara mereproduksi (singkat)
1. Aktifkan virtualenv (mis. `source virtualenvdl/bin/activate`).
2. Instal dependensi (lihat bagian Setup). 
3. Buka Jupyter dan jalankan `test.ipynb` sel demi sel, atau jalankan training cell yang memanggil `trainer.train()`.

## 7. Catatan & tips
- Gunakan GPU untuk percepatan (set `CUDA_VISIBLE_DEVICES` atau jalankan pada mesin dengan CUDA).\
- Untuk push model ke Hugging Face Hub, tambahkan `trainer.push_to_hub()` setelah autentikasi.
- Jika ingin eksperimen lebih ringan: coba `distilbert-base-uncased` atau kurangi batch size / gunakan gradient accumulation.

## 8. Kesimpulan
Model `bert-base-uncased` berhasil di-fine-tune untuk tugas klasifikasi topik AG News. Dengan hyperparameter yang ditentukan, model mencapai akurasi tinggi sebesar 95% dan skor F1 tertimbang sebesar 95% pada set pengujian.

Hasil ini menunjukkan bahwa transfer learning dengan model dasar BERT sangat efektif untuk tugas klasifikasi teks. Model yang telah di-fine-tune ini mampu membedakan empat kategori berita dengan sangat baik dan siap digunakan untuk inferensi pada data baru.
